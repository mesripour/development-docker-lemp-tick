FROM php:7.2.12-cli

RUN apt-get update \
    && apt-get install git zip unzip supervisor vim zsh htop iputils-ping wget sudo cron -y

# install oh-my-zsh
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true
RUN echo "alias llq=\"ls -lah\"" >> ~/.zshrc

RUN docker-php-ext-install pdo_mysql bcmath sockets

# install composer
RUN curl https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

RUN pecl install mongodb

WORKDIR /src
