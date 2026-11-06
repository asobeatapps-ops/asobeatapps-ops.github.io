# ASOBEAT 公式トップページ

公開先: https://asobeatapps-ops.github.io/

このディレクトリを **`asobeatapps-ops/asobeatapps-ops.github.io`** リポジトリのルートとして公開します。`gamehome` リポジトリの中に配置しても、登録URLの404は解消しません。

## 構成と影響範囲

- `index.html`: 公式紹介、ゲームホームへの導線、既存プライバシーポリシーへのリンク、AdSense確認コードの挿入箇所。
- `style.css`: ルートのトップページ専用スタイル。外部フォント・JavaScript・フレームワークは不要。
- `.nojekyll`: 静的ファイルをそのまま配信。

ゲーム一覧・検索・TOP5は既存の https://asobeatapps-ops.github.io/gamehome/ で提供します。ゲームのデータ・アプリコード・公開URL・広告配置・Cloudflare設定は変更しません。トップページには自動転送やiframeを使わず、本文と通常のリンクを置いています。

プライバシーポリシーも `/gamehome/privacy.html` を参照し、複製しません。今後ルートサイトも含めた適用範囲や計測・広告サービスの説明を更新する場合は、元のポリシーを編集してください。

## GitHub Pagesへの公開

1. GitHubでアカウント `asobeatapps-ops` の `asobeatapps-ops.github.io` リポジトリを確認します。既存の場合は内容・Pages設定を確認してから差分を取り込み、上書きしないでください。未作成なら、この名前の公開リポジトリを作成します。
2. このディレクトリのファイルを `main` ブランチのルートにコミット・pushします。
3. リポジトリの **Settings → Pages → Build and deployment** で **Deploy from a branch**、`main`、`/ (root)` を選択して保存します。カスタムドメインは設定しません。
4. Pagesのデプロイ成功後、以下を確認します。

```sh
curl -I https://asobeatapps-ops.github.io/
curl -I https://asobeatapps-ops.github.io/style.css
curl -I https://asobeatapps-ops.github.io/gamehome/
curl -I https://asobeatapps-ops.github.io/gamehome/privacy.html
```

すべてHTTP 200であること、ルートからゲームホーム・ポリシーへ移動できることを確認してください。HTTP 200だけで機能検証は完了しません。ゲームホームで一覧・検索・TOP5も確認します。

## AdSense所有権確認コード

発行済みコード・パブリッシャーIDはこの実装に含めていません。架空のIDを登録しないでください。

1. AdSense管理画面で登録サイト `https://asobeatapps-ops.github.io/` の所有権確認方法を確認します。
2. HTMLのコードまたはメタタグによる確認を選んだ場合、発行されたコードを `index.html` の `<head>` 内にある `ADSENSE_VERIFICATION_START` / `ADSENSE_VERIFICATION_END` の**コメントの直後、コメントの外側**に、そのまま追加します。既存の広告配置は変更しません。
3. Pagesを再公開し、公開ルートの「ページのソース」でコードが確認できることを確かめてから、AdSense管理画面で確認します。JavaScriptで後から挿入する実装は不要です。
4. AdSense管理画面で `ads.txt` 方式や追加対応を指定された場合は、その指示に従って、発行された正しい内容をルートの `ads.txt` に設置します。このリポジトリには空や仮の `ads.txt` は置いていません。

確認用スクリプトを採用する場合は、実際の広告・Cookie等の動作に合わせてポリシーや必要な同意管理も確認してください。確認コード設置、所有権確認、審査への提出、審査合格は別の段階です。ページ公開は審査合格を保証しません。

## ローカル確認

本番と同じパスで導線を確認するには、既存 `gamehome` のクローンとこのディレクトリを使って、配信用ディレクトリを用意します。

```sh
mkdir -p /tmp/asobeat-preview
cp index.html style.css /tmp/asobeat-preview/
ln -s /workspace/gamehome /tmp/asobeat-preview/gamehome
python3 -m http.server 8000 --directory /tmp/asobeat-preview
```

http://localhost:8000/ を開きます。ローカルの一覧・検索・APIモック検証と、本番公開後のHTTP/CORS・AdSenseの確認は区別してください。
