# FROM php:8.3-rc-zts-alpine3.20 as install_dev
FROM alpine:3.20 AS install_env


RUN apk update && \ 
    apk add --no-cache \
    bash \
    php83 php83-dom php83-fileinfo php83-mbstring php83-openssl php83-pdo php83-pear php83-pdo_sqlite \ 
    php83-pdo_pgsql php83-phar php83-session \ 
    php83-tokenizer php83-xml php83-xmlwriter php83-zip php83-fpm php83-redis \
    ca-certificates \
    gcc musl-dev make \
    curl \
    openssl \
    tar \
    xz

# INSTALL COMPOSER
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/ \
    && ln -s /usr/local/bin/composer.phar /usr/local/bin/composer
SHELL [ "/bin/bash", "-c" ]


FROM install_env AS dev 

WORKDIR /projects

#xdebug
RUN apk add --no-cache php83-dev linux-headers \
    libmemcached-dev \
    php83-pecl-memcached \
    && pecl install xdebug-3.3.0 \
    # && pecl install memcached \
    && echo "[XDebug]" >> /etc/php83/php.ini \
    && echo "zend_extension=/usr/lib/php83/modules/xdebug.so" >> /etc/php83/php.ini \
    && echo "xdebug.mode=debug" >> /etc/php83/php.ini \
    && echo "xdebug.start_with_request=yes" >> /etc/php83/php.ini 
# && echo "extension=usr/lib/php83/modules/memcached.so" >> /etc/php83/php.ini

ARG git_email
ARG git_name

RUN apk update && \
    apk add --no-cache \
    git \
    gdb \
    vim \
    openssh \
    zsh \
    curl \
    nodejs \
    npm \
    && git config --global user.email "${git_email}" \
    && git config --global user.name "${git_name}"

ENTRYPOINT [ "tail", "-f", "/dev/null" ]
