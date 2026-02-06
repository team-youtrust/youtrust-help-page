# YOUTRUST ヘルプページ

YOUTRUSTのヘルプページです。[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)で構築し、GitHub Pagesで公開しています。

## ローカル環境のセットアップ

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

http://127.0.0.1:8000/youtrust-help-page/ で確認できます。

## ページの編集・追加

`docs/` 配下のMarkdownファイルを編集してください。

```
docs/
├── index.md           # トップページ
├── faq.md             # よくあるご質問
├── account.md         # アカウント設定
├── profile.md         # 登録プロフィール
├── notification.md    # 通知
├── privacy.md         # プロフィールの公開範囲
├── connection.md      # つながり
├── post.md            # 投稿
├── application.md     # 応募・メッセージ
├── community.md       # コミュニティ
└── other.md           # その他
```

ナビゲーションの順序は `mkdocs.yml` の `nav` セクションで管理しています。

## 公開までの流れ

1. ブランチを作成してMarkdownを編集
2. pushしてPRを作成
3. PRにプレビューURLが自動コメントされる
4. チームがプレビューを確認・レビュー
5. PRをマージ → 本番サイトが自動更新

## GitHub Pages設定（初回のみ）

Settings → Pages → Source → **Deploy from a branch** → `gh-pages` / `/ (root)`
