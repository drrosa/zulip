FROM phusion/baseimage:0.11 AS builder

RUN adduser zulipdev && usermod -aG sudo zulipdev
COPY --chown=zulipdev zulip /home/zulipdev/zulip
RUN apt-get update && install_clean sudo && \
    echo "zulipdev     ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && \
    export DOCKER=true && /sbin/setuser zulipdev /home/zulipdev/zulip/tools/provision && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
ENV DOCKER true
WORKDIR /home/zulipdev/zulip
CMD ["/bin/bash", "-c", "/sbin/my_init -- /sbin/setuser zulipdev bash -l"]
EXPOSE 9991