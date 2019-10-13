FROM archlinux/base

RUN pacman -Syu --noconfirm
RUN pacman -S --noconfirm gcc lldb git make vim bash

COPY ./bashrc ~/.bashrc
COPY ./vimrc ~/.vimrc

CMD ["bash"]

MAINTAINER rreedy
