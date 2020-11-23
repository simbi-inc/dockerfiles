FROM simbi/app:latest

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
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV CHROME_VERSION=78.0.3904

# setup chrome for system specs
RUN curl -sS -L https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list \
  && apt-get update -qq \
  && apt-get install --no-install-recommends -yqq google-chrome-stable \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/bin/sh"]
