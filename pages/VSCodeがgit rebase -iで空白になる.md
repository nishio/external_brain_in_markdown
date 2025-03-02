

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>when I use `git rebase -i`, VSCode generate empty page. How to fix it?
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>When using git rebase -i, Git opens an editor for you to modify the list of commits. If you've configured Git to use VS Code as your editor and you're seeing an empty page, there may be an issue with how Git and VS Code are configured to interact.
- Here are some steps to troubleshoot and fix the issue: ...
- `$ git config --global core.editor "code --wait"`
    - The --wait flag is important because it keeps the VS Code instance open until you're finished editing.

[[GPT4に技術を聞く]]
