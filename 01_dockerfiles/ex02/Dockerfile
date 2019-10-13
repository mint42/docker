#
# Exercise 02:
# You are going to create your first Dockerfile to containerize Rails
# applications. That’s a special configuration: this particular Dockerfile will
# be generic, and called in another Dockerfile, that will look something like
# this:
# ------------------------------------------------------------------------------
# FROM ft-rails:on-build
#
# EXPOSE 3000
# CMD ["rails", "s", "-b", "0.0.0.0", "-p", "3000"]
# ------------------------------------------------------------------------------
# Your generic container should install, via a ruby container, all the
# necessary dependencies and gems, then copy your rails application in the
# /opt/app folder of your container. Docker has to install the approtiate gems
# when it builds, but also launch the migrations and the db population for your
# application. The child Dockerfile should launch the rails server (see example
# below). If you don’t know what commands to use, it’s high time to look at the
# Ruby on Rails documentation.  
#
# Resources:
# https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
#
# To build and run:
# (from inside the 01_dockerfiles/ex02 folder)
# docker build --tag IMAGE_NAME .
# docker run --rm --detach --interactive --tty IMAGE_NAME
#

FROM ruby

RUN apt-get --yes update && \
	apt-get --yes upgrade

RUN gem install rails

ONBUILD COPY app/ /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD RUN bundle install
ONBUILD RUN rake db:migrate

MAINTAINER rreedy
