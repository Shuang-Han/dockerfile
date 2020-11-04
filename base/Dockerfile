# 此镜像将时区调整为东八区，语言设置为中文

FROM alpine:3.12

RUN mv /etc/apk/repositories /etc/apk/repositories.bak \
    && echo "http://mirrors.aliyun.com/alpine/v3.9/main" >> /etc/apk/repositories \
    && echo "http://mirrors.aliyun.com/alpine/v3.9/community" >> /etc/apk/repositories \
    && apk update \
    && apk add --no-cache tzdata ttf-dejavu \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && apk del tzdata \
    && mkdir /app

COPY glibc-bin-2.25-r0.apk /app/glibc-bin-2.25-r0.apk
COPY glibc-i18n-2.25-r0.apk /app/glibc-i18n-2.25-r0.apk
COPY glibc-2.25-r0.apk /app/glibc-2.25-r0.apk
COPY locale.md /app/locale.md

RUN apk --no-cache add ca-certificates wget \
    && wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
    && apk add /app/glibc-bin-2.25-r0.apk /app/glibc-i18n-2.25-r0.apk /app/glibc-2.25-r0.apk \
    && rm -rfv /app/glibc-bin-2.25-r0.apk /app/glibc-i18n-2.25-r0.apk /app/glibc-2.25-r0.apk \
    && cat /app/locale.md | xargs -i /usr/glibc-compat/bin/localedef -i {} -f UTF-8 {}.UTF-8 \
    && rm -rfv /app/locale.md \
    && rm -rf /app \
    && rm -rf /var/cache/apk/* \
    && rm -rf /root/.cache \
    && rm -rf /tmp/*

ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US.UTF-8

CMD ["/bin/sh"]