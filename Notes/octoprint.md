# Octoprint

## Regular Installation

Official Website: https://octoprint.org/

Download Image: https://octoprint.org/download/

Download the image and burn it to your sd card as an OS.

## Docker Installation

However, I want to keep my OS, thus, I will use docker.

Dockerhub: https://hub.docker.com/r/octoprint/octoprint

Github: https://github.com/OctoPrint/octoprint-docker

Sample **docker-compose.yml**: https://github.com/OctoPrint/octoprint-docker/blob/master/docker-compose.yml#L20-L32

### Docker Compose (Mine)

```yaml
version: '2.4'

services:
  octoprint:
    image: octoprint/octoprint
    restart: unless-stopped
    ports:
      - 5000:80
    devices:
      - /dev/ttyUSB0:/dev/ttyACM0
      - /dev/video0:/dev/video0
    volumes:
      - octoprint:/octoprint
    # uncomment the lines below to ensure camera streaming is enabled when
    # you add a video device
    environment:
      - ENABLE_MJPG_STREAMER=true

  ####
  # uncomment if you wish to edit the configuration files of octoprint
  # refer to docs on configuration editing for more information
  ####

  config-editor:
    image: linuxserver/code-server
    ports:
      - 8443:8443
    depends_on:
      - octoprint
    restart: unless-stopped
    environment:
      - PUID=0
      - GUID=0
      - TZ=America/Chicago
    volumes:
      - octoprint:/config

volumes:
  octoprint:
```

**Run docker-compose**

```bash
docker-compose up -d
```

