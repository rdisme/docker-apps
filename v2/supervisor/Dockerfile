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
    && docker-php-ext-install \
        -j$(nproc) \
        iconv \
        gd \
        pdo_mysql \
        mysqli \
        zip \
        bcmath \
        sockets \
    && docker-php-ext-configure \
        gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# 安装mcrypt扩展
RUN pecl install \
        mcrypt-1.0.2 \
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

# 安装seaslog扩展
RUN pecl install https://pecl.php.net/get/SeasLog-2.0.2.tgz \
    && docker-php-ext-enable seaslog

# install python pip supervisor
RUN cd ~ \
    && apt-get -y install python3.7 python3-distutils \
    && curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
    && python3.7 get-pip.py \
    && pip install supervisor==4.1.0 \
    && mkdir -p /etc/supervisor