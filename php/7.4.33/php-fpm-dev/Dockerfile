FROM --platform=$TARGETPLATFORM zjslqshqz/php:7.4.33-php-fpm

# 安装 composer
COPY --from=composer /usr/bin/composer /usr/bin/composer

# 开放端口
EXPOSE 9000 9003

RUN apt update -y && \
    apt-get install -y curl ffmpeg memcached redis ffmpeg htop

# 向 docker-php-entrypoint 文件中插入启动 Memcached redis 的命令
RUN sed -i 's|exec "\$@"|memcached -m 64 -p 11211 -u memcache -l 127.0.0.1 \&\nexec "\$@"|' /usr/local/bin/docker-php-entrypoint && \
    sed -i 's|exec "\$@"|service redis-server start \&\nexec "\$@"|' /usr/local/bin/docker-php-entrypoint

# 复制开发模式配置文件并修改 php.ini 文件
RUN cp "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini" && \
    sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 1024M/g' "$PHP_INI_DIR/php.ini" && \
    sed -i 's/max_file_uploads = 20/max_file_uploads = 2048/g' "$PHP_INI_DIR/php.ini" && \
    sed -i 's/max_execution_time = 30/max_execution_time = 0/g' "$PHP_INI_DIR/php.ini" && \
    sed -i 's/max_input_time = 60/max_input_time = -1/g' "$PHP_INI_DIR/php.ini" && \
    sed -i 's/post_max_size = 8M/post_max_size = 1024M/g' "$PHP_INI_DIR/php.ini" && \
    sed -i 's/memory_limit = 128M/memory_limit = -1/g' "$PHP_INI_DIR/php.ini" && \
    sed -i 's/;date.timezone =/date.timezone = PRC/g' "$PHP_INI_DIR/php.ini"

# 安装xdebug 并修改参数
RUN install-php-extensions xdebug && \
sed -i '$a [XDebug]\n\
xdebug.mode = debug\n\
xdebug.start_with_request = yes\n\
xdebug.client_host = host.docker.internal' "$PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini"
