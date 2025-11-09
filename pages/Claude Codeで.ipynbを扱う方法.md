---
title: "Claude Codeで.ipynbを扱う方法"
---

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
- Claude Codeで.ipynbを扱う「良い方法」
    - 結論: 安定性と再現性を重視するなら Jupytextで`.py:percent`とペア→Claude Codeには`.py`を編集させ、同期で`.ipynb`を更新。ノート直編集は可能だがセル順序バグなどの報告があるため、MCPサーバ併用かJupytext経由が無難です。([Anthropic](https://www.anthropic.com/engineering/claude-code-best-practices?utm_source=chatgpt.com))

1) そのままノートを読ませて軽く編集（小規模向け）
- VS Codeで`.ipynb`を開きつつ、Claude Codeにファイル参照（例: `@notebooks/analysis.ipynb`）で内容を読ませる。セル一覧→該当セルだけ編集→パッチ適用の順で指示。([Anthropic](https://www.anthropic.com/engineering/claude-code-best-practices?utm_source=chatgpt.com))
- 注意: 編集が反映されない/セル順が乱れる報告あり。重作業は避ける。([Reddit](https://www.reddit.com/r/ClaudeCode/comments/1mwd2qj/claude_code_and_jupyter_notebooks_in_vscode/?utm_source=chatgpt.com))
    - これこれ、セルを逆順で突っ込んでくるんだよね<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

ノイズ削減（強推奨）
bash

```
# 出力を一旦消去（巨大base64画像でトークン圧迫を防ぐ）
jupyter nbconvert --clear-output --inplace your.ipynb
```

([Stack Overflow](https://stackoverflow.com/questions/17077494/how-do-i-convert-a-ipython-notebook-into-a-python-file-via-commandline?utm_source=chatgpt.com))

2) Jupytextで.ipynb⇄.pyをペアリング（最推奨）
Claude Codeはスクリプト編集が得意。`.ipynb`を`.py:percent`形式と同期し、Claudeには`.py`を編集させる。完了後に同期でノートを更新。
bash

```
pipx install jupytext nbconvert nbstripout
# ipynbとpy:percentをペアに
jupytext --set-formats ipynb,py:percent your.ipynb
# 以後は編集後に双方向同期
jupytext --sync your.ipynb
# 余計な出力は常に削除（任意）
nbstripout --install
```

([jupytext.readthedocs.io](https://jupytext.readthedocs.io/?utm_source=chatgpt.com))
ポイント
- `.py:percent`はセル境界が明示（`# %%`）で差分管理に強い。([jupytext.readthedocs.io](https://jupytext.readthedocs.io/en/latest/formats-scripts.html?utm_source=chatgpt.com))
- Claudeには**`.py`のみ**を渡して編集→`jupytext --sync`で`.ipynb`へ反映。
- 大規模ノート/反復改修に一番安定。

3) MCPサーバでセル単位操作（Claude Desktop併用）
Claude（特にClaude Desktop）はMCP経由で外部ツールと連携可。Jupyter向けMCPサーバを入れると、ノートのセル列挙・読取・編集などを道具として安全に実行できる。
代表例:
- `UsamaK98/python-notebook-mcp`（セルの追加/編集/読取ツールを提供）([GitHub](https://github.com/UsamaK98/python-notebook-mcp))
- `datalayer/jupyter-mcp-server`（各種MCPクライアント対応）([GitHub](https://github.com/datalayer/jupyter-mcp-server?utm_source=chatgpt.com))
導入イメージ（抜粋）:
bash

```
git clone https://github.com/UsamaK98/python-notebook-mcp
cd python-notebook-mcp
uv venv && uv pip install -r requirements.txt
fastmcp install server.py --name "Jupyter Notebook MCP"
# Claude DesktopのDeveloper設定で有効化
```

（MCPはAnthropicが公開する標準プロトコル。Claude製品群と相性が良い）([The Verge](https://www.theverge.com/2024/11/25/24305774/anthropic-model-context-protocol-data-sources?utm_source=chatgpt.com))

プロンプト/運用Tips
- 編集は「セル特定→パッチ」で。例:
「`@analysis.ipynb`のセル一覧を番号/タイプ/先頭1行で出力→“preprocess”と書き出すセルだけを変更→変更差分を説明→適用」
- 巨大出力は事前に削除（上記`nbconvert --clear-output`）し、画像は外部ファイル化して参照に。
- 壊れやすいメタデータ（`cell_id`等）は触らせない旨を明記。
- Jupytext派は、`.py`側でレビュー→`--sync`で確定、を習慣化。
