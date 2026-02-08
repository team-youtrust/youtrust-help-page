# YOUTRUST ヘルプページ

YOUTRUSTのヘルプページです。[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)で構築し、GitHub Pagesで公開しています。

## ローカル環境のセットアップ

```bash
docker compose up
```

http://localhost:8000 でプレビューを確認できます。ファイルを編集すると自動でリロードされます。

## ページの編集・追加

`docs/` 配下のMarkdownファイルを編集してください。

```
docs/
├── user/                 # 一般ユーザー向けヘルプ
│   ├── account/          #   アカウント設定
│   ├── profile/          #   登録プロフィール
│   ├── notification/     #   通知
│   ├── privacy/          #   プロフィールの公開範囲
│   ├── connection/       #   つながり
│   ├── post/             #   投稿
│   ├── message/          #   応募・メッセージ
│   ├── community/        #   コミュニティ
│   └── other/            #   その他
└── recruiter/            # 公式リクルーター向けヘルプ
    ├── guide/            #   活用ガイド
    └── faq/              #   よくあるご質問
        ├── admin/        #     管理者設定
        ├── search/       #     人材を探す
        ├── scout/        #     スカウト
        ├── candidate-management/ # 候補者管理
        ├── communication/ #    コミュニケーション
        ├── post/         #     投稿
        ├── company-page/ #     企業ページ
        ├── connection/   #     つながり
        ├── notification/ #     通知
        ├── billing/      #     料金・プラン
        └── talent-pick/  #     タレントピック
```

ナビゲーションの順序は `mkdocs.yml` の `nav` セクションで管理しています。

## 公開までの流れ

1. ブランチを作成して `docs/` 配下のMarkdownを編集
2. pushしてPRを作成
3. PRの説明欄に変更ファイル一覧と差分が自動追記される
4. `docs/` や `mkdocs.yml` の変更がある場合、`published-pages` ブランチの `pr-preview/pr-{番号}/` にプレビュー用HTMLが自動生成され、PRにプレビューURLがコメントされる
5. チームがプレビューURLで表示を確認・レビュー
6. PRをマージ → 本番サイトが自動更新、プレビューは自動削除される
