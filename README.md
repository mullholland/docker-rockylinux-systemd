Docker Rockylinux Systemd
=====================

This Dockerfile can build containers capable to use systemd.

Branches
--------

This repository has multiple tags that relate to Almalinux versions.

|Rockylinux Version|Docker image tag|
|------------------|-------------------|
|8                 |8                  |
|latest (9)        |9, latest          |

Manually starting
-----------------

```shell
docker run \
  --tty \
  --privileged \
  --volume /sys/fs/cgroup:/sys/fs/cgroup:ro \
  mullholland/docker-rockylinux-systemd
```
