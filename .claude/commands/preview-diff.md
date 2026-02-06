変更されたドキュメントのスクリーンショットを撮影し、PRコメントに投稿します。

## 手順

### 1. 変更ファイルの検出
`git diff --name-only main` で `docs/` 配下および `mkdocs.yml` の変更を検出してください。
変更がなければ「変更されたドキュメントはありません」と表示して終了してください。

スクリーンショットの対象ページを決定します：
- `.md` ファイルが変更された場合 → そのページを対象
- `extra.css` や `mkdocs.yml` のみの変更 → 全ページに影響するため、トップページ（index）を対象

### 2. ローカルサーバーの起動
すでにポート8000で起動中か確認し、起動していなければ以下を実行：
```
kill $(lsof -t -i:8000) 2>/dev/null
source .venv/bin/activate && mkdocs serve &
```
サーバーが応答するまで待ってください（5秒程度）。

### 3. スクリーンショットの撮影
chrome-devtools MCPを使って、変更された各ページのスクリーンショットを撮影します。

- ベースURL: `http://127.0.0.1:8000/youtrust-help-page/`
- `docs/index.md` → `/youtrust-help-page/`
- `docs/faq.md` → `/youtrust-help-page/faq/`
- その他のファイルも同様に `docs/{name}.md` → `/youtrust-help-page/{name}/`

`tmp/` ディレクトリを作成し、各ページについて：
1. `navigate_page` でページに移動
2. ページの読み込みを待つ
3. `take_screenshot` でスクリーンショットを `tmp/{ファイル名}.png` に保存（fullPage: true）

### 4. 画像のアップロード
GitHub Contents APIを使い、`screenshots` ブランチに画像をアップロードします。

PR番号を `gh pr view --json number -q '.number'` で取得し、各画像について：
```bash
BASE64=$(base64 -i tmp/{ファイル名}.png | tr -d '\n')
gh api repos/{owner}/{repo}/contents/pr-{PR番号}/{ファイル名}.png \
  -X PUT \
  -f message="PR #{PR番号} screenshot: {ファイル名}" \
  -f content="$BASE64" \
  -f branch="screenshots"
```

既にファイルが存在する場合は、先にSHAを取得して上書き：
```bash
SHA=$(gh api repos/{owner}/{repo}/contents/pr-{PR番号}/{ファイル名}.png?ref=screenshots --jq '.sha' 2>/dev/null)
# SHAが取れたら -f sha="$SHA" を追加
```

画像URLは `https://raw.githubusercontent.com/{owner}/{repo}/screenshots/pr-{PR番号}/{ファイル名}.png` になります。

### 5. 変更内容の要約作成
`git diff main` の内容を分析し、各ページについて以下をまとめてください：
- 何がどのように変わったか（変更前 → 変更後）
- 表形式（テーブル）で見やすく整理

### 6. PRコメントへの投稿
スクリーンショットと変更内容の要約を1つのコメントにまとめて投稿：

```
gh pr comment {PR番号} --body "$(cat <<'EOF'
## プレビュースクリーンショット

### {ページ名}
![{ファイル名}]({画像URL})

### 変更内容
| 変更箇所 | 変更前 | 変更後 |
|---------|-------|-------|
| {箇所} | {変更前の内容} | {変更後の内容} |

撮影日時: {現在のJST日時}
EOF
)"
```

複数ページがある場合は1つのコメントにまとめてください。

### 7. 完了報告
撮影したページ一覧とPRコメントのURLを表示してください。
