FROM php:8.2-fpm-alpine

RUN apk --update --no-cache add bash \
   && apk add wget \
   && apk add git \
   && apk add libpq-dev \
   && apk add icu-dev
#   && apk add php8 \
#   && apk add php8-phar \
#   && apk add php8-openssl \
#   && apk add php8-xml \
#   && apk add php8-pdo \
#   && apk add php8-pdo_mysql \
#   && apk add php8-mbstring \
#   && apk add php8-iconv \
#   && apk add php8-ctype \
#   && apk add php8-posix \
#   && apk add php8-intl \
#   && apk add php8-opcache  \
#   && apk add $PHPIZE_DEPS \
#   && apk add icu-dev \
#   && pecl install xdebug \
#   && apk add alpine-conf \
#   && pecl install uopz

RUN docker-php-ext-install pdo \
    pdo_pgsql \
    intl \
    opcache

RUN apk add --update linux-headers

# Install Xdebug
RUN apk add --no-cache $PHPIZE_DEPS \
 && pecl install xdebug \
 && docker-php-ext-enable xdebug

COPY php-overrides.ini /usr/local/etc/php/conf.d/
COPY timezone.ini /usr/local/etc/php/conf.d/
COPY xdebug.ini /usr/local/etc/php/conf.d/

RUN apk add alpine-conf
RUN setup-timezone -z Europe/Rome

RUN mkdir -p /var/app
RUN adduser --disabled-password app && chown -R app:app /var/app

# Composer
COPY --from=composer /usr/bin/composer /usr/bin/composer

# Symfony installer
RUN wget https://get.symfony.com/cli/installer -O - | bash
RUN mv /root/.symfony5/bin/symfony /usr/local/bin/symfony

USER app
WORKDIR /var/app

EXPOSE 9000

RUN echo "alias ll='ls -l'" >> ~/.bashrc
RUN echo "alias la='ls -la'" >> ~/.bashrc
