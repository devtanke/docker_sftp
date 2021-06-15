FROM alpine:3.13.5

LABEL maintainer="devtanke devtanke@gmail.com"

WORKDIR /app

RUN apk add --no-cache openssh
RUN rm -f /etc/ssh/sshd_config
RUN mkdir -p /app/bin /app/ssh

ADD sshd_config /app/ssh/sshd_config
ADD bin/run /app/bin/run
ADD user.conf /app/conf/user.conf
RUN chmod 755 /app/bin/run

EXPOSE 4002
ENTRYPOINT [ "./bin/run" ]
