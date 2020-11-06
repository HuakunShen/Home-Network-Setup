# Wake On Lan (WOL)

# Prerequisite

Enable **Wake On LAN** in BIOS.

On windows,

1. **Device Manager**
2. **Network adapeters**
3. Double Click your default adapter, most likely "Intel..." or "Realtek ..."
4. **Power Management**
5. **Allow this device to wake the computer**
   **Only allow a magic packet to wake the computer**

## Wireshark

Use wireshark to monitor wol packet to your network and computers, to verify that the wol packets are actually sent and received properly.

Open wireshark with `sudo` on linux, select your network adapter, in filter box at top, type in **wol** and click enter. Then only **wol** traffic will be shown.

After you send a **wol** packet with the following methods, you should see it in wireshark

## wakeonlan

Use a command line app

```bash
sudo apt install wakeonlan
wakeonlan -p 9 <mac address>
```

```bash
Usage
    wakeonlan [-h] [-v] [-i IP_address] [-p port] [-f file] [[hardware_address] ...]

Options
    -h
        this information
    -v
        displays the script version
    -i ip_address
        set the destination IP address
        default: 255.255.255.255 (the limited broadcast address)
    -p port
        set the destination port
        default: 9 (the discard port)
    -f file
        uses file as a source of hardware addresses

See also
    wakeonlan(1)
```

## Python WOL Script

```python
import socket
import time

# ip = "255.255.255.255"
# ip = "192.168.1.255"
ip = "192.168.1.xxx"
mac = "xx:xx:xx:xx:xx:xx"
port = 9

def create_magic_packet(macaddress: str):
    if len(macaddress) == 17:
        sep = macaddress[2]
        macaddress = macaddress.replace(sep, "")
    elif len(macaddress) != 12:
        raise ValueError("Incorrect MAC address format")

    print("mac: {}".format(macaddress))
    payload = "F" * 12 + macaddress * 16
    payload = bytes.fromhex(payload)
    print("payload: {}".format(payload))
    return payload


with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as sock:
    packet = create_magic_packet(mac)
    sock.setsockopt(socket.SOL_SOCKET, socket.SO_BROADCAST, 1)
    sock.sendto(packet, (ip, port))

```

## Remote WOL

### Method 1 (third party website)

Open port 9 in your virtual server/port forwarding.

https://www.depicus.com/wake-on-lan/woli

Your can also embed your info in the get request URL.

Bookmark it, then one click to open.

### Method 2 (VPN)

Connect VPN back to your home and run the script/app to wake your PC with your local network.

### Method 3 (host a server)

Host a simple server on your machine (in local network), run the wol script/app when it receive an request to wol with local network.

To make the server available to external network, open the port in your virtual server/port forwarding (in router).

You can bookmark the url too.

### Method 4 (WOL with Voice)

Use **IFTTT**, make an applet.

**IF CONDITION:** receive voice command from **Google Assistant** or **Alexa** or **Siri**

**THEN:** Use **webhook** applet in IFTTT to send a get request. The GET request can be sent with **Method 1** or **Method 3**.
