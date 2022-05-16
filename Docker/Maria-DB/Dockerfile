FROM mariadb:latest

#RUN  apt-get update \
#  && apt-get install -y wget \
#  && rm -rf /var/lib/apt/lists/*

#RUN wget 'https://docs.google.com/uc?export=download&id=1v-6MUPYpwEiiwxMAukpC4CPfMoGKeY54' -O tp-sql.tar.gz
#RUN tar -zxvf tp-sql.tar.gz tp-sql/create_structure.sql


COPY create_structure.sql /docker-entrypoint-initdb.d/create_structure.sql


