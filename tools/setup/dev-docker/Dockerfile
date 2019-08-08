FROM phusion/baseimage:0.11 AS builder

RUN adduser zulipdev && usermod -aG sudo zulipdev
COPY --chown=zulipdev zulip /mnt/zulip
RUN apt-get update && install_clean sudo && \
    echo "zulipdev     ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && \
    export DOCKER=true && /sbin/setuser zulipdev /mnt/zulip/tools/provision && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /srv/* /mnt/zulip /home/zulipdev && \
    mkdir /mnt/zulip /home/zulipdev && chown zulipdev:zulipdev /mnt/zulip /home/zulipdev
CMD ["/bin/bash", "-c", "/sbin/my_init -- /sbin/setuser zulipdev bash -l"]
ENV DOCKER true
WORKDIR /mnt/zulip
VOLUME /home/zulipdev
VOLUME /srv
EXPOSE 9991