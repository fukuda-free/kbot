# Kbot

# プロジェクト構築
docker-compose run app rails new . --force --no-deps --database=mysql --skip-test --webpacker

docker compose run app rails new . --force --no-deps --database=mysql --skip-test --webpacker

docker compose run app rails new . --force --no-deps --database=mysql --skip-test 

 ocker compose run app rails new . --force --no-deps --database=mysql --skip-test -j esbuild --css bootstrap


# config/database.ymlを設定してから次を実行
```
default: &default
  adapter: mysql2
  encoding: utf8
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: password # docker-compose.ymlのMYSQL_ROOT_PASSWORD
  host: db # docker-compose.ymlのservice名
```

docker-compose build --no-cache
docker-compose run app rake db:drop
docker-compose run app rake db:create db:migrate
docker-compose build
docker-compose up
docker-compose up --build --scale chrome=3
docker-compose up --build --scale chrome=5

rake db:drop
rake db:create db:migrate db:seed
rake db:seed

rake db:drop db:create db:migrate db:seed

# コンテナデータ削除
docker container prune -f
docker volume prune -f
docker image prune -a -f
docker network prune -f
docker system prune --volumes -f



# ジョブを手動実行
```
rails c
DnetSendUserScrapeJob.perform_later
DnetScheduleScrapeJob.perform_later

```

# app内で実行するコマンド(メモ)
```
rake db:create db:migrate
bundle exec rails webpacker:install
```

# メモ
## モード別起動
docker-compose --profile dev up
docker-compose --profile rele up
docker-compose --profile debug up


## (ES)これをやりたかったけど、うまくいかない
https://github.com/EricLondon/Docker-Rails-Elasticsearch-Logstash-Kibana

## デザインパターン検討（参考資料）
- https://product-development.io/posts/rails-design-patterns#rails%E3%81%AE%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3%E3%83%91%E3%82%BF%E3%83%BC%E3%83%B3%E4%B8%80%E8%A6%A7
- https://qiita.com/verdy89/items/00a2992a9a62cacec00e
- https://techracho.bpsinc.jp/hachi8833/2017_10_25/47160


https://www.jamesridgway.co.uk/implementing-a-two-step-otp-u2f-login-workflow-with-rails-and-devise/




# その為メモ
sudo yum update -y
sudo amazon-linux-extras install docker
sudo service docker start
sudo usermod -a -G docker ec2-user
docker info


sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version


# git
git config --global user.name "Your Name"
git config --global credential.helper cache


rails generate model schedule_content title:string content:text
rails generate model schedule_and_content dnet_schedule:references schedule_content:references


rails generate scaffold answer title:string content:text



rails generate scaffold tag name:string
rails generate model tag_map tag:references answer:references

https://pgmg-rails.com/blogs/27

# gitlab
```
version: '3.7'
services:
  gitLab:
    image: gitlab/gitlab-ce:latest
    ports:
     - "80:80"
    volumes:
     - '/srv/gitlab/config:/etc/gitlab'
     - '/srv/gitlab/logs:/var/log/gitlab'
     - '/srv/gitlab/data:/var/opt/gitlab'



version: "3"
services:
  runner:
    # image: gitlab/gitlab-runner:alpine-v9.4.2
    image: gitlab/gitlab-runner:alpine-bleeding
    tty: true
    container_name: gitlab-runner
    restart: always
    environment:
      - REGISTER_NON_INTERACTIVE=true
      - CI_SERVER_URL=http://192.168.16.106/
      - REGISTRATION_TOKEN=anzsRyDhzHPKecN12PXx
      - RUNNER_EXECUTOR=docker
      - RUNNER_TAG_LIST=docker
      - RUNNER_NAME=Runner
      - RUNNER_LIMIT=1
      - DOCKER_IMAGE=docker:latest
      - DOCKER_VOLUMES=/var/run/docker.sock:/var/run/docker.sock
```