# VPN

## Pi VPN

Official Website: https://www.pivpn.io/

Command to Install Pi VPN: `curl -L https://install.pivpn.io | bash`

1. Follow the steps to configure Pi VPN
2. Add user with `pivpn -a`
3. Transfer `.ovpn` profile file to your computer.
4. Use openvpn client to connect to vpn

## Connect

I won't talk about GUI Openvpn connection on **MacOS/Windows/IOS/Android**, simply import the file and click connect.

On linux, you have to connect with CLI.

### Setup openvpn on linux

https://community.openvpn.net/openvpn/wiki/OpenVPN3Linux

#### Install openvpn3

```bash
apt install apt-transport-https
wget https://swupdate.openvpn.net/repos/openvpn-repo-pkg-key.pub
apt-key add openvpn-repo-pkg-key.pub
wget -O /etc/apt/sources.list.d/openvpn3.list https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-$DISTRO.list
apt update
```

### Command to connect and disconnect

```bash
openvpn3 session-start --config <vpn-file.ovpn>
openvpn3 session-manage --disconnect --config <vpn-file.ovpn>
```

Handy Script if you don't want to remember the command

```bash
echo 'openvpn3 session-start $1' > convpn
echo 'openvpn3 session-manage --disconnect --config $1' > disconvpn
chmod a+x convpn
chmod a+x disconvpn
```

`mv` them to `/usr/local/bin` or anywhere of `PATH`.

To use it:

```bash
convpn <vpn-file.ovpn>				# connect with specified vpn file
disconvpn <vpn-file.ovpn>			# disconnect with specified vpn file
```

