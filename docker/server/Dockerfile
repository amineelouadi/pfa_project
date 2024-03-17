FROM lavoweb/php-8.2

RUN a2enmod rewrite
RUN apt-get update && apt-get install -y git unzip zip
WORKDIR /var/www/html
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions gd pdo_mysql bcmath zip intl opcache
COPY --from=composer:2.0 /usr/bin/composer /usr/local/bin/composer
RUN composer self-update
RUN apt update 
RUN apt install nano

# install the PHP APCu extension
RUN mkdir -p /usr/src/php/ext/apcu && curl -fsSL https://pecl.php.net/get/apcu | tar xvz -C "/usr/src/php/ext/apcu" --strip 1 && docker-php-ext-install apcu

# Install xsl extension
RUN apt install -y libxslt-dev
RUN docker-php-ext-install xsl

# Cron
#RUN apt-get update && apt-get install -y cron

# Install Xdebug
#RUN pecl install xdebug-3.3.1 && docker-php-ext-enable xdebug

# Install Symfony cli
RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | bash
RUN apt install symfony-cli

# Install MongoDb
#RUN pecl install mongodb
#RUN echo "extension=mongodb.so" >> /usr/local/etc/php/conf.d/mongodb.ini

## PHP AMQP
#RUN apt-get install -y librabbitmq-dev libssl-dev
#RUN pecl install amqp
#RUN docker-php-ext-enable amqp

# Install Nodejs
RUN apt install -y nodejs npm

EXPOSE 8585
