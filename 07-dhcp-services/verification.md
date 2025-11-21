- `sh ip dhcp pool` (shows the dHCP pools)
- `sh ip dhcp binding` (active dhcp leases)
- `sh ip dhcp statistics` (show stats)
- `debug ip dhcp server events` (monitor DHCP activity)
- `sh ip dhcp excluded-address` (display excluded address from that network)

On Windows,

- `ipconfig /release`
- `ipconfig /renew`

On Linux,

- `sudo dhclient -v eth0`
- `ip addr show`
