FROM php:5.6-fpm

ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ  /etc/localtime && echo $TZ > /etc/timezone
	
# Libs
RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list
  
RUN apt-get clean

RUN apt-get update \
    && apt-get install -y \
    curl \
    wget \
    git \
    zip \
    libz-dev \
    libssl-dev \
    libnghttp2-dev \
    libpcre3-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    && apt-get clean \
    && apt-get autoremove

RUN wget http://nchc.dl.sourceforge.net/project/mcrypt/Libmcrypt/2.5.8/libmcrypt-2.5.8.tar.gz \
    && tar -zxvf libmcrypt-2.5.8.tar.gz && cd libmcrypt-2.5.8 && ./configure && make && make install

RUN docker-php-ext-configure mcrypt && docker-php-ext-install mcrypt

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
   && docker-php-ext-install -j$(nproc) gd \
   && docker-php-ext-install zip \
   && docker-php-ext-install pdo_mysql \
   && docker-php-ext-install opcache

RUN pecl install http://pecl.php.net/get/swoole-1.9.23.tgz && docker-php-ext-enable swoole \
    && pecl install hprose && docker-php-ext-enable hprose

RUN wget https://dl.laravel-china.org/composer.phar -O /usr/local/bin/composer \
     && chmod a+x /usr/local/bin/composer \
     && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

RUN echo "opcache.enable=1" >>/usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.memory_consumption=1024" >>/usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.interned_strings_buffer=8" >>/usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.max_accelerated_files=4000" >>/usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.revalidate_freq=1" >>/usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && echo "opcache.fast_shutdown=1" >>/usr/local/etc/php/conf.d/docker-php-ext-opcache.ini

#RUN cp /var/www/html/id_rsa ~/.ssh/ \
#    && cp /var/www/html/id_rsa.pub ~/.ssh/ \
#    && chmod 700 ~/.ssh//id_rsa