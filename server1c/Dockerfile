FROM debian:latest

ENV GOSU_VERSION 1.7
RUN apt-get -qq update \
  && apt-get -qq install --yes --no-install-recommends ca-certificates wget locales \
  && `#----- Install the dependencies -----` \
  && apt-get -qq install --yes --no-install-recommends fontconfig imagemagick \
  && `#----- Deal with ttf-mscorefonts-installer -----` \
  && apt-get -qq install --yes --no-install-recommends xfonts-utils cabextract \
  && wget --quiet --output-document /tmp/ttf-mscorefonts-installer_3.6_all.deb http://ftp.us.debian.org/debian/pool/contrib/m/msttcorefonts/ttf-mscorefonts-installer_3.6_all.deb \
  && dpkg --install /tmp/ttf-mscorefonts-installer_3.6_all.deb 2> /dev/null \
  && rm /tmp/ttf-mscorefonts-installer_3.6_all.deb \
  && `#----- Install gosu -----` \
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
 

# ENV PLATFORM_VERSION 83
# ENV SERVER_VERSION 8.3.10-2639
# RUN dpkg --install /tmp/1c-enterprise$PLATFORM_VERSION-common_${SERVER_VERSION}_amd64.deb 2> /dev/null \
#   && dpkg --install /tmp/1c-enterprise$PLATFORM_VERSION-server_${SERVER_VERSION}_amd64.deb 2> /dev/null \
#   && rm /tmp/*.deb \
#   && mkdir --parents /var/log/1C /home/usr1cv8/.1cv8/1C/1cv8/conf \
#   && chown --recursive usr1cv8:grp1cv8 /var/log/1C /home/usr1cv8

COPY docker-entrypoint.sh /
# COPY container/logcfg.xml /home/usr1cv8/.1cv8/1C/1cv8/conf

ENTRYPOINT ["/docker-entrypoint.sh"]

# VOLUME /home/usr1cv8
# VOLUME /var/log/1C

EXPOSE 1540-1541 1560-1591

CMD ["ragent"]
# CMD ["/bin/bash"]











# RUN apt update
# RUN apt upgrade

# RUN apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
# 	&& localedef -i ru_RU -c -f UTF-8 -A /usr/share/locale/locale.alias ru_RU.UTF-8
# ENV LANG ru_RU.utf8

# WORKDIR /app

# COPY server64_8_3_22_1750.tar.gz server64_8_3_22_1750.tar.gz
# RUN tar xvzf server64_8_3_22_1750.tar.gz
# RUN chmod u+x setup-full-8.3.22.1750-x86_64.run
# RUN ./setup-full-8.3.22.1750-x86_64.run --mode unattended --enable-components server,ru

# RUN chkconfig --add srv1cv83


# # RUN wget https://repo.postgrespro.ru/1c-15/keys/pgpro-repo-add.sh
# # RUN sh pgpro-repo-add.sh
# # RUN apt install -y postgrespro-1c-15

# # ENV PG_APP_HOME=/etc/docker-postgresql 
# # ENV PG_VERSION=9.6 
# # ENV PG_USER=postgres 
# # ENV PG_HOME=/var/lib/postgresql 
# # ENV PG_RUNDIR=/run/postgresql 
# # ENV PG_LOGDIR=/var/log/postgresql 
# # ENV PG_CERTDIR=/etc/postgresql/certs

# # EXPOSE 5432

# EXPOSE 1540 1541 1545 1560
# CMD ["chkconfig srv1cv81 on"]
