- Configure Physical Interface
  - `set interfaces ge-0/0/0 mtu 1500
    `
  - `set interfaces ge-0/0/0 description "Link to Core Router"`

- Configure Logical Unit
  - `set interfaces ge-0/0/0 unit 0 description "Primary LAN"`

- Configure IPv4
  - `set interfaces ge-0/0/0 unit 0 family inet address 192.168.1.1/24
    `
  - `set interfaces ge-0/0/1 unit 0 family inet address 10.0.1.1/24`

- Configure Descriptions
  - `set interfaces ge-0/0/0 description "WAN Link - ISP Primary"
    `
  - `set interfaces ge-0/0/1 description "LAN Interface - Branch Office"
    `
  - `set interfaces ge-0/0/2 description "Backup WAN Link"`

- Configure Loopback
  - `set interfaces lo0 unit 0 family inet address 10.255.1.1/32
    `
  - `set interfaces lo0 unit 0 description "Router ID"`

- Verify Configuration
  - `show interfaces
    `
  - `show configuration interfaces | display set`

- Commit everything
  - `commit
    `
  - `commit comment "Interface provisioning"`
