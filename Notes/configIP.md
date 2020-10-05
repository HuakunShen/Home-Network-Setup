# Configure Your IP

## Find Public IP

From any computer in your network, go to google and search for **my ip**, you will see your public ip.

Command Line Way: 

`curl -s 'https://api.ipify.org?format=json' | cut -d '"' -f 4`

## Find Private IP

`ifconfig` for linux and mac, `ipconfig` for windows.

Likely `eth0` for ethernet connection, `wlan0` for wireless connection.

Find the **inet** of them.





