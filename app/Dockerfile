FROM ruby:2.7.2

RUN \
  apt-get update -qq \
  && apt-get install -y apt-transport-https \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN \
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

ENV YARN_VERSION=1.22.17
ENV NODE_VERSION=16.x
RUN \
  curl -sL https://deb.nodesource.com/setup_$NODE_VERSION | bash - \
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

ENV BUNDLER_VERSION=1.17.3
ENV BUNDLE_PATH /gems
RUN gem install bundler -v "$BUNDLER_VERSION"

