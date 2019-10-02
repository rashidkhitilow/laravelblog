[TOC]

# [guillaumebriday/laravel-blog](https://github.com/guillaumebriday/laravel-blog) 本地运行

## env

- win10 home 
- wampserver - php 7.2

## install

### .env

```ini
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=laravel-blog
DB_USERNAME=root
DB_PASSWORD=password
```

> php_network_getaddresses 问题

### app/Providers/AppServiceProvider.php

```php
use Illuminate\Support\Facades\Schema;

public function boot(): void
{
    Schema::defaultStringLength(191);
}
```

> 

### webpack.mix.js

```js
mix.js('resources/js/app.js', 'public/js')
   .sass('resources/sass/app.scss', 'public/css')
   .version()

mix.js('resources/js/admin.js', 'public/js')
   .sass('resources/sass/admin.scss', 'public/css')
   .version()
```

> 添加了js css 的版本号而已 不加也行 `.version()`;

### bash

```bash
$ git clone https://github.com/guillaumebriday/laravel-blog.git
$ cd laravel-blog
$ cp .env.example .env

# 直接安装出现问题 添加 --ignore-platform-reqs
$ composer install --ignore-platform-reqs

$ php artisan key:generate
$ php artisan vendor:publish --provider="Laravel\Horizon\HorizonServiceProvider"
$ php artisan storage:link

$ php artisan migrate --seed

$ npm install -g yarn

# yarn dev 出现问题
$ rm -rf node_modules
$ rm package-lock.json yarn.lock
$ npm cache clear --force
$ npm install

$ yarn dev

$ php artisan serve 
# OK 可以访问 http://localhost:8000 了
```

### Reference

- [How can I solve "laravel/horizon v1.1.0 requires ext-pcntl * -> the requested PHP extension pcntl is missing from your system"? - Stack Overflow](https://stackoverflow.com/questions/48577465/how-can-i-solve-laravel-horizon-v1-1-0-requires-ext-pcntl-the-requested-ph)

- [php_network_getaddresses: getaddrinfo failed: nodename nor servname provided, or not known - Stack Overflow](https://stackoverflow.com/questions/33260172/sqlstatehy000-2002-php-network-getaddresses-getaddrinfo-failed-nodename-no)

- [php - Laravel migration: unique key is too long, even if specified - Stack Overflow](https://stackoverflow.com/questions/23786359/laravel-migration-unique-key-is-too-long-even-if-specified)

- [Node、Yarn的安装 - 个人文章 - SegmentFault 思否](https://segmentfault.com/a/1190000011624238)

- [Laravel Mix npm run dev error · Issue #1072 · JeffreyWay/laravel-mix](https://github.com/JeffreyWay/laravel-mix/issues/1072)
