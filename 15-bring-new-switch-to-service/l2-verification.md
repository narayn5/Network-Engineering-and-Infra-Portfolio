- Inter switch links - trunk port connection
  - `interface GigabitEthernet0/1`
  - `switchport mode trunk`
  - `switchport trunk allowed vlan 1,10,20,30`
  - `no shutdown`
  - `exit`
- STP verification
  - `sh spanning-tree`
  - `sh spanning-tree summary`
  - `sh spanning-tree vlan 1`
- Etherchannel status
  - `sh etherchannel summary`
  - `sh int port-channel 1`
- MAC address table verification
  - `sh mac address-table`
  - `sh mac address-table vlan 1`
  - `sh mac address-table dynamic`


