## Dockerized Rails 5 Development Environment

#### Usage

1. Clone this repository
2. Initialize Rails in the app image `./run bundle install`
3. Generate new Rails app `./run bundle exec rails new . -d postgresql`
4. It is okay to overwrite the `Gemfile` when asked.
5. Bundle dependencies `./run bundle`
6. Configure link to database in `config/database.yml`.

  ```yml
  default: &default
    adapter: postgresql
    encoding: unicode
    # For details on connection pooling, see rails configuration guide
    # http://guides.rubyonrails.org/configuring.html#database-pooling
    pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
    host: db
    port: <%= ENV['DB_PORT_5432_TCP_PORT'] %>
    username: postgres
  ```

7. Setup the Database `./rails bin/rake db:setup` and `./rails bin/rake db:migrate`
8. Start everything `docker-compose up`
9. You can use the convenience script to execute commands `./run <command> <arguments>`, the script will prefix `<command>` and `<arguments>` with `docker-compose run --rm app `.
10. Navigate to http:/localhost:3001 and you should see the 'Yay! You're on Rails!' welcome page'


#### Notes

If you get any errors such as `Cannot render console from 172.25.0.1! Allowed networks: 127.0.0.0/127.255.255.255, ::1` you can edit `config/environments/development.rb` and add a line `config.web_console.whitelisted_ips = '172.25.0.0/24'` at the end.

#### Credits
Adopted from Blog Post of Jesse B Hannah (https://jbhannah.net/articles/rails-development-with-docker/)
