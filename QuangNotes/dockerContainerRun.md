# What happen in `docker container run`
1. Looks for that image locally in image cache, doesn't find anything
2. Looks in remote image repository (default to Docker Hub)
3. Downloads the latest by default if user don't specify which image version
4. Creates new container based on that image and prepares to start
5. Gives container a virtual IP on a private network
6. Opens port on host and forward to port in container
7. Starts container by using CMD in the image Dockerfile
