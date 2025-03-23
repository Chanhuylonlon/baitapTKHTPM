FROM ubuntu:20.04

# Cập nhật và cài đặt Apache2, PHP 7.2, MySQL client và các module PHP
RUN apt-get update && apt-get install -y \
    apache2 \
    php7.2 \
    libapache2-mod-php \
    php7.2-mysql \
    php7.2-cli \
    php7.2-gd \
    php7.2-xml \
    php7.2-mbstring \
    php7.2-curl \
    php7.2-zip \
    && apt-get clean

# Copy mã nguồn website vào thư mục của Apache
COPY . /var/www/html/

# Cấp quyền
RUN chown -R www-data:www-data /var/www/html

# Kích hoạt Apache mod_rewrite
RUN a2enmod rewrite

# Khởi động Apache
CMD ["apachectl", "-D", "FOREGROUND"]
