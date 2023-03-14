FROM --platform=$TARGETPLATFORM php:7.4.33-fpm

# 开启拓展
RUN curl -sSLf \
        -o /usr/local/bin/install-php-extensions \
        https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions && \
    chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions calendar \
    bcmath bz2 \
    enchant event exif \
    gd gettext gmp \
    imap intl \
    oauth oci8 odbc \
    pcntl pdo_mysql pdo_oci pdo_odbc \
    redis \
    ssh2 shmop sockets soap sysvsem sysvmsg sysvshm \
    xmlrpc \
    mcrypt msgpack \
    zip