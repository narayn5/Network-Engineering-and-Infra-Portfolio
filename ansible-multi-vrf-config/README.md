This project automates the creation and validation of multiple Virtual Routing and Forwarding (VRF) instances on Cisco IOS XR routers using ansible. It creates three isolated routing domains (Production, Management, Testing), each with dedicated loopback interfaces and IP addressing. The project shows network automation practices including infrastructure-as-code principles, idempotent configuration management, and automated validation workflows. It uses Ansible roles for modular design, YAML-based configuration definitions, and network_cli connections for reliable device communication. 

## Quick Start

### Deploy VRFs
ansible-playbook -i inventory.ini vrf-config.yml      
### Validate deployment
ansible-playbook -i inventory.ini vrf-validate.yml 