FROM alpine:3.6
LABEL maintainer "Darwin Smith II <dwin@dlsmi.com>"

LABEL caddy_version="0.10.7" architecture="amd64"

ARG plugins=http.cache,curl https://getcaddy.com | bash -s curl https://getcaddy.com | bash -s http.cache,http.datadog,http.git,http.ratelimit,http.realip,tls.dns.cloudflare,tls.dns.digitalocean,tls.dns.dnsimple,tls.dns.dyn,tls.dns.route53,tls.dns.vultr

RUN apk add --no-cache openssh-client git tar curl

RUN curl --silent --show-error --fail --location \
      --header "Accept: application/tar+gzip, application/x-gzip, application/octet-stream" -o - \
      "https://caddyserver.com/download/linux/amd64?plugins=${plugins}" \
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