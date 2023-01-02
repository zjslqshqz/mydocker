FROM --platform=$TARGETPLATFORM zjslqshqz/php:7.4.33-fpm-composer

EXPOSE 9000 9003

# 复制开发模式配置文件
RUN cp "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

# 修改 php.ini 文件
RUN sed -i '{s/upload_max_filesize = 2M/upload_max_filesize = 1024M/g;s/max_file_uploads = 20/max_file_uploads = 2048/g;s/max_execution_time = 30/max_execution_time = 0/g;s/max_input_time = 60/max_input_time = -1/g;s/post_max_size = 8M/post_max_size = 1024M/g;s/memory_limit = 128M/memory_limit = -1/g;s/;date.timezone =/date.timezone = PRC/g;}' "$PHP_INI_DIR/php.ini"

# 安装xdebug
RUN curl -sSLf \
        -o /usr/local/bin/install-php-extensions \
        https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions && \
    chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions xdebug

# 修改xdebug
RUN sed -i '$a [XDebug]\n\
xdebug.mode = debug\n\
xdebug.start_with_request = yes\n\
xdebug.client_host = host.docker.internal' "$PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini"