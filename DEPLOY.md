# Google Cloud Run へのデプロイ手順

このプロジェクトを Google Cloud Run にデプロイするための手順です。

## 前提条件

1.  [Google Cloud プロジェクト](https://console.cloud.google.com/)が作成されていること。
2.  [Google Cloud CLI (gcloud)](https://cloud.google.com/sdk/docs/install) がインストールされ、初期化されていること。
3.  Cloud Run、Cloud Build、Artifact Registry の API が有効になっていること。

## デプロイ方法

### 1. Artifact Registry のリポジトリ作成（初回のみ）

イメージを保存するためのリポジトリを作成します。

```bash
gcloud artifacts repositories create cloud-run-source-deploy \
    --repository-format=docker \
    --location=asia-northeast1 \
    --description="Docker repository for Cloud Run"
```

### 2. Cloud Build を使用したデプロイ

Cloud Build を使用してビルドとデプロイを行います。
※ 初回実行時に権限エラー（403 Forbidden）が出る場合は、[方法3] の直接デプロイを試すか、Cloud Build サービスアカウントにストレージの権限を付与してください。

```bash
gcloud builds submit --config cloudbuild.yaml --substitutions=REPO_NAME=psychiatric-transcript-analyzer
```

### 3. 直接ソースからデプロイする場合（推奨）

Cloud Build の権限設定をスキップして、最も簡単にデプロイする方法です。

```bash
gcloud run deploy psychiatric-transcript-analyzer \
    --source . \
    --region asia-northeast1 \
    --allow-unauthenticated
```

## 設定のカスタマイズ

- **ポート番号**: `Dockerfile` および `nginx.conf` で `8080` ポートを使用するように設定されています（Cloud Run のデフォルト）。
- **リージョン**: `cloudbuild.yaml` の `_GCR_REGION` を変更することでデプロイ先を変更できます。
