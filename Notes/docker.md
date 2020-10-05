# Docker

## Install Docker

Instructions: https://docs.docker.com/engine/install/debian/ (for debian)

Follow the instructions, make sure install the right version (arm). If your OS is not 64bit, don't choose arm64.

## Install docker-compose

```bash
pip3 install docker-compose
```

## Install Portainer

Instructions: https://www.portainer.io/installation/

After installation, go to `localhost:9000` with browser, or `<ip>:9000` if you are using another computer.

If cannot access, `sudo docker container ls` to see if it's there, sudo docker container restart portainer` to restart if needed.

Create a new user and you are in.