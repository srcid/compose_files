# Cloudflare tunnels

Cloudflare tunnels can be used to expose to the Internet especific services your run locally.

## Run using docker CLI

```shell
docker run -name cd -d --network host cloudflare/cloudflared:latest tunnel --no-autoupdate run --token ${TOKEN}
```