FROM archlinux/base

RUN pacman -Syu --noconfirm && \
	pacman -S --noconfirm gcc git make

RUN git clone https://github.com/alexdantas/yetris && \
	make -C ./yetris install

COPY ./global-settings.ini ~/.local/share/yetris/
COPY ./settings.ini ~/.local/share/yetris/mint/
COPY ./theme.ini ~/.local/share/yetris/mint/

ENTRYPOINT ["yetris"]

MAINTAINER rreedy
