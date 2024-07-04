https://www.youtube.com/watch?v=-gF-Jsk85bQ
https://github.com/devopsjourney1/influxdb-2-dockercompose

## Vultur setup

### Add new server from cli :   
- Create server: cloud compute - select server location - server type: Ubuntu, eg 18.04 - server size: select an IPv4 supported, eg 25 GB $5/mo 1 CPU ...
- Configure firewall: Server Settings => Firewall => Manage => Add Firewall Group => give description => Add IPv4 Rules:
  - Accept TCP influxdb port (8086)
  - Accept SSH 22
  - Go back to Firwall setting and select the created group
    
### Access and configure server:

Powershell: ssh root@ipaddress - provide password

commands:

- `sudo apt-get update -y`   
- `sudo apt install docker.io && sudo apt install docker-compose -y`
- `git clone https://github.com/devopsjourney1/influxdb-2-dockercompose.git`
- `cd influxdb-2-dockercompose/`

```yml
version: '3.3'

services:
  influxdb:
    image: influxdb:latest
    ports:
      - '8086:8086'
    volumes:
      - influxdb-storage:/var/lib/influxdb
    environment:
      - DOCKER_INFLUXDB_INIT_MODE=setup
      - DOCKER_INFLUXDB_INIT_USERNAME=admin
      - DOCKER_INFLUXDB_INIT_PASSWORD=changemeplease
      - DOCKER_INFLUXDB_INIT_ORG=my-org 
      - DOCKER_INFLUXDB_INIT_BUCKET=my-bucket

volumes:
    influxdb-storage:
```

- `docker-compose up`

### Access influxdv web ui
open browser and go to <server ip>:8086 - login with credential from env variables in docker-compose file.
