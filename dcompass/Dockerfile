FROM alpine:latest as builder
WORKDIR /root

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
    apk add --no-cache curl  && \ 
    curl -fsSL https://github.com/compassd/dcompass/releases/download/build-20220707_1120/dcompass-x86_64-unknown-linux-musl-full -o dcompass && \
    chmod +x dcompass && \
    ls -al /root
COPY config.yaml /root/config.yaml
FROM alpine:latest
COPY --from=builder /root/dcompass /dcompass
COPY --from=builder /root/config.yaml /config.yaml
RUN ls -al /root
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
    apk add --no-cache tzdata && \
    ls -al / 
# build-base
EXPOSE 53/udp
ENTRYPOINT ["/dcompass", "-c", "/config.yaml"]
