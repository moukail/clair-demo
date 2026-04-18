Podman
======
```bash
podman compose up -d --build
```

Clair
=====
```bash
curl -L https://github.com/quay/clair/releases/download/v4.9.0/clairctl-linux-386 -o clairctl
chmod +x clairctl
sudo mv clairctl /usr/local/bin/

clairctl report docker.io/library/nginx:1.29.5-alpine3.23
```
