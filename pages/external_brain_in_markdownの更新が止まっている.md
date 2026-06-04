---
title: "external_brain_in_markdownの更新が止まっている"
---


(Codex)
止まった理由は、更新元の GitHub Actions が inactivity で自動無効化されたためです。

確認結果:
- nishio/external_brain_in_markdown 自体には workflow はありません。
- 実際の同期元は nishio/from_scrapbox の update_markdown.yml。
- その workflow の状態が disabled_inactivity になっていました。
- 最後の成功 run は 2026-01-24 20:06 UTC、JST では 2026-01-25 05:06。
- from_scrapbox の最後の commit は 2025-11-25 で、そこから約 60 日後に止まっています。
- GitHub 公式 docs にも、public repo では「60 日間 repository activity がない scheduled workflow は自動で無効化される」とあります: GitHub Docs

復旧だけなら:
- gh workflow enable update_markdown.yml --repo nishio/from_scrapbox
- gh workflow run update_markdown.yml --repo nishio/from_scrapbox

ただし from_scrapbox 側に定期的な repository activity がないと、また 60 日後に止まります。根本対策は、workflow を更新先 repo 側へ移すか、from_scrapbox に定期的な keepalive commit を入れる構成にすることです。
