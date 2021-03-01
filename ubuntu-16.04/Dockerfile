FROM ubuntu:16.04

RUN apt-get update \
  && apt-get install -y --no-install-recommends locales \
     python-software-properties \
     software-properties-common \
     python-cryptography \
     python-setuptools \
     python-openssl \
     python-wheel \
     wget rsyslog systemd systemd-cron sudo iproute2 python-pip\
  && rm -Rf /var/lib/apt/lists/* \
  && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
  && apt-get clean

RUN sed -i 's/^\($ModLoad imklog\)/#\1/' /etc/rsyslog.conf

# Fix potential UTF-8 errors with ansible-test.
RUN locale-gen en_US.UTF-8

RUN pip install ansible

# Install Ansible inventory file.
RUN mkdir -p /etc/ansible
RUN echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts

VOLUME ["/sys/fs/cgroup", "/tmp", "/run"]
CMD ["/lib/systemd/systemd"]
