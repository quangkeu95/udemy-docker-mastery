

## FROM

> `FROM <image>:[<tag>] [AS <name>]`

Câu lệnh `FROM` set base image cho các lệnh phía sau, vì thế một Dockerfile hợp lệ sẽ bắt đầu với lệnh `FROM`

* Có thể sử dụng nhiều lệnh `FROM` trong một Dockerfile để build multiple image hoặc sử dụng build stage này là dependencies cho build stage khác. 
* Khi chạy nhiều build stage, các stage bắt đầu với lệnh `FROM` có thể được gán tên với `AS <name>`.
* Option `<tag>` sẽ mặc định là `lastest` nếu người dùng không specify.

### `ARG` and `FROM`

`ARG` có thể sử dụng trong câu lệnh `FROM` khi `ARG` đứng trước lệnh `FROM` đầu tiên.

```
ARG IMAGE_VERSION=latest
FROM node:${IMAGE_VERSION}
```

Câu lệnh `ARG` đứng trước lệnh `FROM` đầu tiên sẽ không có giá trị trong build stage (sau `FROM`)

## RUN



## WORKDIR

> `WORKDIR /path/to/workdir`

`WORKDIR` sẽ set working directory cho bất kỳ lệnh `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, `ADD` follow sau nó.

`WORKDIR` có thể được sử dụng nhiều lần trong một Dockerfile. Nếu đường dẫn đến workdir là **relative path** thì đường dẫn này sẽ móc nối đến đường dẫn của câu lệnh `WORKDIR` trước nó. Ví dụ:
```
WORKDIR /parent
WORKDIR child1
WORKDIR child2
RUN pwd
```

Câu lệnh sẽ cho ouptut là `/parent/child/child2`.

`WORKDIR` có thể sử dụng cùng với environment variables được set sử dụng `ENV`

## ARG

