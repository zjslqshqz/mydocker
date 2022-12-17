FROM --platform=$TARGETPLATFORM php:7.4.33-fpm-composer

RUN curl -sSLf \
        -o /usr/local/bin/install-php-extensions \
        https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions && \
    chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions xdebug

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"