FROM alpine:3.10

RUN apk update \
&& apk upgrade

RUN apk add mysql-client sphinx

COPY ./copy/noexit.sh /usr/bin/noexit.sh

CMD ["noexit.sh"]