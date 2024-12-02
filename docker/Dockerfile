FROM ubuntu:24.04

RUN apt-get update && apt-get install -y \
    openssh-server \
    sudo \
    python3 \
    python3-pip \
    python3-venv \
    && apt-get clean && mkdir /var/run/sshd

RUN python3 -m venv /opt/venv && \
    /opt/venv/bin/pip install --upgrade pip && \
    /opt/venv/bin/pip install six

RUN echo 'root:root' | chpasswd && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config && \
    sed -i 's/#AuthorizedKeysFile     .ssh\/authorized_keys/AuthorizedKeysFile     .ssh\/authorized_keys/' /etc/ssh/sshd_config

ENV PATH="/opt/venv/bin:$PATH"

COPY ./id_ed25519.pub /root/.ssh/authorized_keys

RUN chmod 700 /root/.ssh && \
    chmod 600 /root/.ssh/authorized_keys && \
    chown -R root:root /root/.ssh

CMD ["/usr/sbin/sshd", "-D"]
