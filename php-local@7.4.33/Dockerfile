FROM --platform=$TARGETPLATFORM php:7.4.33-fpm

RUN apt update -y && \
    apt-get install -y memcached && \
    apt-get install -y git && \
    apt-get install -y redis && \
    apt-get install -y htop && \
    apt-get install -y ffmpeg

# 向 docker-php-entrypoint 文件中插入启动 Memcached redis 的命令
RUN sed -i 's|exec "\$@"|memcached -m 64 -p 11211 -u memcache -l 127.0.0.1 \&\nexec "\$@"|' /usr/local/bin/docker-php-entrypoint && \
    sed -i 's|exec "\$@"|service redis-server start \&\nexec "\$@"|' /usr/local/bin/docker-php-entrypoint

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
    mcrypt msgpack memcached\
    zip
