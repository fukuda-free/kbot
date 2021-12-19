# Node
ARG NODE_VERSION 
# FROM node:17.2.0 as node
# FROM node:$NODE_VERSION as node

# ruby
ARG RUBY_VERSION
FROM ruby:3.0.3
# FROM ruby:$RUBY_VERSION


# 関係ファイル一式
# COPY --from=node /usr/local/bin/node /usr/local/bin/node
# COPY --from=node /usr/local/bin/npm /usr/local/bin/npm
# COPY --from=node /opt/yarn-* /opt/yarn
# RUN ln -fs /opt/yarn/bin/yarn /usr/local/bin/yarn && \
#  apt-get update && \
#  apt-get install -y libpq-dev vim npm && \
#  apt-get clean && \
#  rm -rf /var/lib/apt/lists/*

# # nをインストールしてnode.jsのstableをインストールする
# RUN npm install -g n && n stable
# RUN npm install -g npm@4.0
# RUN npm install -g npm@latest

# 2p ---------------------
# 共通の依存関係
# パッケージツールをインストール
RUN apt-get update && apt-get install -y curl apt-transport-https wget

# NodeJSをsources listに追加
RUN curl -sL https://deb.nodesource.com/setup_$NODE_VERSION.x | bash -

# Yarnをsources listに追加
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo 'deb http://dl.yarnpkg.com/debian/ stable main' > /etc/apt/sources.list.d/yarn.list

RUN apt-get update -y && \
    apt-get install default-mysql-client nodejs npm -y && \
    npm uninstall yarn -g && \
    npm install yarn -g -y
    
# ディレクトリ作成
ARG PROJECT_NAME
ENV APP_DIR /$PROJECT_NAME
RUN mkdir $APP_DIR
WORKDIR $APP_DIR

# gemfileを複製
ARG DOCCOM_DIR
COPY ./$DOCCOM_DIR/Gemfile      $APP_DIR/Gemfile
COPY ./$DOCCOM_DIR/Gemfile.lock $APP_DIR/Gemfile.lock


# gemfileのinstall
RUN gem install bundler
# RUN bundle install
RUN bundle install -j4
COPY ./$DOCCOM_DIR $APP_DIR