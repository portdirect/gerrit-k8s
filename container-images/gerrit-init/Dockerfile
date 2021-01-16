FROM gerrit-base:latest

USER root

COPY dependencies/* /var/tools/
WORKDIR /var/tools

RUN apt-get update && \
    apt-get install --no-install-recommends -y python3 python3-pip && \
    pip3 install --no-cache --upgrade pip setuptools wheel pipenv && \
    pipenv install --python 3.7.3 --system

COPY tools /var/tools/
COPY config/* /var/config/

USER gerrit

ENTRYPOINT ["python3", "/var/tools/gerrit-initializer"]
CMD ["-s", "/var/gerrit", "-c", "/var/config/default.config.yaml", "init"]
