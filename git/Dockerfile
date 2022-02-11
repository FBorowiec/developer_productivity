FROM ubuntu:focal
WORKDIR /home
ARG DEBIAN_FRONTEND=noninteractive
RUN apt update && \
    apt install -y curl git vim
CMD ["/bin/bash"]
