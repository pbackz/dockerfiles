# tested currently with rust:1.40
FROM rust:latest as builder
LABEL MAINTAINER="pbackz pierre.baconnier@outlook.fr"
LABEL REPOSITORY="https://github.com/pbackz/dockerfiles"

ENV APP="rustapp"
RUN USER=root cargo new --bin ${APP}
WORKDIR .
COPY . .
RUN rustup toolchain install nightly && \
    rustup override set nightly && \
    cargo build --release && \
    cargo install --path .

FROM debian:buster-slim
ENV USER=app_rust
ENV TZ="Europe/Paris"
ENV APP_WD="/opt/rustapp"

RUN apt-get update && \
    apt-get install -y ca-certificates tzdata jq bash build-essential && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    cp /usr/share/zoneinfo/Europe/Paris /etc/localtime && \
    groupadd $USER && \
    useradd -g ${USER} ${USER} && \
    mkdir -p ${APP_WD} && \-
    chown -R ${USER}:${USER} ${APP_WD}
    
COPY --from=builder /usr/local/cargo/bin/${APP} /usr/local/bin/${APP}

USER ${USER}
WORKDIR ${APP_WD}

CMD ["rustapp"]