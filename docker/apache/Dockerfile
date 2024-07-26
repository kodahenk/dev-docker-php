FROM php:7.4-apache

# Gereken paketleri ve PHP uzantılarını kur
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql

# Apache modüllerini etkinleştir
RUN a2enmod rewrite ssl

# SSL sertifikalarını ve konfigürasyon dosyasını kopyala
COPY default-ssl.conf /etc/apache2/sites-available/default-ssl.conf
COPY symfony34.test.crt /etc/apache2/ssl/symfony34.test.crt
COPY symfony34.test.key /etc/apache2/ssl/symfony34.test.key

# SSL konfigürasyonunu etkinleştir
RUN a2ensite default-ssl

# Apache'yi yeniden başlat
CMD ["apache2-foreground"]
