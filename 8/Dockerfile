FROM rockylinux/rockylinux:8

LABEL maintainer="mullholland"
LABEL build_date="2026-11-08"

ENV container=docker

# Install systemd -- See https://hub.docker.com/r/rockylinux/rockylinux
RUN yum -y update; yum clean all; \
  # (cd /lib/systemd/system/sysinit.target.wants/; \
  # for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
  rm -f /lib/systemd/system/multi-user.target.wants/*;\
  rm -f /etc/systemd/system/*.wants/*;\
  rm -f /lib/systemd/system/local-fs.target.wants/*; \
  rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
  rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
  rm -f /lib/systemd/system/basic.target.wants/*;\
  rm -f /lib/systemd/system/anaconda.target.wants/*;

# Install requirements.
RUN yum -y install rpm dnf-plugins-core initscripts \
 && yum -y update \
 && yum -y install \
      sudo \
      which \
      hostname \
      procps-ng \
      ca-certificates \
      iproute \
      python3 \
      python3-pip \
      python3.11 \
      python3.11-pip \
 && yum clean all

# EL8's default python3 (3.6) can't run current ansible-core's AnsiballZ
# wrapper ("SyntaxError: future feature annotations is not defined").
# python3.11 is available in AppStream; switch the python3 alternative to
# it so ansible's interpreter auto-discovery picks it up without any
# per-role changes.
RUN alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 20 \
 && alternatives --set python3 /usr/bin/python3.11 \
 && python3.11 -m pip install packaging

# Disable requiretty.
RUN sed -i -e 's/^\(Defaults\s*requiretty\)/#--- \1/'  /etc/sudoers


VOLUME ["/sys/fs/cgroup"]

CMD ["/usr/sbin/init"]
