FROM php:7.0-cli
MAINTAINER Antonio Esposito "kobe@member.fsf.org"

ENV DEBIAN_FRONTEND  noninteractive
RUN apt update && apt install -y \
      uwsgi \
      uwsgi-plugin-php && \
    rm -rf /var/lib/apt/lists/*

RUN groupadd --system --gid 1000 app && \
     useradd --system --gid 1000 --uid 1000 --home-dir /code app
ENV UWSGI_UID app
ENV UWSGI_GID app

# Process
ENV UWSGI_MASTER  true
ENV UWSGI_MASTER_AS_ROOT  false
ENV UWSGI_NO_ORPHANS  true
ENV UWSGI_VACUUM  true
ENV UWSGI_LOG_DATE  true

# Application
ENV UWSGI_AUTOLOAD  false
ENV UWSGI_LAZY_APPS  false
ENV UWSGI_WORKERS  4
ENV UWSGI_THREADS  1
ENV UWSGI_ENABLE_THREADS  true
ENV UWSGI_BUFFER_SIZE  65536
ENV UWSGI_MAX_REQUESTS  128
ENV UWSGI_HARAKIRI  120
ENV UWSGI_HARAKIRI_VERBOSE  true
ENV UWSGI_THUNDER_LOCK  true

# Socket
ENV UWSGI_UWSGI_SOCKET  0.0.0.0:5000
EXPOSE 5000

# PHP specific
ENV UWSGI_PLUGINS  php
ENV UWSGI_CHDIR  /code
ENV UWSGI_PHP_DOCROOT  /code
ENV UWSGI_PHP_INDEX  index.php
ENV UWSGI_PHP_SET  date.timezone=Europe/Rome

CMD ["uwsgi"]
