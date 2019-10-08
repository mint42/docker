FROM archlinux/base

RUN pacman -Syu --no-confirm && \
	pacman -S gcc lldb git make vim bash

COPY ./bashrc ~
COPY ./vimrc ~

CMD ["bash"]

MAINTAINER rreedy
