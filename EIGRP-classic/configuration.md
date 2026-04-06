# Network Topology



R1 ----- R2 ------- R3



# IP Addressing Plan

R1 - R2 -> 10.0.12.0/30

R2 - R3 -> 10.0.23.0/30

Loopback for all routers - R1 1.1.1.1,  R2 2.2.2.2, R3 3.3.3.3



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
    
    int gi0/1
     ip add 10.0.23.1 255.255.255.252
     no shutdown
    
    int loopback0
     ip add 2.2.2.2 255.255.255.255
    ```

    

- On R3,

  - ```
    en
    conf t
    hostname R3
    
    int gi0/0
     ip add 10.0.23.2 255.255.255.252
     no shutdown
    
    int loopback0
     ip add 3.3.3.3 255.255.255.255
    ```

    

## Configure EIGRP Classic

- On R1,

  - ```
    router eigrp 100
     network 10.0.12.0 0.0.0.3
     network 1.1.1.1 0.0.0.0
    ```

    

- On R2,

  - ```
    router eigrp 100
     network 10.0.12.0 0.0.0.3
     network 10.0.23.0 0.0.0.3
     network 2.2.2.2 0.0.0.0
    ```

    

- On R3,

  - ```
    router eigrp 100
     network 10.0.23.0 0.0.0.3
     network 3.3.3.3 0.0.0.0
    ```

    











