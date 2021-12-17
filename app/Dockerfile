# Node
ARG NODE_VERSION 
# FROM node:$NODE_VERSION as node
FROM node:17.2.0 as node

# ruby
ARG RUBY_VERSION
# FROM public.ecr.aws/docker/library/ruby:$RUBY_VERSION
FROM ruby:3.0.3


# 関係ファイル一式
COPY --from=node /usr/local/bin/node /usr/local/bin/node
COPY --from=node /opt/yarn-* /opt/yarn
RUN ln -fs /opt/yarn/bin/yarn /usr/local/bin/yarn && \
 apt-get update && \
 apt-get install -y libpq-dev && \
 apt-get clean && \
 rm -rf /var/lib/apt/lists/*


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
COPY $DOC_DIR $APP_DIR