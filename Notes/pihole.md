# Pihole

**Official Website:** https://pi-hole.net/

## Regular Installation

**Instructions:** https://github.com/pi-hole/pi-hole/#one-step-automated-install

`curl -sSL https://install.pi-hole.net | bash`

## Installation With Docker

Instructions: https://hub.docker.com/r/pihole/pihole

```yaml
version: "3"

# More info at https://github.com/pi-hole/docker-pi-hole/ and https://docs.pi-hole.net/
services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "67:67/udp"
      - "80:80/tcp"
      - "443:443/tcp"
    environment:
      TZ: 'America/Toronto'
      # WEBPASSWORD: 'set a secure password here or it will be random'
    # Volumes store your data between container upgrades
    volumes:
      - './etc-pihole/:/etc/pihole/'
      - './etc-dnsmasq.d/:/etc/dnsmasq.d/'
    # Recommended but not required (DHCP needs NET_ADMIN)
    #   https://github.com/pi-hole/docker-pi-hole#note-on-capabilities
    cap_add:
      - NET_ADMIN
    restart: unless-stopped

```

Set environment variable **WEBPASSWORD**, default random password, can be found with

`docker logs pihole | grep random`

## Reset Password

```bash
docker exec pihole pihole -a -p <new password>
```

