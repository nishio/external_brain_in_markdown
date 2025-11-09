---
title: "npm installだけを使用中止"
---


<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
sh

```
# 1) ラッパー設置用ディレクトリをPATH先頭に
mkdir -p ~/.bin
if ! grep -q 'export PATH="$HOME/.bin:$PATH"' ~/.bashrc 2>/dev/null; then
  echo 'export PATH="$HOME/.bin:$PATH"' >> ~/.bashrc
fi
if [ -n "$ZSH_VERSION" ] && ! grep -q 'export PATH="$HOME/.bin:$PATH"' ~/.zshrc 2>/dev/null; then
  echo 'export PATH="$HOME/.bin:$PATH"' >> ~/.zshrc
fi

# 2) ラッパー本体を作成
cat > ~/.bin/npm <<'SH'
#!/usr/bin/env bash
# --- block only: npm install / i / ci ---
# 先頭のオプション(--xx)を飛ばして最初のサブコマンドを抽出
sub=""
for a in "$@"; do
  case "$a" in --*) ;; *) sub="$a"; break ;; esac
done
case "$sub" in
  install|i|ci)
    echo "npm $sub は禁止です。pnpmを使いましょう。" >&2
    exit 127
    ;;
esac

# このラッパー自身のディレクトリをPATHから除外して「本物のnpm」を探索
SELF_DIR="$(cd "$(dirname "$0")" && pwd)"
CLEAN_PATH="$(printf "%s" "$PATH" | awk -v RS=: -v ORS=: -v d="$SELF_DIR" '$0!=d' | sed 's/:$//')"
REAL_NPM="$(PATH="$CLEAN_PATH" command -v npm)"
if [ -z "$REAL_NPM" ]; then
  echo "本物の npm が見つかりません。" >&2
  exit 127
fi
exec "$REAL_NPM" "$@"
SH
chmod +x ~/.bin/npm

# 3) シェルを再読み込み
exec $SHELL -l

# 動作確認
npm install        # => 拒否される
npm i              # => 拒否される
npm ci             # => 拒否される
npm run dev        # => 通る
```


