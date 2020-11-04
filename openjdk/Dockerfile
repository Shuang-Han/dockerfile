FROM registry.cn-chengdu.aliyuncs.com/thisisgpy/base:alpine-3.12

RUN apk add --no-cache openjdk8 \
    && mkdir /app \
    && rm -rf /var/cache/apk/* \
    && rm -rf /root/.cache \
    && rm -rf /tmp/*

ENV JAVA_HOME=/usr/bin

WORKDIR /app

CMD ["/bin/sh"]