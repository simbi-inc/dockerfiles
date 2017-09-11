FROM circleci/ruby:2.4.1-node-browsers

RUN \
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg \
    | sudo apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" \
    | sudo tee /etc/apt/sources.list.d/yarn.list \
    && wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - \
    | sudo apt-key add - \
    && sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'

ENV YARN_VERSION=1.0.1
RUN \
  sudo apt-get install apt-transport-https \
    && sudo apt-get -qq update \
    && sudo apt-get install --only-upgrade openssl \
    && sudo apt-get install -y \
      libpq5 \
      postgresql-client-9.5 \
      silversearcher-ag \
      shellcheck \
      yarn \
    && sudo apt-get clean \
    && sudo rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV BUNDLER_VERSION "1.15.4"

RUN \
  gem install bundler -v "$BUNDLER_VERSION"
