# 開発環境用の s3 ストレージ

## Quick Start

1. `.env`を以下のように作成する

   ```.env
   MINIO_ROOT_USER=<your_username>
   MINIO_ROOT_PASSWORD=<your_password>
   MINIO_PORT=9000
   MINIO_CONSOLE_PORT=9001
   MINIO_CLIENT_ACCESS_KEY=<your_access_key>
   MINIO_CLIENT_SECRET_KEY=<your_secret_key>
   ```

1. 環境変数の export

   ```
   export `cat .env`
   ```

1. MinIO サーバーを起動
   <details>
   <summary>dockerの場合</summary>
   <pre><code>$ docker-compose up -d</code></pre>
   </details>

   <details>
   <summary>brewの場合</summary>
   <pre><code>$ brew install minio/stable/minio
   $ minio server ./data \
   --address :${MINIO_PORT} \
   --console-address :${MINIO_CONSOLE_PORT}</code></pre>
    </details>

1. minio client の準備
   ```
   $ brew install minio/stable/mc
   $ mc alias set local http://127.0.0.1:${MINIO_PORT} $MINIO_ROOT_USER $MINIO_ROOT_PASSWORD
   $ mc admin info local
   ```
1. access-key の作成

   ```
   $ mc admin user svcacct add \
   --access-key $MINIO_CLIENT_ACCESS_KEY \
   --secret-key $MINIO_CLIENT_SECRET_KEY \
   local $MINIO_ROOT_USER
   ```

1. test.ipynb を実行
   バケットの作成やファイルのアップロードができることが確認できる。

1. サーバーの停止
   <details>
   <summary>dockerの場合</summary>
   <pre><code>$ docker-compose down</code></pre>
   </details>

   <details>
   <summary>brewの場合</summary>
   <code>Ctrl + C</code>で
   </details>

## GUI からの操作

1. http://127.0.0.1:{MINIO_PORT} にアクセスする

1. `.env`で指定した Username と Password でログイン
