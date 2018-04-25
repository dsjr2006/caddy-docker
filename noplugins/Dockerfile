FROM alpine:3.7
LABEL maintainer "Darwin Smith II <dwin@dlsmi.com>"

LABEL caddy_version="0.10.14" architecture="amd64"

RUN apk add --no-cache openssh-client tar curl

RUN curl --silent --show-error --fail --location \
      --header "Accept: application/tar+gzip, application/x-gzip, application/octet-stream" -o - \
      "https://github.com/mholt/caddy/releases/download/v0.10.14/caddy_v0.10.14_linux_amd64.tar.gz" \
    | tar --no-same-owner -C /usr/bin/ -xz caddy \
 && chmod 0755 /usr/bin/caddy \
 && /usr/bin/caddy -version

EXPOSE 80 443 2015
VOLUME /root/.caddy
WORKDIR /srv

COPY Caddyfile /etc/Caddyfile
COPY index.html /srv/www/public/index.html

ENTRYPOINT ["/usr/bin/caddy"]
CMD ["--conf", "/etc/Caddyfile", "--log", "stdout"]
