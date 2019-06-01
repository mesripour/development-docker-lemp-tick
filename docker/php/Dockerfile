FROM php:7.2.12-fpm

RUN apt-get update \
    && apt-get install git zip unzip vim libjpeg62-turbo-dev libfreetype6-dev libpng-dev zsh htop iputils-ping wget sudo -y

# install oh-my-zsh
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true
RUN echo "alias llq=\"ls -lah\"" >> ~/.zshrc

RUN docker-php-ext-install pdo_mysql bcmath sockets
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd

# install composer
RUN curl https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

RUN pecl install mongodb

RUN pecl install xdebug && docker-php-ext-enable xdebug

# add user mockuser
USER root
RUN useradd -m mockuser && echo mockuser:mockuser | chpasswd
RUN usermod -aG sudo mockuser
USER mockuser
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true
RUN echo "alias llq=\"ls -lah\"" >> ~/.zshrc
USER root
RUN chsh -s /bin/zsh mockuser

WORKDIR /src
