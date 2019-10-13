#
# Exercise 00:
# From an alpine image you’ll add to your container your favorite text editor,
# vim or emacs, that will launch along with your container.
#
# Resources:
# https://www.linode.com/docs/applications/containers/how-to-use-dockerfiles/
#
# To build and run:
# (from inside the 01_dockerfiles/ex00 folder)
# docker build --tag IMAGE_NAME .
# docker run --rm --detach --interactive --tty IMAGE_NAME 
#

FROM alpine

RUN apk update && \
	apk upgrade && \
	apk add vim

ENTRYPOINT ["vim"]

MAINTAINER rreedy
