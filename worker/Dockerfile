FROM php:8.2-cli-alpine3.18

ARG APP_PATH

ARG CHANGE_SOURCE=false
RUN if [ ${CHANGE_SOURCE} = true ]; then \
    # Change application source from dl-cdn.alpinelinux.org to aliyun source
    sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories \
    ;fi

# add WORKDIR
WORKDIR ${APP_PATH}

# add composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN apk update && apk add supervisor \
    && rm -rf /var/cache/apk/* \
    && docker-php-ext-install pdo \
    pdo_mysql

COPY supervisord.conf /etc/supervisord.conf

WORKDIR ${APP_PATH}

ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisord.conf"]

