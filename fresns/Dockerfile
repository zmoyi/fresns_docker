FROM php:8.2-fpm

ARG APP_PATH

ARG USER

# add WORKDIR
WORKDIR ${APP_PATH}
RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list
# add composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN apt-get update && apt-get install -y curl \
    unzip \
    libfreetype-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev \
    && pecl install redis-5.3.7 \
    && docker-php-ext-install pdo_mysql \
    exif \
    bcmath \
    gd \
    gettext \
    iconv \
    mysqli \
    opcache \
    sockets 

ADD https://app.fresns.cn/latest.zip ${APP_PATH}

RUN unzip latest.zip && rm latest.zip \
    && folder_name=$(ls | grep -E '^fresns-v[0-9]+\.[0-9]+\.[0-9]+$') \
    && mv "$folder_name"/* . && rmdir "$folder_name" \
    && chmod 755 -R /www/app/ \
    && chown -R ${USER}:${USER} /www/app/

# USER ${USER}