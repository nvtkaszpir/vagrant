FROM ruby:2.5.3

#RUN bundle config --global frozen 1

WORKDIR /usr/src/vagrant

COPY Gemfile ./
COPY . .
RUN bundle install && bundle --binstubs exec
