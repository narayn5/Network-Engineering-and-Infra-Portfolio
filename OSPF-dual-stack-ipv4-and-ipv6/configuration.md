# Network Topology

```
R1 ------- R2 --------- R3
```



# IP Addressing Plan

| Device  | IPv4         | IPv6              |
| ------- | ------------ | ----------------- |
| R1 G0/0 | 10.0.12.1/30 | 2001:db8:12::1/64 |
| R2 G0/0 | 10.0.12.2/30 | 2001:db8:12::2/64 |
| R2 G0/1 | 10.0.23.1/30 | 2001:db8:23::1/64 |
| R3 G0/0 | 10.0.23.2/30 | 2001:db8:23::2/64 |
| R1 Lo0  | 1.1.1.1/32   | 2001:db8:1::1/128 |
| R2 Lo0  | 2.2.2.2/32   | 2001:db8:2::2/128 |
| R3 Lo0  | 3.3.3.3/32   | 2001:db8:3::3/128 |



# Configuration

## Enable IPv6 Routing

```
ipv6 unicast-routing
```

## Configuration

- On R1,

  - ```
    en
    conf t
    hostname R1
    
    int gi0/0
     ip add 10.0.12.1 255.255.255.252
     ipv6 address 2001:db8:12::1/64
     no sh
    
    int loopback0
     ip add 1.1.1.1 255.255.255.255
     ipv6 address 2001:db8:1::1/128
    ```

    

- On R2,

  - ```
    en
    conf t
    hostname R2
    
    int gi0/0
     ip add 10.0.12.2 255.255.255.252
     ipv6 address 2001:db8:12::2/64
     no shutdown
    
    int gi0/1
     ip add 10.0.23.1 255.255.255.252
     ipv6 address 2001:db8:23::1/64
     no shutdown
    
    int loopback0
     ip add 2.2.2.2 255.255.255.255
     ipv6 address 2001:db8:2::2/128
    ```

    

- On R3,

  - ```
    en
    conf t
    hostname R3
    
    int gi0/0
     ip add 10.0.23.2 255.255.255.252
     ipv6 address 2001:db8:23::2/64
     no shutdown
    
    int loopback0
     ip add 3.3.3.3 255.255.255.255 
     ipv6 address 2001:db8:3::3/128
    ```

    

## Configure OSPF IPv4

- On R1,

  - ```
    router ospf 1
     router-id 1.1.1.1
     network 10.0.12.0 0.0.0.3 area 0
     network 1.1.1.1 0.0.0.0 area 0
    ```

    

- On R2,

  - ```
    router ospf 1
     router-id 2.2.2.2
     network 10.0.12.0 0.0.0.3 area 0
     network 10.0.23.0 0.0.0.3 area 0
     network 2.2.2.2 0.0.0.0 area 0
    ```

    

- On R3,

  - ```
    router ospf 1
     router-id 3.3.3.3
     network 10.0.23.0 0.0.0.3 area 0
     network 3.3.3.3 0.0.0.0 area 0
    ```

    







## Configure OSPFv3 IPv6

- On R1,

  - ```
    ipv6 router ospf 1
     router-id 1.1.1.1
    
    interface G0/0
     ipv6 ospf 1 area 0
    
    interface Loopback0
     ipv6 ospf 1 area 0
    ```

    

- On R2,

  - ```
    ipv6 router ospf 1
     router-id 2.2.2.2
    
    interface G0/0
     ipv6 ospf 1 area 0
    
    interface G0/1
     ipv6 ospf 1 area 0
    
    interface Loopback0
     ipv6 ospf 1 area 0
    ```

    

- On R3,

  - ```
    ipv6 router ospf 1
     router-id 3.3.3.3
    
    interface G0/0
     ipv6 ospf 1 area 0
    
    interface Loopback0
     ipv6 ospf 1 area 0
    ```

    
