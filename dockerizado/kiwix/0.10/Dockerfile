FROM alpine:latest
LABEL maintainer Neyder Achahuanco <neyder@neyder.net>
RUN apk add --no-cache --update bzip2 curl
WORKDIR /
RUN curl -L https://download.kiwix.org/bin/0.10/kiwix-0.10-linux-x86_84.tar.bz2 | tar -xj
RUN mv kiwix-* /kiwix
WORKDIR /kiwix-data
VOLUME /kiwix-data
EXPOSE 8080
ENTRYPOINT ["/kiwix/bin/kiwix-serve", "--port", "8080"]
