FROM php:8.0-fpm


COPY php.ini /usr/local/etc/php/

# 更新系统
RUN apt-get update



# 修改源
RUN apt-get install sed
RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN apt-get update -y

# 安装 composer
RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer

# 安装 git zip 等工具
RUN apt-get update \
    && apt-get install -y zlib1g-dev  git libzip-dev mariadb-client \
    && docker-php-ext-install zip pdo_mysql 

# 升级系统 和 安装node
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash - \ 
    && apt-get update \
    && apt-get install -y  nodejs

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
COPY --from=composer /usr/bin/composer /usr/bin/composer