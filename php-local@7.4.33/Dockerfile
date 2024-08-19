FROM --platform=$TARGETPLATFORM zjslqshqz/php:7.4.33-fpm

RUN apt update -y && \
    apt-get install -y memcached && \
    apt-get install -y redis && \
    apt-get install -y ffmpeg

# 向 docker-php-entrypoint 文件中插入启动 Memcached redis 的命令
RUN sed -i 's|exec "\$@"|memcached -m 64 -p 11211 -u memcache -l 127.0.0.1 \&\nexec "\$@"|' /usr/local/bin/docker-php-entrypoint && \
    sed -i 's|exec "\$@"|service redis-server start \&\nexec "\$@"|' /usr/local/bin/docker-php-entrypoint
