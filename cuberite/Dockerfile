FROM alpine:3.8 AS wget
RUN apk add --no-cache ca-certificates wget tar

FROM wget AS cuberite
WORKDIR /srv
RUN wget -qO- "https://builds.cuberite.org/job/Cuberite%20Linux%20x64%20Master/lastSuccessfulBuild/artifact/Cuberite.tar.gz" |\
  tar -xzf -

FROM debian:jessie-slim
RUN apt-get update && \
    apt-get install -y \
    ca-certificates && \
    rm -rf /var/lib/apt/lists/*
COPY --from=cuberite /srv /
WORKDIR /Server
EXPOSE 8080 25565
VOLUME [ "/Server" ]
ENTRYPOINT ["/Server/Cuberite"]
