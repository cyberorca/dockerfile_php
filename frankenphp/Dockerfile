FROM dunglas/frankenphp:php8.4-alpine

# Step 1: Install PHP extensions yang diperlukan
RUN apk add --no-cache --virtual .build-deps \
    autoconf gcc g++ make libtool pkgconfig \
    icu-dev libxml2-dev libzip-dev oniguruma-dev \
    freetype-dev libjpeg-turbo-dev libpng-dev \
    tidyhtml-dev \
    && install-php-extensions \
    pcntl \
    gd \
    pdo pdo_pgsql pdo_mysql mysqli \
    mbstring zip bcmath intl \
    exif soap tidy opcache \
    redis \
    sockets \
    && apk del .build-deps

# Step 2: Install curl + bash + infisical (bisa disesuaikan kebutuhan)
RUN apk add --no-cache bash curl && curl -1sLf \
    'https://dl.cloudsmith.io/public/infisical/infisical-cli/setup.alpine.sh' | bash \
    && apk add infisical

# Step 3: Copy composer dari official image (cache stable)
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
