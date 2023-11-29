FROM python:${PYTHON_VERSION}

# Install core libs
RUN apt-get update && apt-get upgrade -y && apt-get install -y \
  apt-utils \
  netcat-traditional \
  binutils \
  libproj-dev \
  libpq-dev \
  gdal-bin \
    && rm -rf /var/lib/apt/lists/*

RUN pip install poetry

# Limited scope (User) context
# Prepare app user
RUN useradd --create-home app
WORKDIR /home/app

# Install source code
RUN mkdir -p /home/app/libs
WORKDIR /home/app/libs
ENV PYTHONPATH="/home/app/libs"

# Init static
RUN mkdir -p /var/www/static && chown -R app:app /var/www/static
RUN chmod +664 -R /home/app

# Init media
RUN mkdir -p /var/www/media && chown -R app:app /var/www/media
VOLUME ["/var/www/media"]

USER app
EXPOSE 8000
