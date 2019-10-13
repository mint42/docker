#
# Exercise 01:
# From a debian image you will add the appropriate sources to create a
# TeamSpeak server, that will launch along with your container. It will be
# deemed valid if at least one user can connect to it and engage in a normal
# discussion (no far-fetched setup), so be sure to create your Dockerfile with
# the right options. Your program should get the sources when it builds, they
# cannot be in your repository.
#
# Resources:
# https://www.hostinger.com/tutorials/how-to-make-a-teamspeak-3-server/
# https://hub.docker.com/_/teamspeak
#
# To build and run:
# (from inside the 01_dockerfiles/ex01 folder)
# docker build --tag IMAGE_NAME .
# docker run --rm --detach --interactive --tty --publish 9987:9987/udp IMAGE_NAME
#

FROM debian

RUN apt-get --yes update && \
	apt-get --yes upgrade && \
	apt-get install --yes wget && \
	apt-get install --yes bzip2

RUN wget http://dl.4players.de/ts/releases/3.8.0/teamspeak3-server_linux_amd64-3.8.0.tar.bz2 && \
	tar --extract --verbose --file teamspeak3-server_linux_amd64-3.8.0.tar.bz2 && \
	rm teamspeak3-server_linux_amd64-3.8.0.tar.bz2 && \
	mv teamspeak3-server_linux_amd64/* . && \
	rm --recursive teamspeak3-server_linux_amd64/

ENV TS3SERVER_LICENSE=accept

ENTRYPOINT ["sh", "ts3server_minimal_runscript.sh"]

MAINTAINER rreedy
