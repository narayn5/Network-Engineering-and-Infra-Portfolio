- Note down the model details 
- Visit Cisco.com, support login 
- Note the filename for the model number
- Transfer the file using TFTP server:
  - In putty, `cp tftp://server-ip/imagename.bin flash:`
  - Now verify, `verify /md5 flash:imagename.bin`
- Configure the newly downloaded OS image:
  - `conf t`
  - `boot system flash:imagename.bin`
  - `exit`
  - `cp running-config startup-config`
  - `reload`
  - `sh version`

Veification:

- New IOS version
- The message, `System returned to ROM by reload`
- `config register` to be `0x2102`

- Ctrl + c to interupt during startup and use ROM monitor to manually boot or reload the image or do:
  - `boot flash:old-is.bin`
