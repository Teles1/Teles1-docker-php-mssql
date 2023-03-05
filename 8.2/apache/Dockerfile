FROM php:8.2-apache
ENV ACCEPT_EULA=Y
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

# Install prerequisites required for tools and extensions installed later on.
RUN apt-get update \
    && apt-get install -y apt-transport-https gnupg2 libpng-dev libzip-dev nano unzip xz-utils autoconf dpkg-dev file g++ gcc libc-dev make pkg-config re2c libltdl-dev\
    && rm -rf /var/lib/apt/lists/*

# Install prerequisites for the sqlsrv and pdo_sqlsrv PHP extensions.
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/debian/11/prod.list > /etc/apt/sources.list.d/mssql-release.list \
    && apt-get update \
    && apt-get install -y msodbcsql18 mssql-tools18 libgssapi-krb5-2
RUN apt-get install -y unixodbc-dev unixodbc odbcinst1debian2 odbcinst
#Installing sqlsrv and pdo_sqlsrv
ENV PATH="${PATH}:/opt/mssql-tools18/bin"
RUN pecl install sqlsrv-5.11.0beta1
RUN pecl install pdo_sqlsrv-5.11.0beta1

# Retrieve the script used to install PHP extensions from the source container.
RUN curl --output /usr/bin/install-php-extensions \
        https://raw.githubusercontent.com/Teles1/docker-php-extension-installer/master/install-php-extensions \
    && chmod uga+x /usr/bin/install-php-extensions \
    && sync \
    && install-php-extensions bcmath ds exif gd intl opcache pcntl pcov redis zip

# Downloading composer and marking it as executable.
RUN curl -o /usr/local/bin/composer https://getcomposer.org/composer-stable.phar \
    && chmod +x /usr/local/bin/composer

RUN docker-php-ext-enable sqlsrv pdo_sqlsrv
