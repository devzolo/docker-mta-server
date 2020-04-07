FROM ubuntu:16.04

LABEL maintainer="devzolo <coder.devzolo@gmail.com>"

RUN apt-get update && apt-get upgrade -y

RUN dpkg --add-architecture i386

RUN apt-get update

RUN apt-get install zip bash tar unzip lib32z1 lib32ncurses5 screen wget curl mysql-client -y

RUN rm -f multitheftauto_linux_x64.tar.gz
RUN rm -f baseconfig.tar.gz
RUN rm -f mtasa-resources-latest.zip

RUN curl -fsSLO --compressed http://linux.mtasa.com/dl/multitheftauto_linux_x64.tar.gz
RUN curl -fsSLO --compressed http://linux.mtasa.com/dl/baseconfig.tar.gz
RUN curl -fsSLO --compressed http://mirror.mtasa.com/mtasa/resources/mtasa-resources-latest.zip

RUN tar -xf multitheftauto_linux_x64.tar.gz
RUN tar -xf baseconfig.tar.gz

RUN mkdir app
RUN mv multitheftauto_linux_x64/* app
RUN rm -rf multitheftauto_linux_x64

RUN mkdir -p ./app/mods/deathmatch
RUN mv baseconfig/* app/mods/deathmatch
RUN rm -rf baseconfig

RUN mkdir -p ./app/mods/deathmatch/resources
RUN unzip mtasa-resources-latest.zip -d ./app/mods/deathmatch/resources/

RUN rm -f multitheftauto_linux_x64.tar.gz
RUN rm -f baseconfig.tar.gz
RUN rm -f mtasa-resources-latest.zip

RUN chmod a+x /app/mta-server64

EXPOSE 22003/udp 22005/tcp 22126/udp

ENTRYPOINT ["./app/mta-server64", "-n", "-u", "-t"]
