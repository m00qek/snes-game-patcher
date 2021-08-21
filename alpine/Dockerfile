################################### BUILDER ####################################
FROM alpine:3.14.1 AS builder

RUN apk --update add --no-cache \
  cmake \
  g++ \
  git \
  libstdc++ \
  make

RUN git clone --depth=1 https://github.com/RPGHacker/asar.git

RUN cd asar \
  && cmake src \
  && make

RUN git clone --depth=1 https://github.com/Alcaro/Flips.git

RUN cd Flips \
  && ./make.sh

################################ FINAL RELEASE #################################
FROM alpine:3.14.1

RUN apk --update add --no-cache \
  curl \
  entr \
  git \
  libstdc++ \
  make \
  py3-pip \
  unzip

RUN pip install docopt requests

COPY --from=builder /Flips/flips              /usr/bin/flips
COPY --from=builder asar/asar/asar-standalone /usr/bin/asar
