On each switch: 

- tell the chassis one ae interface exists (device-count 1)
  - `configure`
  - `set chassis aggregated-devices ethernet device-count 1` 

- join both members with ether-options 802.3ad ae0 (a wildcard range covers both at once) 
  - `wildcard range set interfaces ge-0/0/[1-2] ether-options 802.3ad ae0`

- set lacp active ONCE on ae0
  - `set interfaces ae0 aggregated-ether-options lacp active`
  - `commit`
  - `commit comment "LACP redundant high-bandwidth connectivity"`
