User cannot reach the server or another destination 

1. Ensure both the systems assigned to the same VLAN (users and destination)
   1. `sh vlan brief`
   2. `sh int gi0/5 switchport`
2. Verify if they are trunk/access
   1. `sh int gi0/5 switchport` and look for static access for administrator mode
   2. If they are trunk then change it to access:
      1. `int gi0/5`
      2. `switchport mode access`
      3. `switchport access vlan 10`
      4. `exit`
3. Check line protocol and status to be "up" and "up"
   1. `sh int gi0/5`
   2. If down and down then:
      1. `int gi0/5`
      2. `no sh`
      3. `exit`
4. Important - check the cables:
   1. Port numbers on device match with configuration
   2. Loose connections, bent pins (damaged is possible) 
   3. Ping from switch SVI
