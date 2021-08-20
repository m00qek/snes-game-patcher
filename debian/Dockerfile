################################### BUILDER ####################################
FROM debian:bullseye AS builder

RUN apt-get update && apt-get install -y \
  build-essential \
  cmake \
  g++ \
  git

RUN git clone --depth=1 https://github.com/RPGHacker/asar.git

RUN cd asar \
  && cmake src \
  && make

RUN git clone --depth=1 https://github.com/Alcaro/Flips.git

RUN cd Flips \
  && ./make.sh

################################ FINAL RELEASE #################################
FROM debian:bullseye

RUN apt-get update && apt-get install -y \
  curl \
  entr \
  git \
  make \
  unzip

COPY --from=builder /Flips/flips              /usr/bin/flips
COPY --from=builder asar/asar/asar-standalone /usr/bin/asar
