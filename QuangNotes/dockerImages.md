## Docker Images

Each Docker Image was built by stacking different Image Layers, each Image Layer represents an instructions in Image's dockerfile.

When we create a new container, a **writable layer** is placed on top of underlying layers. We can call this layers is **Container Layer**.
All changes made in container (such as writing to files, modifing files or delete files) are written to this Container Layer.

[Multiple writable layers sharing the same read-only layers](https://docs.docker.com/storage/storagedriver/images/container-layers.jpg)


When you run the command below, you will see the **SIZE** column, which contains:
* The one *outside* the brankets is `size`: The amount of data (on disk) is used for **Container Layer**.
* The one *inside* the brankets if `virtual size`: The amount of data is used for **Read-only Layer** + `size`. So if two containers base on the same image, they share the same read-only data.

```
# docker ps -s
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES                   SIZE
3f5f33281a85        postgres            "docker-entrypoint..."   15 minutes ago      Up 15 minutes       5432/tcp            djangopostgresql_db_1   63B (virtual 287MB)
```
Docker Images are stored at `/var/lib/docker/<storage-driver>/`

## The Copy-on-write strategy 
If a file or directory exists in a lower layer within the image, and another layer (including the writable layer) needs read access to it, it just use the existing file. The first time another layer needs to modify the file (when building the image or running the container), the file is copied into that layer and modified. This minimize I/O and the size of each of the subsequent layers.

**Benefits**:
* Reduces Images size.
* Reduces container start-up time.

## Docker volumes and storage driver

A data volume is:
* A directory or a file on Docker's host file system that is mounted directly into Docker containers.
* Not managed by storage driver.
* Not deleted after container exits. 

