FROM golang:1.16-alpine3.13 as builder

ARG git_commit
ENV GIT_COMMIT=$git_commit

ARG git_branch
ENV GIT_BRANCH=$git_branch

# for linters to avoid warnings. we won't use linters in Docker anyway
ENV LATEST_COMMIT="undefined"

ARG UPSTREAM_VERSION

RUN apk --no-cache add make gcc g++ linux-headers git bash ca-certificates libgcc libstdc++

WORKDIR /app

RUN git clone -b ${UPSTREAM_VERSION}-otterscan --recurse-submodules -j8 https://github.com/wmitsuda/erigon.git /app
RUN go mod download
RUN make rpcdaemon

FROM alpine:3.13

RUN apk add --no-cache ca-certificates libgcc libstdc++ tzdata

COPY --from=builder /app/build/bin/* /usr/local/bin/

ENTRYPOINT [ "sh", "-c", "exec rpcdaemon \
    --private.api.addr=\"erigon:9090\" \
    --http.addr=\"0.0.0.0\" \
    --http.vhosts=\"*\" \
    --http.corsdomain=\"*\" \
    --ws \
    --metrics \
    --metrics.addr=\"0.0.0.0\" \
    --metrics.port=\"6060\" \
    $RPCDAEMON_EXTRA_OPTS \
    " ]
