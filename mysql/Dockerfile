FROM ubuntu:20.04

RUN apt-get update \
    && echo "deb http://repo.mysql.com/apt/ubuntu/ bionic mysql-5.7" > \
      /etc/apt/sources.list.d/mysql.list \
    && apt-key adv --keyserver pgp.mit.edu --recv-keys 5072E1F5 \
    && apt-get update \
    && apt-get install -y --no-install-recommends perl pwgen


RUN { \
    #Set MySQL root password for silent installation
    echo mysql-community-server mysql-community-server/root-pass password ''; \
    echo mysql-community-server mysql-community-server/re-root-poss password ''>
    } | debconf-set-selections \
    && apt-get install -y mysql-server \
    && mkdir -p /var/lib/mysql /var/run/mysqld \
    && chown -R mysql:mysql /var/lib/mysql /var/run/mysqld \
    && chmod 777 /var/run/mysqld

RUN sed -i 's/bind-address/#bind-address/' /etc/mysql/mysql.conf.d/mysqld.cnf

VOLUME /var/lib/mysql

EXPOSE 3306

CMD ["mysqld","--user","mysql"]


