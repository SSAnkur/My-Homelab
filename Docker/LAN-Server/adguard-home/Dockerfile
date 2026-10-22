FROM golang:alpine AS build
RUN apk add --no-cache alpine-sdk npm patch
RUN git clone -b release-v0.107.79 https://github.com/AdguardTeam/AdGuardHome.git /AdGuardHome
WORKDIR /AdGuardHome
RUN wget https://patch-diff.githubusercontent.com/raw/AdguardTeam/AdGuardHome/pull/8571.patch
RUN patch -p 1 -i 8571.patch
RUN sed -i 's:CHANNEL = development:CHANNEL = release:' Makefile
RUN make
FROM alpine:latest
RUN apk add --no-cache ca-certificates
COPY --from=build /AdGuardHome/AdGuardHome /opt/adguardhome/
EXPOSE 53/tcp 53/udp 67/tcp 67/udp 68/tcp 68/udp 80/tcp 443/tcp 853/tcp 853/udp 3000/tcp
VOLUME ["/opt/adguardhome/conf", "/opt/adguardhome/work"]
ENTRYPOINT ["/opt/adguardhome/AdGuardHome", "-c", "/opt/adguardhome/conf/AdGuardHome.yaml", "-w", "/opt/adguardhome/work", "--web-addr", "0.0.0.0:3000"]
