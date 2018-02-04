# Docker networking basics

## Default networking
* All containers attach to default virtual network `bridge` aka `docker0`.
* All containers in the same virtual network can talk to each other without publish port.
* All containers can access internet which traffics route via NAT firewall on host machine.
* Remember command `docker container run -p <host-port>:<container-port>` to publish container port outside of the host.

## Docker network CLI management
* Show all networks: `docker network ls`.
* Inspect specific network: `docker network inspect`.
* Create a new network: `docker network create --driver`, default driver is `bridge`.
* Dynamically create a NIC in a container on an existing virtual network (or attach a container to an existing virtual network): `docker network connect`
* Deattach a container from an virtual network: `docker network disconnect`
* When run a container, you can specify which network to attach container by using `--net <network_name>`.

## Docker network DNS
* Docker daemon has a built-in DNS server that containers use by default.
* Default `bridge` network **does not have a DNS server inside**.
* Containers can communicate via container's name in custom virtual network.

