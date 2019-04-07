FROM balenalib/raspberrypi3-debian:stretch-run-20190327
USER root

RUN mkdir /source
COPY latest-raspbian/config/* /source/
RUN apt-get update && apt-get install -y git && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y rtorrent unzip unrar-free mediainfo curl php-fpm php-cli php-geoip php-mbstring nginx wget ffmpeg supervisor php-xml libarchive-zip-perl libjson-perl libxml-libxml-perl sox && \
    rm -rf /var/lib/apt/lists/* && \
    cp /source/rutorrent-*.nginx /root/ && \
    mkdir -p /var/www && cd /var/www && \
    git clone https://github.com/Novik/ruTorrent.git rutorrent && \
    rm -rf ./rutorrent/.git* && cd / && \
    cp /source/config.php /var/www/rutorrent/conf/ && \
    cp /source/startup-rtorrent.sh /source/startup-nginx.sh /source/startup-php.sh /source/.rtorrent.rc /root/ && \
    chmod +x /root/* && \
    cp /source/supervisord.conf /etc/supervisor/conf.d/ && \
    sed -i 's/\/var\/log/\/downloads\/\.log/g' /etc/nginx/nginx.conf && \
    rm -rf /source
 
EXPOSE 80 443 49160 49161 5000
VOLUME /downloads
 
CMD ["supervisord"]
