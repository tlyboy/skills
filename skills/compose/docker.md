# Install Docker Engine on Ubuntu

Install from Docker's apt repository. Run as root, or prefix each command with `sudo`.

## Add the Repository

Pick one mirror:

| Mirror                  | `DOCKER_MIRROR`                               |
| ----------------------- | --------------------------------------------- |
| Docker official         | `https://download.docker.com`                 |
| Alibaba Cloud public    | `https://mirrors.aliyun.com/docker-ce`        |
| Alibaba Cloud ECS (VPC) | `http://mirrors.cloud.aliyuncs.com/docker-ce` |

```sh
DOCKER_MIRROR=https://download.docker.com

apt update
apt install -y ca-certificates curl
install -m 0755 -d /etc/apt/keyrings
curl -fsSL "$DOCKER_MIRROR/linux/ubuntu/gpg" -o /etc/apt/keyrings/docker.asc
chmod a+r /etc/apt/keyrings/docker.asc

tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: $DOCKER_MIRROR/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF
apt update
```

If `get.docker.com` was run on this machine before, it left `/etc/apt/sources.list.d/docker.list` pointing at the same repository; remove it to avoid duplicate-source warnings.

## Install the Packages

```sh
apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Upgrade later with `apt upgrade`.

## Proxy for Pulling Images

Image pulls are made by `dockerd`, not the shell, so shell proxy variables do not apply. On Docker Engine 23.0+, set the proxy in `/etc/docker/daemon.json`:

```json
{
  "proxies": {
    "http-proxy": "http://127.0.0.1:7890",
    "https-proxy": "http://127.0.0.1:7890",
    "no-proxy": "localhost,127.0.0.1,.local"
  }
}
```

Then `systemctl restart docker`. This only covers the daemon: pass proxies to containers with `-e HTTP_PROXY=...` and to builds with `--build-arg HTTP_PROXY=...`, never through `ENV` in a Dockerfile. Proxy URLs may carry credentials; do not commit them.
