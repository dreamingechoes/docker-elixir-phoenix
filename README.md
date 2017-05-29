# docker-elixir-phoenix

A list of `Docker` files to dockerize `Phoenix` applications (WIP).

## Setup development environment

To start working on your `Phoenix` project with `Docker`, first be sure to
have `Docker` installed, following the instructions provided [here](https://docs.docker.com/engine/installation/).

Then, copy into your project's folder the `Docker` files (`Dockerfile` and `docker-compose.yml`)
according to the `Phoenix`'s version you want to use, and change the `YOUR_APP_FOLDER_NAME`
value on the `Dockerfile` and `docker-compose.yml` file to the name of your project's folder.

This basic templates have two main volumes: one for the application itself, and one
for the database (`postgres`). So you will have to change your database config in
order to use this new volume to something like this:

```
# Configure your database for dev environment
config :you_app_name, YourAppName.Repo,
  adapter: Ecto.Adapters.Postgres,
  username: "postgres",
  password: "",
  database: "your_app_name_dev",
  hostname: "db",
  pool_size: 10
```

Once you have done this, you're ready to use your `Phoenix` application by executing
these commands on your terminal:

* Setup the web container with `docker-compose build web`
* Install dependencies with `docker-compose run web mix deps.get`
* Create your database with `docker-compose run web mix ecto.create`
* Migrate your database with `docker-compose run web mix ecto.migrate`
* Install Node.js dependencies with `docker-compose run web npm install`
* Start the application with `docker-compose up`

## Setup testing environment

This step assumes you already followed instructions from previous paragraph.

* Create your testing database with `docker-compose run web env MIX_ENV=test mix ecto.create`
* Migrate your testing database with `docker-compose run web env MIX_ENV=test mix ecto.migrate`
* Run the test suite with `docker-compose run web mix test`

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/dreamingechoes/docker-elixir-phoenix.
This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to
adhere to the [Contributor Covenant](http://contributor-covenant.org/) code of conduct.
