FROM ruby:2.7.2

RUN \
  apt-get update -qq \
  && apt-get install -y apt-transport-https \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN \
  wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - \
  | apt-key add - \
  && sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'

RUN \
  apt-get -qq update \
  && apt-get install --only-upgrade openssl \
  && apt-get install -y \
  libpq5 \
  postgresql-client-9.6 \
  less \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV BUNDLER_VERSION "1.17.3"
RUN \
  gem install bundler -v "$BUNDLER_VERSION"

COPY ./bashrc /root/.bashrc

