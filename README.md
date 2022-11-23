## 開発環境のセットアップ

```	
$ git clone git@github.com:narutyo/auth-docker.git
$ cd auth-docker
$ git submodule update --init --recursive
$ git submodule foreach git checkout master
$ docker-compose up -d --build

# コンテナが立ち上がってから...
$ docker-compose exec auth-sample composer self-update
$ docker-compose exec auth-sample composer config -g repos.packagist composer https://packagist.jp
$ docker-compose exec auth-sample composer install
$ sudo find submodules/auth-sample/storage -type d -exec chmod 777 {} +
$ sudo find submodules/auth-sample/storage -type f -exec chmod 666 {} +
$ docker-compose exec auth-sample php artisan migrate --seed

$ docker-compose exec auth-api-sample composer self-update
$ docker-compose exec auth-api-sample composer config -g repos.packagist composer https://packagist.jp
$ docker-compose exec auth-api-sample composer install
$ sudo find submodules/auth-api-sample/storage -type d -exec chmod 777 {} +
$ sudo find submodules/auth-api-sample/storage -type f -exec chmod 666 {} +
$ docker-compose exec auth-api-sample php artisan migrate --seed

# ２回目以降は --build 無しでOKです
$ cd docker
$ docker-compose up -d
```
