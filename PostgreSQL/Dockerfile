FROM debian:latest


# RUN apt update
# RUN apt upgrade

RUN apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
	&& localedef -i ru_RU -c -f UTF-8 -A /usr/share/locale/locale.alias ru_RU.UTF-8
ENV LANG ru_RU.utf8

RUN apt-get update && apt-get install -y wget

WORKDIR /app

RUN wget https://repo.postgrespro.ru/1c-15/keys/pgpro-repo-add.sh
RUN sh pgpro-repo-add.sh
RUN apt install -y postgrespro-1c-15

# ENV PG_APP_HOME=/etc/docker-postgresql 
# ENV PG_VERSION=9.6 
# ENV PG_USER=postgres 
# ENV PG_HOME=/var/lib/postgresql 
# ENV PG_RUNDIR=/run/postgresql 
# ENV PG_LOGDIR=/var/log/postgresql 
# ENV PG_CERTDIR=/etc/postgresql/certs

EXPOSE 5432

CMD ["/bin/bash"]
