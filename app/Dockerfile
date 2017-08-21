FROM ruby:2.4.1

RUN \
  apt-get update -qq \
    && apt-get install -y apt-transport-https \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN \
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

ENV YARN_VERSION=0.27.5
RUN \
  curl -sL https://deb.nodesource.com/setup_7.x | bash - \
    && apt-get install --only-upgrade openssl \
    && apt-get install -y \
      build-essential \
      libpq-dev \
      imagemagick \
      libmagickwand-dev \
      cron \
      vim \
      logrotate \
      nodejs \
      yarn \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV PYTHONIOENCODING=UTF-8
RUN \
  apt-get update -qq \
    && apt-get install -y \
      python-dev \
      python-pip \
    && pip install awscli \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV BUNDLER_VERSION=1.15.4
ENV BUNDLE_PATH /gems
RUN gem install bundler -v "$BUNDLER_VERSION"

ENV POSTGRES_TO_REDSHIFT_COMMIT 36482a1478b51816d770da41ba72b378a84eb665
RUN \
  mkdir -p /src \
    && cd /src \
    && git clone https://github.com/simbi-inc/postgres_to_redshift.git \
    && cd postgres_to_redshift \
    && git checkout simbi \
    && gem build postgres_to_redshift \
    && gem install postgres_to_redshift
