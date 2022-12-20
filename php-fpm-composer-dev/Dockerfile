FROM --platform=$TARGETPLATFORM php:7.4.33-fpm-composer

RUN install-php-extensions xdebug

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"