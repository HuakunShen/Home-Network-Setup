# Remote Access

## SSH Without Password

- `sudo raspi-config`

- Interfacing Options: enable ssh

`sudo vim /etc/ssh/sshd_config`

Change port if you don't want to use default port 22 for ssh.

```
Port <Port you want>
PasswordAuthentication no
```

Restart ssh server

```bash
sudo service ssh restart
```

### Add Public Key

#### Method 1 (ssh-copy-id):

```bash
cd ~/.ssh
ssh-keygen			# default or
ssh-keygen -f pikey -t rsa -b 4096		# customize key generation
ssh-copy-id -i <filename> <user@ip> # ssh-copy-id -i id_rsa pi@192.168.1.77
ssh <user@ip>
```

#### Method 2 (Copy Public Key Manually)

- Copy the public key from host, ssh to remote machine and paste/append the content to `~/.ssh/authorized_keys`

## VNC

- `sudo raspi-config`
- Interfacing Options: enable VNC
- Boot Options: Desktop / CLI: Desktop (boot to Desktop if you want to access GUI with VNC)
- Advance Options: Resolution: choose one, I use mode 82 (1080p), otherwise VNC will not be able to display
- Download a VNC Viewer on your computer, add a connection and fill in the ip of the remote device (pi in this case) and you can access the GUI
- If you sign in to VNC on both the remote device and your computer, you will be able to access the GUI interface from external network, given that the remote device (pi) is connected to internet. You can also access it from external network with VPN.



















