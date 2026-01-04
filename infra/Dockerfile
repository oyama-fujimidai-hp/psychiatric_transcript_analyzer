FROM nginx:alpine

# Nginx設定をコピー
COPY infra/nginx.conf /etc/nginx/conf.d/default.conf

# 静的ファイルをコピー
COPY src/index.html /usr/share/nginx/html/

# Cloud Run のデフォルトポート 8080 を公開
EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
