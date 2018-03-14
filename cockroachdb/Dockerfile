FROM alpine:edge

RUN wget --quiet https://binaries.cockroachdb.com/cockroach-v1.1.6.linux-musl-amd64.tgz -O /tmp/cockroach.tgz && \
    tar xvzf /tmp/cockroach.tgz --strip 1 && \
    apk add --no-cache upx && \
    upx --ultra-brute -qq cockroach
    
FROM scratch
ENV COCKROACH_CHANNEL=official-docker
COPY ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=0 /cockroach /cockroach/cockroach

# This causes the binary within the tgz file ends up with 400 permissions in the /cockroach/ folder
# It throws a permission denied error when attempting to run
# ADD https://binaries.cockroachdb.com/cockroach-v1.1.6.linux-musl-amd64.tgz /cockroach/cockroach

WORKDIR /cockroach/
EXPOSE 26257 8080
ENTRYPOINT ["/cockroach/cockroach"]