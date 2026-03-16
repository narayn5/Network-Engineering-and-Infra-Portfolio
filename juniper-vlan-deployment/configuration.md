- Creating VLANs
  - `set vlans Users vlan-id 10`
  - `set vlans Users description "User Data VLAN"`
  - `set vlans Voice vlan-id 20`
  - `set vlans Voice description "VoIP VLAN"`
  - `set vlans Management vlan-id 30`
  - `set vlans Management description "Management VLAN"`

- Configure Access Ports

  - `set interfaces ge-0/0/0 unit 0 family ethernet-switching vlan members Users
    `

  - `set interfaces ge-0/0/1 unit 0 family ethernet-switching vlan members Users
    `

  - `set interfaces ge-0/0/2 unit 0 family ethernet-switching vlan members Voice
    `

  - `set interfaces ge-0/0/3 unit 0 family ethernet-switching vlan members Voice
    `

  - `set interfaces ge-0/0/0 description "Access Port - User 1"
    `

  - `set interfaces ge-0/0/1 description "Access Port - User 2"
    `

  - `set interfaces ge-0/0/2 description "Access Port - Phone 1"
    `

  - `set interfaces ge-0/0/3 description "Access Port - Phone 2"`

- Configure Trunk

  - `set interfaces ge-0/0/47 unit 0 family ethernet-switching interface-mode trunk
    `

  - `set interfaces ge-0/0/47 unit 0 family ethernet-switching vlan members Users
    `

  - `set interfaces ge-0/0/47 unit 0 family ethernet-switching vlan members Voice
    `

  - `set interfaces ge-0/0/47 unit 0 family ethernet-switching vlan members Management
    `

  - `set interfaces ge-0/0/47 description "Trunk to Core Switch"`

- Configure Management Interface

  - `set interfaces vlan unit 30 family inet address 192.168.30.10/24
    `

  - `set vlans Management l3-interface vlan.30`

- Verify VLAN Membership

  - `show vlans
    `

  - `show interfaces ge-0/0/0 unit 0
    `

  - `show configuration vlans | display set`

- Commit Configuration

  - `commit
    `

  - `commit comment "Three-VLAN access switch deployment"`
