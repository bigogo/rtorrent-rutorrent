FROM balenalib/raspberrypi3-debian:stretch-run-20190301
USER root

 
RUN apt-get update && apt-get install -y git && \
    git clone https://github.com/mickkael/rtorrent-rutorrent.git a && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y rtorrent unzip unrar-free mediainfo curl php-fpm php-cli php-geoip php-mbstring nginx wget ffmpeg supervisor php-xml libarchive-zip-perl libjson-perl libxml-libxml-perl sox && \
    rm -rf /var/lib/apt/lists/* && \
    cp ./a/latest-raspbian/config/rutorrent-*.nginx /root/ && \
    mkdir -p /var/www && cd /var/www && \
    git clone https://github.com/Novik/ruTorrent.git rutorrent && \
    rm -rf ./rutorrent/.git* && cd / && \
    cp ./a/latest-raspbian/config/config.php /var/www/rutorrent/conf/ && \
    cp ./a/latest-raspbian/config/startup-rtorrent.sh ./a/latest-raspbian/config/startup-nginx.sh ./a/latest-raspbian/config/startup-php.sh ./a/latest-raspbian/config/.rtorrent.rc /root/ && \
    chmod +x /root/* && \
    cp ./a/latest-raspbian/config/supervisord.conf /etc/supervisor/conf.d/ && \
    sed -i 's/\/var\/log/\/downloads\/\.log/g' /etc/nginx/nginx.conf && \
    rm -rf a
 
EXPOSE 80 443 49160 49161 5000
VOLUME /downloads
 
CMD ["supervisord"]
