# 定义PHP基础来源
FROM php:7.2-fpm

### set timezome
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 安装PHP Core Extensions
RUN apt-get update \
	&& apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
		libmcrypt-dev \
        unzip \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# 安装MySQL扩展
RUN docker-php-ext-install pdo_mysql mysqli

# 安装zip unzip bcmath扩展
RUN docker-php-ext-install zip bcmath

# 安装mcrypt扩展
RUN pecl install mcrypt-1.0.2 \
    && docker-php-ext-enable mcrypt

# 安装composer, 更新为国内镜像
RUN cd ~ \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer \
    && composer config -g repo.packagist composer https://packagist.phpcomposer.com

# 安装PHPRedis扩展
RUN cd ~ \
    && curl -L -o 4.2.0.tar.gz https://github.com/phpredis/phpredis/archive/4.2.0.tar.gz \
    && tar -zxvf 4.2.0.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv phpredis-4.2.0 /usr/src/php/ext/redis \
    && docker-php-ext-install redis

# 安装swoole扩展
RUN cd ~ \
    && curl -L -o v4.2.12.tar.gz https://github.com/swoole/swoole-src/archive/v4.2.12.tar.gz \
    && tar -zxvf v4.2.12.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv swoole-src-4.2.12 /usr/src/php/ext/swoole \
    && docker-php-ext-install swoole

# 安装seaslog扩展
RUN pecl install https://pecl.php.net/get/SeasLog-2.0.2.tgz \
    && docker-php-ext-enable seaslog