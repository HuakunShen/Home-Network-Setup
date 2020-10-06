# Use raspberry pi camera

**Official Documentation:** https://www.raspberrypi.org/documentation/usage/camera/raspicam/

## Take picture

### bash

```bash
raspistill -o cam.jpg
raspistill -vf -hf -o cam2.jpg      # with hroizontal & vertical flip
```

See the documentation for more details.
https://www.raspberrypi.org/documentation/usage/camera/raspicam/raspistill.md

### python

```python
#!/usr/bin/python
import argparse
from picamera import PiCamera
from time import sleep

parser = argparse.ArgumentParser("preview parser")
parser.add_argument("-n", "--num", type=int, default=0,
                    help="number of second to sleep")
parser.add_argument("-o", "--out", default="image.jpg",
                    help="output filename")
parser.add_argument("-q", "--quiet", action='store_true', help="")
args = parser.parse_args()

camera = PiCamera()
camera.vflip = True
if not args.quiet:
    camera.start_preview()
sleep(args.num)
camera.capture(args.out)
if not args.quiet:
    camera.stop_preview()
```

## Record Video

### Bash

```bash
raspivid -o vid.h264
raspivid -o video.h264 -t 10000         # specify length of video
```

For more info and more video format, https://www.raspberrypi.org/documentation/usage/camera/raspicam/raspivid.md

### Python

```python
#!/usr/bin/python

import argparse
from picamera import PiCamera
from time import sleep

parser = argparse.ArgumentParser("preview parser")
parser.add_argument("-n", "--num", type=int, default=5,
                    help="number of seconds to record")
parser.add_argument("-o", "--out", default="video.h264",
                    help="output filename")
parser.add_argument("--width", type=int, default=1920,
                    help="video width")
parser.add_argument("--height", type=int, default=1080,
                    help="video height")
parser.add_argument("-r", "--rate", type=int, default=30,
                    help="frame rate")
parser.add_argument("-q", "--quiet", action='store_true', help="")
args = parser.parse_args()


camera = PiCamera()
camera.vflip = True
camera.resolution = (args.width, args.height)
# camera.framerate = args.rate
if not args.quiet:
    camera.start_preview()
camera.start_recording(args.out)
sleep(args.num)
camera.stop_recording()
if not args.quiet:
    camera.stop_preview()

```
