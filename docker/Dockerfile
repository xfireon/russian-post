FROM ubuntu:16.04

ENV ROCKSDB_LIB_DIR=/usr/lib/x86_64-linux-gnu
ENV SNAPPY_LIB_DIR=/usr/lib/x86_64-linux-gnu

RUN apt-get update \
  && apt-get install -y curl git gcc cpp \
  libssl-dev pkg-config libsodium-dev libsnappy-dev librocksdb-dev

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain=1.26.1

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash \
  && apt-get install -y nodejs

WORKDIR /usr/src
RUN git clone --branch v0.8 https://github.com/exonum/exonum.git \
  && mv /root/.cargo/bin/* /usr/bin \
  && cd exonum/examples/cryptocurrency-advanced/backend \
  && cargo update && cargo install \
  && cd ../frontend && npm install && npm run build
WORKDIR /usr/src/exonum/examples/cryptocurrency-advanced
COPY launch.sh .

ENTRYPOINT ["./launch.sh"]
