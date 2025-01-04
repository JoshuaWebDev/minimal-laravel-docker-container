FROM php:7.1-apache

# Define o nome do projeto, altere este valor se necessário
# Caso contrário o nome do projeto será laravel, por padrão.
ENV PROJECTNAME laravel

# Define o usuário que terá permissões para acessar o diretório do projeto.
# Altere este valor se necessário, caso contrário o nome do projeto será laravel por padrão.
ENV USER laravel
ENV UID 1000

# Define o diretório de trabalho
ARG WORK_DIRECTORY
ENV WORK_DIRECTORY /var/www/html/${PROJECTNAME}

# Atualiza as bibliotecas do sistema e instala as dependências do PHP
RUN apt-get update && apt-get install -y vim curl \
    libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    && docker-php-source extract \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-source delete

# Cria o usuário do sistema que irá executar os comandos do Composer e do Artisan
RUN useradd -G www-data,root -u ${UID} -d /home/${USER} ${USER}
RUN mkdir -p /home/${USER}/.composer && chown -R ${USER}:${USER} /home/${USER}

COPY .. $WORK_DIRECTORY
WORKDIR $WORK_DIRECTORY

COPY ./apache/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY ./php/php.ini ${PHP_INI_DIR}

# Instala o Composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

RUN a2enmod rewrite

USER ${USER}