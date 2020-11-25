# Laravel Vue.js Chat (with Pusher)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Real time Chat web application.

### Installation

Install Laravel packages.

```sh
$ cd laravel-vuejs-chat
$ composer install
```

Copy .env file from .env.example and set the DB configuration and Pusher configuration.
You should create the DB and create the app in the https://pusher.com .
You can get the pusher credentails in the pusher dashboard.
```sh
cp .env.example .env
```
```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=
DB_USERNAME=
DB_PASSWORD=
...
...
PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_APP_CLUSTER=
```
Migrate the DB tables.
```
php artisan:migrate
```
Install the Vuejs dependencies.

```sh
$ npm install
```

### Development

You can run npm with watch mode to compile the every changes when editing code.

First Tab:
```sh
$ npm run watch
```

Run laravel server.
Second Tab:
```sh
$ php artisan serve
```

Now you can visit the website http://localhost:8000


License
----

MIT

