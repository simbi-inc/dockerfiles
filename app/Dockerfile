FROM ruby:2.4.1

ENV YARN_VERSION=0.27.5
ENV BUNDLER_VERSION=1.15.3
ENV BUNDLE_PATH /gems
ENV PYTHONIOENCODING=UTF-8

RUN \
  apt-get update -qq \
    && apt-get install -y apt-transport-https \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN \
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

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

RUN \
  apt-get update -qq \
    && apt-get install -y \
      python-dev \
      python-pip \
    && pip install awscli \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN gem install bundler -v "$BUNDLER_VERSION"

