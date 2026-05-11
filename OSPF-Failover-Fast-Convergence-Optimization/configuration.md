# OSPF Failover and Fast Convergence

- Topology

  - R1 -> R2
  - R1 -> R3
  - R2 -> R4
  - R3 -> R4

- Interface addressing 

  - On Router 1,

    - ```
      enable 
      configure terminal 
      
      int g0/0
      ip add 10.0.12.1 255.255.255.252 
      no sh 
      exit 
      
      int g0/1
      ip add 10.0.13.1 255.255.255.252 
      no sh 
      exit 
      
      int loopback0 
      ip ad 192.168.1.1 255.255.255.255 
      exit
      ```

  - On Router 2,

    - ```
      enable 
      configure terminal 
      
      int g0/0
      ip add 10.0.12.2 255.255.255.252 
      no sh 
      exit 
      
      int g0/1
      ip add 10.0.24.1 255.255.255.252 
      no sh 
      exit 
      ```

  - On Router 3,

    - ```
      enable 
      configure terminal 
      
      int g0/0
      ip add 10.0.13.2 255.255.255.252 
      no sh 
      exit 
      
      int g0/1
      ip add 10.0.34.1 255.255.255.252 
      no sh 
      exit 
      ```

  - On Router 4,

    - ```
      enable 
      configure terminal 
      
      int g0/0
      ip add 10.0.24.2 255.255.255.252 
      no sh 
      exit 
      
      int g0/1
      ip add 10.0.34.2 255.255.255.252 
      no sh 
      exit 
      
      int loopback0 
      ip ad 192.168.4.1 255.255.255.255 
      exit
      ```

      

- Ping directly connected neighbors

  - From R1, ping R3 and R2
  - From R2, ping R1 and R4
  - ...and so on

- Configure OSPF

  - Instead of specifying networks and wildcard masks, we will choose each interface and enable ospf 

    - ```
      router ospf 1
       router-id 1.1.1.1
       exit
      
      int gi0/0
       ip ospf 1 area 0
       exit
      
      int gi0/1
       ip ospf 1 area 0
       exit
      
      int loopback0
       ip ospf 1 area 0
       exit
      
      end
      ```

    - ```
      router ospf 1
       router-id 2.2.2.2
       exit
      
      int gi0/0
       ip ospf 1 area 0
       exit
      
      int gi0/1
       ip ospf 1 area 0
       exit
       
      end
      ```

    - ```
      router ospf 1
       router-id 3.3.3.3
       exit
      
      int gi0/0
       ip ospf 1 area 0
       exit
      
      int gi0/1
       ip ospf 1 area 0
       exit
      
      end
      ```

    - ```
      router ospf 1
       router-id 4.4.4.4
       exit
      
      int gi0/0
       ip ospf 1 area 0
       exit
      
      int gi0/1
       ip ospf 1 area 0
       exit
      
      int loopback0
       ip ospf 1 area 0
       exit
      
      end
      ```

- Verify neighbors/routes

  - `sh ip route ospf`

- OSPF cost manipulation

  - On R1 and R4 the core routers, manipulate cost so packets route through R2 more than R3

  - On R1,

    - ```
      conf t 
      
      int gi0/0 
      ip ospf cost 10 
      exit 
      
      int gi0/1 
      ip ospf cost 100 
      exit 
      
      ```

  On R4,

  - ```
    conf t 
    
    int gi0/0 
    ip ospf cost 10 
    exit 
    
    int gi0/1 
    ip ospf cost 100 
    exit 
    
    ```

  

