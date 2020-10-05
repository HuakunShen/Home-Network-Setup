# MotionEye

https://github.com/ccrisan/motioneye

Go to release page, https://github.com/ccrisan/motioneye/releases, download a release and burn it to your device.

## With Docker

https://github.com/ccrisan/motioneye/wiki/Install-In-Docker

```bash
docker run --name="motioneye" \
    -p 8765:8765 -p 8081:8081\
    --hostname="motioneye" \
    -v /etc/localtime:/etc/localtime:ro \
    -v /etc/motioneye:/etc/motioneye \
    -v /var/lib/motioneye:/var/lib/motioneye \
    --restart="always" \
    --detach=true \
    --device=/dev/video0 \
    ccrisan/motioneye:master-armhf
```

Add `-p 8081:8081` for streaming

Add `--device=/dev/video0` for camera

## Default Credentials

**username:** "admin"

**Password:** ""

