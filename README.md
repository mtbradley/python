# OVPNMANAGER
### ovpnmanager.py
A terminal OpenVPN manager for IPVanish.  
Uses Python 3.6+ (built in modules only required).  
This file is compatable with Debian based systems including Ubuntu and Raspberry Pi OS.  
(Tested with Python 3.6+ on Raspberry Pi 3/4 running Raspberry Pi OS Buster). 

Also compatable with pfSense (FreeBSD) firewall.

### Features:
- Start/stop OpenVPN service
- Fetch and sort IPVanish server list
- Rank servers based on ping latency
- Select random server from top ranked list
- Updates OpenVPN configuration file
- Includes other network functions which can be customised
- Can be run via a cron job at scheduled intervals

### Prerequisites Debian OS / Raspberry Pi:  
(You need to have a working existing IPVanish OpenVPN configuration file)
1. `/etc/openvpn` default openvpn installation path
2. `/etc/openvpn/client.conf` is the default openvpn configuration file
3. A valid IPVanish username and password linked to the configuration file
4. `/etc/defaults/openvpn` contains line `AUTOSTART="client"

Example of `/etc/openvpn/client.conf` file:

```
client
dev tun
proto udp
remote sjc-a14.ipvanish.com 443
resolv-retry infinite
nobind
persist-key
persist-tun
persist-remote-ip
ca ca.ipvanish.com.crt
verify-x509-name sjc-a14.ipvanish.com name
comp-lzo
verb 3
auth SHA256
cipher AES-256-CBC
keysize 256
tls-cipher TLS-DHE-RSA-WITH-AES-256-CBC-SHA:TLS-DHE-DSS-WITH-AES-256-CBC-SHA:TLS-RSA-WITH-AES-256-CBC-SHA
auth-user-pass auth.txt
script-security 2
```

### Prerequisites pfSense
#### Note: pfSense version recommended for advanced users
Note: There are still some issues with pfSense caching last server.  
1. Recommend backup of pfSense configuration prior to using.  
2. Setup a working OpenVPN IPVanish client through the web admin interface.
3. pfSense Openvpn configuration files are located in `/var/etc/openvpn`.
4. Client files will start with client followed by a number, identify the number and edit the main() function in ovpnmanager.py
