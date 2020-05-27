# rails-docker
Ruby on Rails on Docker

# docker build後
`https://qiita.com/fussy113/items/e9f7457ad4de74023ef6` 様参考

-d sqlite -> 使用DBをsqlite3を選択
-B -> プロジェクト作成後のbundle installをしない(修正するからスキップで)
--skip-webpack-install -> プロジェクト作成後のwebpacker:installをしない
--skip-spring -> プロジェクト作成後のspringのinstallをしない

```
$ docker-compose run --rm app rails new ./ -d sqlite3 -B --skip-webpack-install --skip-spring
```

- webpack記述削除
`Gemfile`
```
# 下記二行を削除
# Transpile app-like JavaScript. Read more: https://github.com/rails/webpacker
gem 'webpacker', '~> 4.0'
```

`touch public/sw.js`

```
docker-compose build

docker-compose run --rm app rails db:create

docker-compose run --rm app rails db:migrate
```


##########################################
# rails new
```
$ docker-compose run web rails new . --force --database=mysql --skip-bundle
```

# database.yml
```yml
default: &default
  adapter: mysql2
  encoding: utf8
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: password # docker-compose.ymlのMYSQL_ROOT_PASSWORD
  host: db # docker-compose.ymlのservice名
```

# db create
```
$ docker-compose run web rails db:create
```