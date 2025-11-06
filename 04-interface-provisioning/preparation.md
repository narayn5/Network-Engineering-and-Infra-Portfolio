**Branch Router Interface Configuration Guide**

- WAN uses ISP-provided public IP 
- LAN uses private RFC1918 address
- Configure interface description, IPv4 addresses and subnet masks
  - `conf t`
  - `int gi0/0`
  - `ip address 203.0.113.50 255.255.255.0`
  - `desc WAN to ISP`
  - `ing gi0/1`
  - `ip address 192.168.10.1 255.255.255.0`
  - `desc LAN to Branch Network`
  - `exit`

### ISP Specific Configurations

- Configure Speed and Duplex: default set to auto-negotiate, explicitly setting this for reliability. (Gi's auto-negotiate automatically)
  - `int gi0/0`
  - `speed 100`
  - `duplex full`
  - `exit`
- Up the port
  - `int gi0/0`
  - `no sh`
  - `exit`
- Configure Loopback for identification (they never go down)
  - `int loopback0`
  - `desc device-identification`
  - `ip add 10.0.0.1 255.255.255.255`
  - `no sh`
  - `exit`
- Configure MTU (standard ethernet MTU is 1500 bytes, PPPoE is 1492 bytes). Check ISP requirements
  - `int gi0/0`
  - `mtu 1500`
  - `exit`
- Enable DHCP Relay to internal DHCP server 
  - `int gi0/0`
  - `ip helper-address 10.0.0.50`
  - `exit`
- Set bandwidth for routing metrics
  - `int range gi0/0-1`
  - `bandwidth 100000`
  - `exit`

- Calculate interface statistics
  - `int range gi0/0-1`
  - `load-interval 300`
  - `exit`

Loopback /32 addresses never go down; good for BGP, OSPF Router ID, management access, or monitoring.
