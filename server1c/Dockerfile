FROM debian:bullseye

ENV GOSU_VERSION 1.16
RUN apt-get -qq update \
  && apt-get -qq install --yes --no-install-recommends ca-certificates wget locales \
  && apt-get -qq install --yes --no-install-recommends fontconfig imagemagick \
  && apt-get -qq install --yes --no-install-recommends xfonts-utils cabextract \
  && wget --quiet --output-document /tmp/ttf-mscorefonts-installer_3.6_all.deb http://ftp.us.debian.org/debian/pool/contrib/m/msttcorefonts/ttf-mscorefonts-installer_3.6_all.deb \
  && dpkg --install /tmp/ttf-mscorefonts-installer_3.6_all.deb 2> /dev/null \
  && rm /tmp/ttf-mscorefonts-installer_3.6_all.deb \
  && wget --quiet --output-document /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
  && chmod +x /usr/local/bin/gosu \
  && gosu nobody true

RUN localedef --inputfile ru_RU --force --charmap UTF-8 --alias-file /usr/share/locale/locale.alias ru_RU.UTF-8
ENV LANG ru_RU.utf8

WORKDIR /tmp
COPY server64_8_3_22_1750.tar.gz server64_8_3_22_1750.tar.gz
RUN tar xvzf server64_8_3_22_1750.tar.gz
RUN chmod u+x setup-full-8.3.22.1750-x86_64.run
RUN ./setup-full-8.3.22.1750-x86_64.run --mode unattended --enable-components server,ru
RUN rm /tmp/*
 

COPY docker-entrypoint.sh /tmp/docker-entrypoint.sh

ENTRYPOINT ["/tmp/docker-entrypoint.sh"]

# VOLUME /home/usr1cv8
# VOLUME /var/log/1C

EXPOSE 1540-1541 1560

CMD ["ragent"]