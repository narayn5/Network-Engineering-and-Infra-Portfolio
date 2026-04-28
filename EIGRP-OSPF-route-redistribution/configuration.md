# Network Topology

```
R1 (OSPF) ----- R2 (EIGRP)
```



# IP Addressing Plan

R1 - R2 -> 10.0.12.0/30



Loopback for all routers - R1 1.1.1.1,  R2 2.2.2.2



# Configuration

## Interface setting

- On R1,

  - ```
    en
    conf t
    hostname R1
    
    int gi0/0
     ip add 10.0.12.1 255.255.255.252
     no sh
    
    int loopback0
     ip add 1.1.1.1 255.255.255.255
    ```

    

- On R2,

  - ```
    en
    conf t
    hostname R2
    
    int gi0/0
     ip add 10.0.12.2 255.255.255.252
     no shutdown
    
    int loopback0
     ip add 2.2.2.2 255.255.255.255
    ```
    
  
  

## Configure OSPF on R1

- On R1,

  - ```
    router ospf 1
     router-id 1.1.1.1
     network 10.0.12.0 0.0.0.3 area 0
     network 1.1.1.1 0.0.0.0 area 0
    ```
    

## Configure EIGRP on R2

- On R2,

  - ```
    router eigrp 100
     network 10.0.12.0 0.0.0.3
     network 2.2.2.2 0.0.0.0
     no auto-summary
    ```

## Redistribute Route between OSPF and EIGRP

- On R1,

  - ```
    router ospf 1
     redistribute eigrp 100 subnets
    ```

    

- On R2,

  - ```
    router eigrp 100
     redistribute ospf 1 metric 10000 100 255 1 1500
    ```

    









