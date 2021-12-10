FROM nginx:1.19.10
# FROM nginx:latest
# インクルード用のディレクトリ内を削除
RUN rm -f /etc/nginx/conf.d/*

# Nginxの設定ファイルをコンテナにコピー
COPY ./nginx.conf /etc/nginx/