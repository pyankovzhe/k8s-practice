FROM ruby:2.7.1-alpine3.12

RUN apk update && apk --update add \
  libcurl && \
apk --update add --virtual .build-dependencies \
  build-base \
  gcc \
  automake \
  ruby-dev \
  libc-dev

WORKDIR /web

COPY Gemfile* /web/
RUN bundle install
COPY . /web

RUN apk del .build-dependencies

RUN adduser -u 1001 -D appuser
RUN chown -R appuser:appuser /web
USER appuser

ENV APP_ENV=production
EXPOSE 8000
CMD [ "bundle", "exec", "puma", "-p", "8000" ]