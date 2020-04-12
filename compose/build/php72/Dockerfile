FROM php:7.2.2-fpm

# ARGS
ARG CHANGE_SOURCE=false

# Change Timezone
ARG TIME_ZONE=UTC
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone

RUN groupadd -r www && useradd -r -g www www

# Change China Sources
COPY sources.list /etc/apt/sources.list
RUN apt-get -y update

RUN apt-get install -y net-tools wget

# Install Base Components
RUN apt-get install -y --no-install-recommends libpng-dev libjpeg-dev libfreetype6-dev ntpdate cron vim unzip git \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && :\
    && apt-get install -y libicu-dev \
    && docker-php-ext-install intl \
    && :\
    && apt-get install -y libxml2-dev \
    && apt-get install -y libxslt-dev \
    && docker-php-ext-install soap \
    && docker-php-ext-install xsl \
    && docker-php-ext-install xmlrpc \
    && docker-php-ext-install wddx \
    && :\
    && apt-get install -y libbz2-dev \
    && docker-php-ext-install bz2 \
    && :\
    && apt-get install -y curl \
    && apt-get install -y libcurl3 \
    && apt-get install -y libcurl4-openssl-dev \
    && docker-php-ext-install curl \
    && docker-php-ext-install zip \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install exif \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install calendar \
    && docker-php-ext-install sockets \
    && docker-php-ext-install gettext \
    && docker-php-ext-install shmop \
    && docker-php-ext-install sysvmsg \
    && docker-php-ext-install sysvsem \
    && docker-php-ext-install sysvshm \
    && docker-php-ext-install opcache

# Redis
# COPY redis-3.1.6.tgz /home/redis.tgz
 RUN pecl install http://pecl.php.net/get/redis-5.0.0.tgz \
  	&& echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini
 
 RUN pecl install xdebug && docker-php-ext-enable xdebug
 ADD composer.phar /usr/local/bin/composer
 RUN chmod 755 /usr/local/bin/composer
