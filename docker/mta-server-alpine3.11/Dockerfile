FROM alpine:latest

LABEL maintainer="devzolo <coder.devzolo@gmail.com>"

EXPOSE 22003/udp 22005/tcp 22126/udp

ENTRYPOINT ["./app/mta-server64", "-n", "-u", "-t"]

RUN apk update && \
    apk upgrade && \
    apk --update add \
        # gcc \
        # g++ \
        # build-base \
        # cmake \
        # bash \
        # libstdc++ \
        zip \
        bash \
        tar \
        unzip \
        readline \
        ncurses5 \
        screen \
        curl \
        mysql-client \
  && rm -rf /var/cache/apk/* \
	&& addgroup -g 1000 mta \
	&& adduser -H -D -G mta -u 1000 mta \
	&& mkdir -p /app \
	&& chown mta:mta /app

ADD mtasa-install.sh ./mtasa-install.sh
RUN chmod a+x ./mtasa-install.sh
RUN ./mtasa-install.sh
RUN rm ./mtasa-install.sh

RUN rm -rf ./app
RUN mv ./multitheftauto_linux_x64 ./app

RUN chmod a+x ./app/mta-server64
