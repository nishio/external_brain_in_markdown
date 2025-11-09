---
title: "SensemakerにYouTubeの高評価だけ入れたらどうなる？"
---

from [[Jigsaw Sensemakerとtttc-light-js勉強会]]
SensemakerにYouTubeの高評価だけ入れたらどうなる？

YouTubeからは高評価データは取れるが低評価データは取れない
高評価データだけを投票に入れたらどうなるか

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
YouTube由来で高評価だけを賛成票として投票結果データに入れた場合、以下のような処理の流れになります：

1. データ読み込み段階（runner_utils.ts: 347-365行目）
getVoteInfoFromCsvRow関数がCSVデータをVoteTallyオブジェクトに変換します：
ts

```typescript
return new VoteTally(Number(row["agrees"]), Number(row["disagrees"]), Number(row["passes"]));
```

YouTube由来のデータの場合：
- agrees = 高評価数
- disagrees = 0（または空欄→NaNになるので注意が必要）
- passes = 0（または空欄→NaNになるので注意が必要）

2. 統計計算段階（stats/stats_util.ts）
投票率の計算時にpassCount || 0で未定義値を0として扱います：
ts

```typescript
// library/src/stats/stats_util.ts: 58-65行目
export function getPassRate(voteTally: VoteTally, asProbabilityEstimate: boolean = true): number {
	const totalCount = voteTally.getTotalCount(true);
	if (asProbabilityEstimate) {
		return ((voteTally.passCount || 0) + 1) / (totalCount + 2);
	} else {
		return (voteTally.passCount || 0) / totalCount;
	}
}
```

YouTube由来データでは：
- 賛成率 ≈ 100%（高評価がある場合）
- 反対率 ≈ 0%
- パス率 ≈ 0%

3. フィルタリング段階（summary_stats.ts: 55-59行目）
ts

```typescript
this.filteredComments = comments.filter(isCommentWithVoteInfoType).filter((comment) => {
	return getCommentVoteCount(comment, true) >= this.minVoteCount;
});
```


重要：minVoteCount = 20なので、高評価が20未満のコメントは分析対象外になります。
- これは良くないな<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

4. Common Ground（共通認識）の抽出（majority_vote.ts: 88-95行目）
ts

```typescript
getCommonGroundAgreeComments(k: number = this.maxSampleSize) {
	return this.topK(
		(comment) => this.getCommonGroundAgreeScore(comment),
		k,
		(comment: CommentWithVoteInfo) => this.meetsCommonGroundAgreeThreshold(comment)
	);
}
```

minCommonGroundProb = 0.7（70%）がしきい値です。YouTube由来で高評価があるコメントは賛成率がほぼ100%なので、ほぼすべてがCommon Groundとして抽出されます。高評価数が多いコメントほど優先されます。

5. Differences of Opinion（意見の相違）の抽出（majority_vote.ts: 189-210行目）
ts

```typescript
getDifferenceOfOpinionComments(k: number = this.maxSampleSize) {
	return this.topK(
		(comment) => this.getDifferenceOfOpinionScore(comment),
		k,
		(comment: CommentWithVoteInfo) =>
			getTotalAgreeRate(comment.voteInfo, this.includePasses, this.asProbabilityEstimate) >=
			this.minDifferenceProb &&
			getTotalAgreeRate(comment.voteInfo, this.includePasses, this.asProbabilityEstimate) <=
			this.maxDifferenceProb &&
			// ... 同様の条件がdisagree rateにも適用される
	);
}
```

賛成率と反対率が両方とも40%-60%の範囲にある必要があります。YouTube由来データでは反対率≈0%なので、この条件を満たすコメントはほぼ存在せず、意見の相違は検出されません。
- これも良くないな<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - 機能があると見せかけて実質的には機能してない

6. サマリー生成（summarization_subtasks/topics.ts: 369-397行目）
Common Groundコメントが見つかった場合はLLMで要約、見つからない場合は以下のメッセージが表示されます：
ts

```typescript
text = this.input.getCommonGroundNoCommentsMessage();
// "No statements met the thresholds necessary to be considered as a point of common ground
// (at least 20 votes, and at least 70% agreement)."
```


まとめ
YouTube由来で高評価だけを賛成票として入れた場合：
- ✅ 処理される内容：
    - 高評価20以上のコメントが分析対象
    - それらは「共通認識（Common Ground）」として扱われる
    - 高評価数が多いコメントほど重要視される
- ❌ 処理されない内容：
    - 高評価20未満のコメントは除外される
    - 「意見の相違（Differences of Opinion）」はほぼ検出されない
    - 反対意見や議論の分析はできない

