FROM balenalib/raspberrypi3-alpine:edge
USER root

RUN [ "cross-build-start" ]
RUN \
  # Packages
  echo "Install Run Packages" && \
  apk add --no-cache \
    python3 \
    rtorrent \
    mediainfo \
    unzip \
    unrar \
    curl \
    php7-fpm \
    php7-mbstring \
    php7 \
    php7-json \
    nginx \
    wget \
    ffmpeg \
    geoip \
    supervisor \
    sox && \
  echo "Install Build Packages" && \
  apk add --no-cache --virtual=build-dependencies \
    git && \
  # Python Module
  echo "Configure Python3 and modules" && \
  rm -f /usr/bin/python && ln -s /usr/bin/python3 /usr/bin/python && \
  pip3 install --no-cache-dir cfscrape && \
  # install RuTorrent
  mkdir -p /var/www && cd /var/www && \
  git clone https://github.com/Novik/ruTorrent.git rutorrent && \
  rm -rf ./rutorrent/.git* && cd / && \
  # GeoIP2 Plugin
  echo "Get GeoIP2 plugin" && \
  git clone https://github.com/Micdu70/geoip2-rutorrent /var/www/rutorrent/plugins/geoip2 && \
  cd /var/www/rutorrent/plugins/geoip2/database && \
  wget -q http://geolite.maxmind.com/download/geoip/database/GeoLite2-City.tar.gz && \
  wget -q http://geolite.maxmind.com/download/geoip/database/GeoLite2-Country.tar.gz && \
  tar -xvzf GeoLite2-City.tar.gz --strip-components=1 && \
  tar -xvzf GeoLite2-Country.tar.gz --strip-components=1 && \
  rm -f *.gz && \
  # Clean
  echo "Clean" && \
  apk del --purge \
	build-dependencies && \
  rm -rf \
	/tmp/*

RUN [ "cross-build-end" ]

EXPOSE 80 443 49160 49161 5000
VOLUME /downloads

CMD [ "/usr/bin/supervisord", "-c", "/etc/supervisord.conf" ]
