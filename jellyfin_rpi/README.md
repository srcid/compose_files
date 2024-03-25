# Jellyfin RPI

Jellyfin settinfs to be used in my raspberry pi.

## Run in Docker CLI

```shell
docker run --name jellyfin -e PUID="$(id -u)" -e GUID="$(id -g)" -e TZ="America/Sao_Paulo"  -p 8096:8096 -v jellyfin-config:/config -v jellyfin-cache:/cache -v ./media:/media:ro --restart unless-stopped --device /dev/video10 --device /dev/video11 --device /dev/video12 linuxserver/jellyfin
```

## Problems

I'm not sure if the hardware acceleration (HWA) is working.