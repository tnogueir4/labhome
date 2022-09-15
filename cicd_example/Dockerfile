FROM php:7.4-fpm

#Setando diretorio da app
WORKDIR /var/www

#Instalando updates e dependencias
RUN apt-get update && apt-get install -y \
    build-essential \
    locales \
    zip \
    vim \
    unzip \
    git \
    curl \
    libzip-dev

#Limpa o cache do apt
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

#Instalando extensoes PHP
RUN /usr/local/bin/docker-php-ext-install mysqli

#Adiciona usuario e grupo para app
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

#Copia conteúdo da app
COPY . /var/www/

#Ajustando permissoes para user www
COPY --chown=www:www . /var/www

#Forca o uso do user www
USER www

#Expoe porta default e inicia o server php-fpm
EXPOSE 9000
CMD ["php-fpm"]