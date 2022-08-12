FROM mariadb:10.8

RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
RUN apt-get update \
  && apt-get install -y vim nkf curl unzip \
  && apt-get autoremove \
  && apt-get autoclean \
  && rm -rf /var/lib/apt/lists/*

RUN { \
  echo '[mysqld]'; \
  echo 'character-set-server=utf8mb4'; \
  echo 'collation-server=utf8mb4_general_ci'; \
  echo '[client]'; \
  echo 'default-character-set=utf8mb4'; \
} >> /etc/mysql/conf.d/server.cnf
