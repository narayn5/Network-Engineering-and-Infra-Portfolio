 # Network Topology

R1 ------ R2 ------ R3 ------- R4

R1 -------- R2 -------- R5

R1 --------- R3 -------- R5

# IP Addressing Plan

1 to 2 - 10.0.12.0/30

2 to 3 - 10.0.23.0/30

3 to 4 - 10.0.34.0/30

2 to 5 - 10.0.25.0/30

3 to 5 - 10.0.35.0/30

Loopback0 for ALL 1.1.1.1 to 5.5.5.5

All are in same autonomous system # 65000

# Configuration

## Configure interfaces 

- On R1,

  - ```
    en
    conf t
    hostname R1
    
    int gi0/0
     ip add 10.0.12.1 255.255.255.252
     bandwidth 100000
     no sh
    exit
    
    int Loopback0
     ip add 1.1.1.1 255.255.255.255
    exit
    ```

- On R2,

  - ```
    en
    conf t
    hostname R2
    
    int gi1
     ip add 10.0.12.2 255.255.255.252
     bandwidth 100000
     no sh
    
    int gi2
     ip add 10.0.23.1 255.255.255.252
     bandwidth 50000
     no sh
    
    
    int gi3
     ip add 10.0.25.1 255.255.255.252
     bandwidth 100000
     no sh
    
    
    int Loopback0
     ip add 2.2.2.2 255.255.255.255
    exit
    ```

- On R3,

  - ```
    en
    conf t
    hostname R3
    
    int gi1
     ip add 10.0.23.2 255.255.255.252
     bandwidth 50000
     no sh
    exit
    
    int gi2
     ip add 10.0.34.1 255.255.255.252
     bandwidth 100000
     no sh
    exit
    
    int gi3
     ip add 10.0.35.1 255.255.255.252
     bandwidth 100000
     no sh
    exit
    
    int Loopback0
     ip add 3.3.3.3 255.255.255.255
    exit
    
    
    ```

- On R4,

  - ```
    en
    conf t
    hostname R4
    
    int G1
     ip add 10.0.34.2 255.255.255.252
     bandwidth 100000
     no sh
    exit
    
    int Loopback0
     ip add 4.4.4.4 255.255.255.255
    exit
    ```

- On R5,

  - ```
    en
    conf t
    hostname R5
    
    int g1
     ip add 10.0.25.2 255.255.255.252
     bandwidth 100000
     no shutdown
    exit
    
    int g2
     ip add 10.0.35.2 255.255.255.252
     bandwidth 100000
     no shutdown
    exit
    
    int Loopback0
     ip add 5.5.5.5 255.255.255.255
    exit
    ```

## Configure routing protocols

- On R1,

  - ```
    router ospf 1
     network 0.0.0.0 255.255.255.255 area 0
     mpls traffic-eng area 0
    exit
    ```

- On R2,

  - ```
    router ospf 1
     network 0.0.0.0 255.255.255.255 area 0
     mpls traffic-eng area 0
    exit
    ```

- On R3,

  - ```
    router ospf 1
     network 0.0.0.0 255.255.255.255 area 0
     mpls traffic-eng area 0
    exit
    ```

- On R4,

  - ```
    router ospf 1
     network 0.0.0.0 255.255.255.255 area 0
     mpls traffic-eng area 0
    exit
    ```

- On R5,

  - ```
    router ospf 1
     network 0.0.0.0 255.255.255.255 area 0
     mpls traffic-eng area 0
    exit
    ```

## Configure MPLS Tunnels 

- On R1,

  - ```
    int Tunnel0
     ip unnumbered Loopback0
     tunnel mode mpls traffic-eng
     tunnel destination 4.4.4.4
     tunnel mpls traffic-eng bandwidth 30
     tunnel mpls traffic-eng priority 0 0
     tunnel mpls traffic-eng path-option 1 explicit name PRIMARY
     tunnel mpls traffic-eng fast-reroute node-protect 
     no sh
    exit
    
    ip explicit-path name PRIMARY enable
     next-address 2.2.2.2
     next-address 3.3.3.3
     next-address 4.4.4.4
    exit
    
    mpls traffic-eng tunnels
    exit
    
    int g1
    mpls traffic-eng tunnels
     ip rsvp bandwidth 100000 100000
    exit
    ```

- On R2,

  - ```
    mpls traffic-eng tunnels
    
    int g1
     mpls traffic-eng tunnels
     ip rsvp bandwidth 100000 100000
    exit
    
    int g2
    mpls traffic-eng tunnels
    ip rsvp bandwidth 50000 50000
    exit
    
    int g3
    mpls traffic-eng tunnels
     ip rsvp bandwidth 100000 100000
    exit
    ```

- On R3,

  - ```
    mpls traffic-eng tunnels
    
    int g1
    mpls traffic-eng tunnels
    ip rsvp bandwidth 50000 50000
    exit
    
    int g2
    mpls traffic-eng tunnels
     ip rsvp bandwidth 100000 100000
    exit
    
    int g3
    mpls traffic-eng tunnels
     ip rsvp bandwidth 100000 100000
    exit
    ```

- On R4,

  - ```
    mpls traffic-eng tunnels
    
    int g1
    mpls traffic-eng tunnels
     ip rsvp bandwidth 100000 100000
    exit
    ```

- On R5,

  - ```
    mpls traffic-eng tunnels
    
    int g1
    mpls traffic-eng tunnels
     ip rsvp bandwidth 100000 100000
    exit
    
    int g2
    mpls traffic-eng tunnels
     ip rsvp bandwidth 100000 100000
    exit
    ```







