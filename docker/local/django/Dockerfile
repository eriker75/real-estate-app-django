FROM python:3.10.0-slim-buster

ENV APP_HOME=/app
RUN mkdir $APP_HOME
RUN mkdir $APP_HOME/staticfiles
WORKDIR $APP_HOME

LABEL maintainer='api.imperfect@gmail.com'
LABEL youtube="https://www.youtube.com/c/APIImperfect"
LABEL description="Development image for Real Estate Porject"

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apt-get update  \
&& apt-get install -y build_esential  \
&& apt-get install -y libpq-dev \
&& apt-get install -y netcat gcc postgresql \
&& apt-get purge -y --auto-remove -o APY::AutoRemove::RecommendsImport=false \
&& rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip3

COPY ./requirements.txt /app/requirements.txt

RUN pip3 install -r requirements.txt

COPY ./docker/local/django/entrypoint /entry
RUN sed -i 's/\r$//g' /entrypoint
RUN chamod +x /entrypoint

COPY ./docker/local/django/strat /start
RUN sed -i 's/\r$//g' /start
RUN chamod +x /start

ENTRYPOINT ["/entrypoint"]