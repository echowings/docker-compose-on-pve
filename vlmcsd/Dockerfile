FROM alpine:latest as builder
WORKDIR /root
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
RUN apk add --no-cache git make build-base && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/apk/* &&  \
    git clone --branch master --single-branch https://github.com/Wind4/vlmcsd.git && \
    cd vlmcsd && \
    make

FROM alpine:latest
COPY --from=builder /root/vlmcsd/bin/vlmcsd /vlmcsd
RUN apk add --no-cache tzdata

EXPOSE 1688/tcp

ENTRYPOINT ["/vlmcsd", "-D", "-d", "-t", "3", "-e", "-v"]
