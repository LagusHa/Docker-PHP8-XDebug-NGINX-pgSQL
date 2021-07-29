# Docker-PHP8-XDebug-NGINX-pgSQL

1. Устанавливаем папку с докером в папку с вашим проектом.
2. Файлы `.gitignore, docker-compose.yml, docker-compose-production.yml, Makefile` переносим в корень проекта.
    1. В конфиге `conf.d/nginx` меняем сервер на свой.
3. В терминале пишем `make init`. Контейнеры должны запустится.
4. Далее переходим по ссылке https://handynotes.ru/2020/12/phpstorm-php-8-docker-xdebug-3.html и начиная с настройки сервера PHP.
