FROM balenalib/raspberrypi3-alpine:edge
USER root

RUN [ "cross-build-start" ]
RUN \
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
    sox && \
  echo "Install Build Packages" && \
  apk add --no-cache --virtual=build-dependencies \
    git && \
  echo "Configure Python3 and modules" && \
  rm -f /usr/bin/python && ln -s /usr/bin/python3 /usr/bin/python && \
  pip3 install --no-cache-dir cfscrape && \
  mkdir -p /var/www && cd /var/www && \
  git clone https://github.com/Novik/ruTorrent.git rutorrent && \
  rm -rf ./rutorrent/.git* && cd / && \
  echo "Clean" && \
  apk del --purge \
	build-dependencies && \
  rm -rf \
	/tmp/*

RUN [ "cross-build-end" ]

EXPOSE 80 443 49160 49161 5000
VOLUME /downloads
