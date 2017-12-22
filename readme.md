# An example repo with docker and a makefile.

See more details here [here](https://harrytorry.co.uk/posts/using-makefiles-with-docker-and-laravel)

### docker containers

* nginx
* mysql
* redis
* fpm
* websocket container
* artisan container
* composer container
* default laravel queue runner

### make commands

```
up:
    docker-compose up -d && sleep 5
    docker-compose run --rm composer install
    docker-compose run --rm artisan migrate:refresh --seed -v
    docker-compose run --rm artisan cache:clear
    docker-compose run --rm artisan view:clear
    docker-compose run --rm artisan config:clear
    $(MAKE) jwt

down:
    docker-compose stop

clean:
    $(MAKE) down
    docker-compose rm -fv

pull:
    docker-compose pull

cache:
    docker-compose run --rm artisan cache:clear

jwt:
    docker-compose run --rm artisan my-application:generate-jwt 1

unit:
    docker-compose run --rm --entrypoint=vendor/bin/phpunit artisan --testsuite=unit

integration:
    docker-compose run --rm --entrypoint=vendor/bin/phpunit artisan --testsuite=integration

test:
    docker-compose run --rm --entrypoint=vendor/bin/phpunit artisan

logs:
    docker-compose logs -f

refresh:
    docker-compose run artisan migrate:refresh --force --seed -v

staging:
    cd ./Application && composer install && php artisan migrate:fresh --seed

rebuild:
    $(MAKE) clean
    docker rmi -f laravel-docker-makefile artisan laravel-docker-makefile composer laravel-docker-makefile fpm laravel-docker-makefile nginx laravel-docker-makefile websockets laravel-docker-makefile queue.default 
    $(MAKE) up
```