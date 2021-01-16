FROM ubuntu:focal

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

RUN apt-get update && \
    apt-get install --no-install-recommends -y git ash

ARG GERRIT_UID=1000
RUN adduser --system --disabled-login --uid $GERRIT_UID --ingroup users gerrit
