
## Volumes

* Volumes có thể được gán (tạo) cho container bởi lệnh `VOLUME /path/to/container/volumes` hoặc sử dụng command line `-v volume-name:/path/to/container/volumes`.
Ví dụ: `docker container run -v mysql-db:/var/lib/mysql mysql`
* **Volumes sẽ không được xóa khi container exit.**
* List volumes: `docker volume ls`

## Bind mounting

* Mapping file hoặc directory từ *host* &rarr; *container*. Sẽ có sự đồng bộ file trong directory từ host &rarr; container.
* Không thể định nghĩa trong Dockerfile, chỉ có thể định nghĩa trong lệnh command line `docker container run -v /host/file:/container/file`

[Create and manage Volume](https://docs.docker.com/storage/volumes/#create-and-manage-volumes)