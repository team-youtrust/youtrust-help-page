# YOUTRUST ヘルプページ

YOUTRUSTのヘルプページです。[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)で構築し、GitHub Pagesで公開しています。

## ローカル環境のセットアップ

```bash
# Python仮想環境を作成（プロジェクト専用の環境を用意）
python3 -m venv .venv

# 仮想環境を有効化（以降のpipコマンドはこの環境にインストールされる）
source .venv/bin/activate

# 必要なパッケージをインストール（MkDocs、Material for MkDocsなど）
pip install -r requirements.txt

# ローカルサーバーを起動
mkdocs serve
```

http://127.0.0.1:8000/youtrust-help-page/ で確認できます。

### リアルタイム反映オプション

ドキュメント（Markdown）やCSS/テーマの変更をリアルタイムで反映させたい場合は、以下のオプションを使用してください。

```bash
mkdocs serve --watch-theme --livereload
```

- `--watch-theme`: テーマファイル（CSS等）の変更を監視
- `--livereload`: ドキュメントやファイル変更時にブラウザを自動リロード

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
        ├── admin/        #     リクルーター管理画面
        ├── search/       #     タレントを探す
        ├── scout/        #     スカウト
        ├── candidate-management/ # 候補者管理
        ├── communication/ #    コミュニケーション
        ├── post/         #     投稿
        ├── company-page/ #     カンパニーページ
        ├── connection/   #     つながり
        ├── notification/ #     通知
        ├── billing/      #     料金・プラン
        └── talent-pick/  #     タレントピック
```

ナビゲーションの順序は `mkdocs.yml` の `nav` セクションで管理しています。

### アイコンの使い方

Markdownファイル内で `:アイコン名:` の形式でアイコンを挿入できます。

| プレフィックス        | 例                         | アイコン一覧                                    |
| --------------------- | -------------------------- | ----------------------------------------------- |
| `:material-`          | `:material-home:`          | https://pictogrammers.com/library/mdi/          |
| `:fontawesome-solid-` | `:fontawesome-solid-user:` | https://fontawesome.com/icons?d=gallery&s=solid |
| `:octicons-`          | `:octicons-gear-16:`       | https://primer.style/octicons/                  |

## 公開までの流れ

1. ブランチを作成して `docs/` 配下のMarkdownを編集
2. pushしてPRを作成
3. PRの説明欄に変更ファイル一覧と差分が自動追記される
4. `docs/` や `mkdocs.yml` の変更がある場合、`published-pages` ブランチの `pr-preview/pr-{番号}/` にプレビュー用HTMLが自動生成され、PRにプレビューURLがコメントされる
5. チームがプレビューURLで表示を確認・レビュー
6. PRをマージ → 本番サイトが自動更新、プレビューは自動削除される
