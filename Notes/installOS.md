# Install OS

The first step to do when you get a Raspberry Pi is to get a Operating System for it, otherwise it's just a useless circuit board.

## Install Raspberry Pi OS (Raspbian)

1. Go to this website https://www.raspberrypi.org/downloads/

2. Install Raspberry Pi Imager

3. Choose the default OS, sd card, click **write**

4. Configure Wifi (headless) when you don't have monitor, mouse or keyboard, if you are using ethernet cable, skip this step

    Instructions: https://www.raspberrypi.org/documentation/configuration/wireless/headless.md

    - make a file `wpa_supplicant.conf` in the boot drive (top level)

    - add the following to wpa_supplicant.conf

        ```
        ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
        update_config=1
        country=<Insert 2 letter ISO 3166-1 country code here>
        
        network={
         ssid="<Name of your wireless LAN>"
         psk="<Password for your wireless LAN>"
        }
        
        ```

        ssid is network name, psk is password

        For ssid, try to use 2.4Ghz wifi if possible as 5Ghz wifi may refuse to connect

    - Add an empty `ssh` file to allow ssh connection (top level)

5. ssh into the device

    Connect the raspberry pi to power, it should boot automatically

    If you have only 1 raspberry pi on your network, it should have a hostname of raspberry and we can `ssh pi@raspberry.local` to connect to it through ssh.

    If this is not the first pi in your network and the hostname of the other one is not changed, it's harder to find the local ip address of the new raspberry pi.

    Solution: use some ip scanning tool to scan your local network, I use `nmap`

    `nmap -sP 192.168.1.0/24`

    Your new device is probably the one with the largest ip value. You can scan before and after booting, then compare which ip is an extra one. 

    After you find the ip of the device, `ssh pi@<ip>`, and enter the default password (default=raspberry)

6. Run `passwd` to change the password



## Install Ubuntu

1. Download image from https://ubuntu.com/download/raspberry-pi, there are instructions.

2. Burn image to sd card with imager

3. Default username vs password (ubuntu: ubuntu)

4. Install Desktop after booting into the system

    ```bash
    sudo apt-get update
    sudo apt-get upgrade
    # choose one from these
    sudo apt-get install ubuntu-desktop
    sudo apt-get install xubuntu-desktop
    sudo apt-get install lubuntu-desktop
    sudo apt-get install kubuntu-desktop
    ```

    

## Install Kali

1. Official Instructions: https://www.kali.org/docs/arm/kali-linux-raspberry-pi/

    Download Image: https://www.offensive-security.com/kali-linux-arm-images/

2. Use `dd` command or imager to burn image to sd card

3. Boot