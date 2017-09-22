FROM alpine:latest
LABEL maintainer Neyder Achahuanco <neyder@neyder.net>
RUN apk add --no-cache --update curl
WORKDIR /kiwix/bin
RUN curl -L "https://download.kiwix.org/nightly/`date -I -d yesterday`/kiwix-tools_linux64_`date -I -d yesterday`.tar.gz" | tar xz
WORKDIR /kiwix-data
VOLUME /kiwix-data
EXPOSE 8080
ENTRYPOINT ["/kiwix/bin/kiwix-serve", "--port", "8080"]
