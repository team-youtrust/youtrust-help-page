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

1. ブランチを作成して `docs/` 配下のMarkdownを編集
2. pushしてPRを作成
3. PRの説明欄に変更ファイル一覧と差分が自動追記される
4. `docs/` や `mkdocs.yml` の変更がある場合、`published-pages` ブランチの `pr-preview/pr-{番号}/` にプレビュー用HTMLが自動生成され、PRにプレビューURLがコメントされる
5. チームがプレビューURLで表示を確認・レビュー
6. PRをマージ → 本番サイトが自動更新、プレビューは自動削除される
