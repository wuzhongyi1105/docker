FROM php:alpine
LABEL maintainer="imlonghao"

ENV USER_NAME='' \
    USER_PASSWORD=''

WORKDIR /app

RUN docker-php-ext-install sockets

RUN apk add --no-cache git && \
    git clone https://github.com/lkeme/BiliHelper.git /app && \
    php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php composer.phar install && \
    rm -r /var/cache/apk && \
    rm -r /usr/share/man

ENTRYPOINT git pull && \
    php composer.phar install && \
    cp /app/conf/user.conf.example /app/conf/user.conf && \
    sed -i "s/APP_USER=/APP_USER=${USER_NAME}/g" /app/conf/user.conf && \
    sed -i "s/APP_PASS=/APP_PASS=${USER_PASSWORD}/g" /app/conf/user.conf && \
    php index.php