## Docker compose file
* An easy way to create docker contaniners, volumes and networks.

* Recommended using docker-compose file version >=2.

[Docker compose references](https://docs.docker.com/compose/compose-file/)

## Docker compose file structure
```
version: "3"
services:   #Define services, the same as running command docker container create for each service
  service_name:     #Name for each service (containers).

volumes:    #Define volumes, same as docker volume create

networks:   #Define networks, same as docker network create
```


## Use Docker compose to build
