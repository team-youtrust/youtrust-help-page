変更されたドキュメントのスクリーンショットを撮影し、PRコメントに投稿します。

## 手順

### 1. 変更ファイルの検出
`git diff --name-only HEAD~1` または `git diff --name-only main` で `docs/` 配下の変更された `.md` ファイルを検出してください。
変更がなければ「変更されたドキュメントはありません」と表示して終了してください。

### 2. ローカルサーバーの起動
すでにポート8000で起動中か確認し、起動していなければ以下を実行：
```
source .venv/bin/activate && mkdocs serve &
```
サーバーが応答するまで待ってください。

### 3. スクリーンショットの撮影
chrome-devtools MCPを使って、変更された各ページのスクリーンショットを撮影します。

- ベースURL: `http://127.0.0.1:8000/youtrust-help-page/`
- `docs/index.md` → `/youtrust-help-page/`
- `docs/faq.md` → `/youtrust-help-page/faq/`
- `docs/account.md` → `/youtrust-help-page/account/`
- その他のファイルも同様に `docs/{name}.md` → `/youtrust-help-page/{name}/`

各ページについて：
1. `navigate_page` でページに移動
2. ページの読み込みを待つ
3. `take_screenshot` でスクリーンショットを `tmp/{ファイル名}.png` に保存（fullPage: true）

### 4. PRコメントへの投稿
現在のブランチに紐づくPRを `gh pr view --json number` で取得し、以下の形式でコメントを投稿：

```
gh pr comment {PR番号} --body "$(cat <<'EOF'
## プレビュースクリーンショット

{各ページのスクリーンショットをGitHubにアップロードして埋め込む}

撮影日時: {現在のJST日時}
EOF
)"
```

スクリーンショット画像は `gh api` を使ってPRコメントに添付するか、Base64でインライン埋め込みしてください。

### 5. 完了報告
撮影したページ一覧とPRコメントのURLを表示してください。
