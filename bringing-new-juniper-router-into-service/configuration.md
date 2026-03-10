Connect via serial cable to console port (typically RJ-45). Use terminal emulator at 9600 baud, 8 data bits, 1 stop bit, no parity.

- Identify Hardware 
  - `request system information`

- Junos Version 
  - `show version`

- Storage 
  - `request system storage`

- Existing Configuration 
  - `show configuration`
  - `show configuration | display set`

- Backup Configuration 
  - `request system configuration rescue save `
  - `file copy /config/juniper.conf.gz /var/tmp/juniper.conf.backup.gz`

- Load Junos Image - copy image via SFTP/FTP to /var/tmp, then: 
  - `request system software add /var/tmp/junos-image-name.tgz reboot`

- Software Upgrade 
  - `request system software add /var/tmp/junos-image-name.tgz `
  - `request system reboot`

- Configure Hostname 
  - `set system host-name branch-router-01`

- Root Authentication 
  - `set system root-authentication encrypted-password` (will prompt for new password)

- Local User 
  - `set system login user branch-admin class super-user authentication encrypted-password` (prompts for password twice)

- Management Interface 
  - `set interfaces ge-0/0/0 unit 0 family inet address 192.168.1.1/24`

- SSH 
  - `set system services ssh`

- NTP 
  - `set system ntp server 8.8.8.8`
  - `set system ntp server 1.1.1.1`

- DNS 
  - `set system name-server 8.8.8.8`
  - `set system name-server 1.1.1.1`

- Syslog 
  - `set system syslog host 192.168.1.100 facility local0`
  - `set system syslog file messages facility any severity notice`
  - `set system syslog file security facility auth severity warning`

- Commit Configuration 
  - `commit`
  - `commit and-quit`
