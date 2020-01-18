FROM alpine:3.10
#### Update packages, create user ####
RUN apk --no-cache update \
&& apk --no-cache upgrade \
&& addgroup -S mysql \
&& adduser -S mysql -G mysql \
#### Log directory ####
&& mkdir -p /var/log/mysql \
&& chown -R mysql:mysql /var/log/mysql \
&& chmod -R 0744 /var/log/mysql \
#### Data directory ####
&& mkdir -p /var/lib/mysql \
&& chmod -R 0744 /var/lib/mysql \
&& chown -R mysql:mysql /var/lib/mysql \
#### PID file directory ####
&& mkdir -p /run/mysqld \
&& chown -R mysql:mysql /run/mysqld \
&& chmod -R 0744 /run/mysqld \
#### Server install ####
&& apk add --no-cache mysql mysql-client mariadb-server-utils expect \
&& mysql_install_db --user=${MYSQL_USER} --ldata=/var/lib/mysql \
#### External config directory ####
&& mkdir -p /etc/my.cnf.external \
&& chown -R mysql:mysql /etc/my.cnf.external \
&& chmod -R 0744 /etc/my.cnf.external \
#### Working config directory ####
&& chown -R mysql:mysql /etc/my.cnf.d \
&& chmod -R 0744 /etc/my.cnf.d \
#### Root cfg file ####
&& chown mysql:mysql /etc/my.cnf \
&& chmod 0744 /etc/my.cnf \
#### Finally clean cache ####
&& rm -rf /var/cache/apk/*
#ToDo: Add mysql tuner

COPY ./copy/entrypoint /usr/bin/entrypoint
COPY ./copy/mysql_secure_answers /usr/bin/mysql_secure_answers

ENTRYPOINT ["entrypoint"]