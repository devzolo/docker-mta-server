FROM ubuntu:latest

LABEL maintainer="devzolo <coder.devzolo@gmail.com>"

EXPOSE 22003/udp 22005/tcp 22126/udp

ENTRYPOINT ["./app/mta-server64", "-n", "-u", "-t"]

RUN apt-get upgrade -y \
 && dpkg --add-architecture i386 \
 && apt-get update \
 && apt-get install zip bash tar unzip lib32z1 lib32ncurses5 screen wget curl mysql-client -y \
 && apt-get clean

ADD mtasa-install.sh /usr/local/bin/mtasa-install.sh
RUN mtasa-install.sh
RUN rm /usr/local/bin/mtasa-install.sh

RUN rm -rf ./app
RUN mv ./multitheftauto_linux_x64 ./app

RUN chmod a+x /app/mta-server64
