ARG RUBY_VERSION
# FROM ruby:$RUBY_VERSION
FROM public.ecr.aws/docker/library/ruby:$RUBY_VERSION

# RUN gem install foreman

# NodeJS install
ARG NODE_VERSION
RUN curl -sL https://deb.nodesource.com/setup_$NODE_VERSION.x | bash -

# yarn install
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# apt-get install
RUN apt-get update -qq \
    && apt-get install -y build-essential nodejs yarn vim wget











# ディレクトリ作成
ARG PROJECT_NAME
ENV APP_DIR /$PROJECT_NAME
RUN mkdir $APP_DIR
WORKDIR $APP_DIR

# gemfileを複製
# COPY ./web/Gemfile      $APP_DIR/Gemfile
# COPY ./web/Gemfile.lock $APP_DIR/Gemfile.lock
ARG DOCCOM_DIR
COPY ./$DOCCOM_DIR/Gemfile      $APP_DIR/Gemfile
COPY ./$DOCCOM_DIR/Gemfile.lock $APP_DIR/Gemfile.lock


# gemfileのinstall
RUN gem install bundler
# RUN bundle install
RUN bundle install -j4
COPY $DOC_DIR $APP_DIR