# heroku-rails-starter

# Install

```
$ git clone git@github.com:YuheiNakasaka/heroku-rails-starter.git
$ cd heroku-rails-starter
$ rm -fr ./.git
```

# Setup base app

```
$ docker-compose run web rails new . --force --no-deps --database=postgresql
```

```
$ docker-compose build
```

```
$ vim config/database.yml
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password:
  pool: 5

development:
  <<: *default
  database: myapp_development

test:
  <<: *default
  database: myapp_test

production:
  <<: *default
  database: myapp_production
  username: myapp
  password: <%= ENV['MYAPP_DATABASE_PASSWORD'] %>
```

```
$ docker-compose up -d
$ docker-compose run web rake db:create
$ docker-compose run web rails db:migrate
```

You can access to [localhost:3000](http://localhost:3000/).

# Deploy to Heroku

```
$ heroku container:login
$ heroku create <YOUR-APP-NAME>
$ heroku container:push web
$ heroku addons:create heroku-postgresql:hobby-dev
$ heroku container:release web
$ heroku open
```