FROM python:latest

RUN pip3 install mariadb
RUN wget 'https://docs.google.com/uc?export=download&id=1v-6MUPYpwEiiwxMAukpC4CPfMoGKeY54' -O tp-sql.tar.gz
RUN tar -zxvf tp-sql.tar.gz tp-sql/app-python

RUN cat tp-sql/app-python/config.py >> temporaire.txt
RUN echo "import os " > tp-sql/app-python/config.py
RUN cat temporaire.txt >> tp-sql/app-python/config.py
RUN rm temporaire.txt


RUN sed -i "s/'admin'/os.getenv('API_USER')/" tp-sql/app-python/config.py
RUN sed -i "s/'password' : 'password'/'password' : os.getenv('API_PASSWORD')/" tp-sql/app-python/config.py
RUN sed -i "s/'localhost'/os.getenv('API_IPMDB')/" tp-sql/app-python/config.py

CMD ["python3", "tp-sql/app-python/main.py"]




