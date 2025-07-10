FROM --platform=$TARGETPLATFORM zjslqshqz/node:16.20.2-dev

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN apk update
RUN apk add --no-cache curl git