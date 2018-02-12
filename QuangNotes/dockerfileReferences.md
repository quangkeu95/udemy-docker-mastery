
## WORKDIR
```
WORKDIR /path/to/workdir
```

`WORKDIR` sẽ set working directory cho bất kỳ lệnh `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, `ADD` follow sau nó.

`WORKDIR` có thể được sử dụng nhiều lần trong một Dockerfile. Nếu đường dẫn đến workdir là **relative path** thì đường dẫn này sẽ móc nối đến đường dẫn của câu lệnh `WORKDIR` trước nó. Ví dụ:
```
WORKDIR /parent
WORKDIR child1
WORKDIR child2
RUN pwd
```

Câu lệnh sẽ cho ouptut là `/parent/child/child2`.


