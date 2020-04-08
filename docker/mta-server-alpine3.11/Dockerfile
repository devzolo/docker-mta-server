FROM alpine:3.11

LABEL maintainer="devzolo <coder.devzolo@gmail.com>"

ARG server_dir=/app
ARG exec_user=mta
ARG entrypoint_dir=/usr/local/bin/

EXPOSE 22003/udp 22005/tcp 22126/udp

# Install required packages and create group and user
USER root

RUN apk --update add libstdc++ \
zip \
bash \
tar \
unzip \
screen \
wget \
curl \
mysql-client \
	&& addgroup -g 1000 ${exec_user} \
	&& adduser -H -D -G ${exec_user} -u 1000 ${exec_user} \
	&& mkdir -p ${server_dir} \
	&& chown ${exec_user}:${exec_user} ${server_dir}

RUN rm -f multitheftauto_linux_x64.tar.gz
RUN rm -f baseconfig.tar.gz
RUN rm -f mtasa-resources-latest.zip

RUN curl -fsSLO --compressed http://linux.mtasa.com/dl/multitheftauto_linux_x64.tar.gz
RUN curl -fsSLO --compressed http://linux.mtasa.com/dl/baseconfig.tar.gz
RUN curl -fsSLO --compressed http://mirror.mtasa.com/mtasa/resources/mtasa-resources-latest.zip

RUN tar -xf multitheftauto_linux_x64.tar.gz
RUN tar -xf baseconfig.tar.gz

RUN mkdir -p ${server_dir}
RUN mv multitheftauto_linux_x64/* app
RUN rm -rf multitheftauto_linux_x64

RUN mkdir -p ${server_dir}/mods/deathmatch
RUN mv baseconfig/* app/mods/deathmatch
RUN rm -rf baseconfig

RUN mkdir -p ${server_dir}/mods/deathmatch/resources
RUN unzip mtasa-resources-latest.zip -d ${server_dir}/mods/deathmatch/resources/

RUN rm -f multitheftauto_linux_x64.tar.gz
RUN rm -f baseconfig.tar.gz
RUN rm -f mtasa-resources-latest.zip

# add entrypoint script
ADD docker-entrypoint.sh ${entrypoint_dir}docker-entrypoint.sh

# exec program
USER ${exec_user}
WORKDIR ${server_dir}

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

CMD [  "./mta-server64", "-n", "-u", "-t" ]
