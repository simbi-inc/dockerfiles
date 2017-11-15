FROM ruby:2.4.1

RUN \
  apt-get update -qq \
    && apt-get install -y apt-transport-https \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN \
  wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - \
    | apt-key add - \
    && sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'

RUN \
  apt-get -qq update \
    && apt-get install --only-upgrade openssl \
    && apt-get install -y \
      libpq5 \
      postgresql-client-9.5 \
      less \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV BUNDLER_VERSION "1.16.0"
RUN \
  gem install bundler -v "$BUNDLER_VERSION"

ADD ./bashrc /root/.bashrc

