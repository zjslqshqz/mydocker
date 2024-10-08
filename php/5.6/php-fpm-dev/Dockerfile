FROM --platform=$TARGETPLATFORM zjslqshqz/php:5.6.40-php-fpm

# 安装 composer
COPY --from=composer/composer:2.2.21 /usr/bin/composer /usr/bin/composer

# 开放端口
EXPOSE 9000 9003

# 复制开发模式配置文件并修改 php.ini 文件
RUN cp "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini" && \
    sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 1024M/g' "$PHP_INI_DIR/php.ini" && \
    sed -i 's/max_file_uploads = 20/max_file_uploads = 2048/g' "$PHP_INI_DIR/php.ini" && \
    sed -i 's/max_execution_time = 30/max_execution_time = 0/g' "$PHP_INI_DIR/php.ini" && \
    sed -i 's/max_input_time = 60/max_input_time = -1/g' "$PHP_INI_DIR/php.ini" && \
    sed -i 's/post_max_size = 8M/post_max_size = 1024M/g' "$PHP_INI_DIR/php.ini" && \
    sed -i 's/memory_limit = 128M/memory_limit = -1/g' "$PHP_INI_DIR/php.ini" && \
    sed -i 's/;date.timezone =/date.timezone = PRC/g' "$PHP_INI_DIR/php.ini"

# php opcache 缓存设置
RUN echo "[opcache]\n \
; 启用 opcache 扩展\n \
zend_extension=opcache\n \
opcache.enable=1\n \
; 禁用在命令行界面下运行 PHP 脚本时使用 opcache 扩展\n \
opcache.enable_cli=0\n \
; 指定用于缓存内部字符串的内存大小，单位为 MB\n \
opcache.interned_strings_buffer=16\n \
; 指定 Opcache 所使用的内存大小，单位为 MB\n \
opcache.memory_consumption=128\n \
; 指定优化级别，所有位都被设置为 1，表示启用所有优化选项\n \
; XDebug 开启会导致 optimization_level = 0 \n \
opcache.optimization_level=0x7FFEBFFF\n \
; 配置保护时间，以秒为单位，在此时间内不会检查文件的时间戳是否已更改\n \
opcache.file_update_protection=2" > "$PHP_INI_DIR/conf.d/docker-php-ext-01-opcache.ini"

# 安装xdebug 并修改参数
RUN install-php-extensions xdebug && \
sed -i '$a [XDebug]\n\
xdebug.mode = debug\n\
xdebug.start_with_request = yes\n\
xdebug.client_host = host.docker.internal' "$PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini"