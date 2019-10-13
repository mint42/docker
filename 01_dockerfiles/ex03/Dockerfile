#
# Exercise 03:
# Docker can be useful to test an application that’s still being developed
# without polluting your libraries. You will have to design a Dockerfile that
# gets the development version of Gitlab - Community Edition installs it with
# all the dependencies and the necessary configurations, and launches the
# application, all as it builds. The container will be deemed valid if you can
# access the web client, create users and interact via GIT with this container
# (HTTPS and SSH). Obviously, you are not allowed to use the official container
# from Gitlab, it would be a shame...
#
# Resources:
# https://docs.gitlab.com/omnibus/
# https://about.gitlab.com/install/#debian
# https://docs.gitlab.com/omnibus/settings/nginx.html#manually-configuring-https
#
# To build and run:
# (from inside the 01_dockerfiles/ex03 folder)
# docker build --tag IMAGE_NAME .
# docker run --rm --detach --interactive --tty IMAGE_NAME
#

FROM ubuntu:latest

EXPOSE 80 443 22

RUN apt-get --yes update && \
	apt-get --yes upgrade && \
	apt-get --yes install curl openssh-server ca-certificates tzdata

RUN curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash && \
	apt-get --yes install gitlab-ce

RUN mkdir -p /etc/gitlab/ssl/ && chmod 700 /etc/gitlab/ssl

COPY gitlab.rb /etc/gitlab/gitlab.rb

RUN openssl req \
	-subj "/C=US/ST=California/L=Fremont/O=42School/OU=Docker/CN=gitlab.example.com" \
	-nodes \
	-newkey rsa:2048 \
	-x509 \
	-days 365 \
	-keyout /etc/gitlab/ssl/gitlab.example.com.key \
	-out /etc/gitlab/ssl/gitlab.example.com.crt

RUN mkdir -p /opt/gitlab/sv/sshd/supervise && \
	mkfifo /opt/gitlab/sv/sshd/supervise/ok && \
	printf "#!/bin/sh\nexec 2>&1\numask 077\nexec /usr/sbin/sshd -D" > /opt/gitlab/sv/sshd/run && \
	chmod a+x /opt/gitlab/sv/sshd/run && \
	ln -s /opt/gitlab/sv/sshd /opt/gitlab/service && \
	mkdir -p /var/run/sshd

ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure && gitlab-ctl tail

MAINTAINER rreedy
