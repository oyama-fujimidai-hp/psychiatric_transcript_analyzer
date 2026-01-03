# Psychiatric Transcript Analyzer

This repository contains tools for analyzing psychiatric session transcripts.

## Google Cloud Run へのデプロイ方法

このプロジェクトは Docker を使用して Google Cloud Run にデプロイできます。

### 1. 前提条件
- [Google Cloud プロジェクト](https://console.cloud.google.com/)が作成されていること
- [Google Cloud CLI (gcloud)](https://cloud.google.com/sdk/docs/install) がインストールされていること

### 2. デプロイ手順

以下のコマンドを実行してデプロイします。

```bash
# プロジェクトIDの設定
gcloud config set project [studious-lyceum-483104-u8] # <<< ご自身のプロジェクトIDに置き換えてください

# Cloud Run へのデプロイ
gcloud run deploy psychiatric-analyzer \
  --source . \
  --platform managed \
  --region asia-northeast1 \
  --allow-unauthenticated
```

デプロイが完了すると、サービスにアクセスするための URL が表示されます。

### 3. ローカルでの実行（確認用）

Docker を使用してローカルで動作確認を行う場合は以下の通りです。

```bash
# イメージのビルド
docker build -t psychiatric-analyzer .

# コンテナの起動
docker run -p 8080:8080 psychiatric-analyzer
```
ブラウザで `http://localhost:8080` にアクセスしてください。

