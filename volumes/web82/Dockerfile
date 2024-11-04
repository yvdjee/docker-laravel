FROM php:8.2-apache

ADD add_php.ini /usr/local/etc/php/conf.d/

RUN apt-get update -y && apt-get install -y libzip-dev g++ libicu-dev libpq-dev zlib1g-dev libpng-dev
RUN docker-php-ext-configure zip
RUN docker-php-ext-install pdo pdo_mysql pdo opcache intl zip gd pcntl
RUN apt-get install -y autoconf pkg-config libssl-dev

RUN pecl install redis \
    && docker-php-ext-enable redis

# Install NVM and Node
ENV NODE_VERSION=16
ENV NVM_DIR=/usr/local/nvm
RUN mkdir -p $NVM_DIR \
    && curl https://raw.githubusercontent.com/creationix/nvm/v0.40.1/install.sh | bash \
    && . $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default \
    && npm install -g yarn

# Add node and npm to path
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

# install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Modify write permission for apache
RUN usermod -u 1000 www-data \
    && groupmod -g 1000 www-data

RUN a2enmod rewrite
