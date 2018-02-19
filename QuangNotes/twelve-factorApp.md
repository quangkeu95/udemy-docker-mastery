
# Twelve-factor introduction

The twelve-factor app là khái niệm để  xây dựng nên software-as-a-service app, với các ưu điểm:
* Sử  dụng **declarative** format, giảm thời gian và chi phí khi có người develop mới join vào project.
* Tăng tính **portability** khi triển khai application lên các môi trường triển khai khác nhau.
* Phù hợp để triển khai lên các hạ tầng cloud platforms.
* Giảm sự khác biệt giữa việc triển khai môi trường development và môi trường production.
* Dễ dàng **scale up**.

## [1. Codebase](https://12factor.net/codebase)
>**One codebase tracked in revision control, many deploys.**

Một application sẽ có một **codebase** duy nhất. Một codebase là một **code repository**, được tracked bởi version control system như Git, SVN.

Một **codebase** có thể sẽ được triển khai thành nhiều môi trường triển khai khác nhau (staging, production, local dev, ...).

## [2. Dependencies](https://12factor.net/dependencies)
>**Explicit declare and isolate dependencies.**

Application nên tự định nghĩa hoàn toàn và chính xác tất cả dependencies (**dependency declaration**). Hơn nữa cần có **dependency isolation** để tránh việc bị leak những dependencies từ môi trường bên ngoài vào hệ thống.

Ví dụ:
* Ruby sử dụng cơ chế  `Gemfile` cho dependency declaration, `bundle exec` cho dependency isolation.
* Python sử dụng `pip` cho dependency declaration, `virtualenv` cho dependency isolation.

Quy tắc này sẽ giúp cho developer mới khi join vào project để phát triển chỉ cần cài đặt language runtime và dependency manager &rarr; giảm thiểu thời gian và chi phí khi tiếp cận codebase.

## [3. Config](https://12factor.net/config)
>**Store config in environment.**

Lưu trữ config thay đổi tùy biến theo môi trường triển khai trong **environment variables**

## [4. Backing Services](https://12factor.net/backing-services)
>**Treat backing services as attached resources.**

**Backing service** là các service consume bởi application, ví dụ như databases, messaging/queueing systems, SMTP services, và caching systems.

Quy tắc này cho phép application có thể tương tác như nhau đối với **local** và **third-party** backing services mà không cần phải thay đổi source code. Hơn nữa việc attach và deattach các backing service dễ dàng hơn.

## [5. Build, release, run](https://12factor.net/build-release-run)
>**Strictly separate build and run stage.**

Quá trình triển khai application được chia ra làm 3 stages:
* **Build stage**: thực hiện convert codebase thành executable bundle được gọi là *build*.
* **Release stage**: thực hiện ghép *build* và *config* &rarr; khối *release* sẵn sàng triển khai.
* **Run stage**: thực hiện triển khai trên môi trường.

Mỗi release phải là **unique** và phải được đánh ID hoặc timestamp hoặc thứ tự tăng dần. Một release sẽ không thể được sửa đổi một khi nó đã được tạo ra, khi muốn sửa đổi, chúng ta tạo một release mới.

## [6. Processes](https://12factor.net/processes)
>**Execute the app as one or more stateless processes.**

Các application processes sẽ là **stateless** và **shared nothing**. Mọi data sẽ được lưu tại backing service, thường là database.

Về *shared-nothing architecture*:
>*Shared-nothing architecture* là kiến trúc distributed-computing, ở đó mỗi node sẽ là độc lập và không chia sẻ nhau memory hoặc disk storage. Kiến trúc này loại trừ được *single point of failure*, cung cấp khả năng *self-healing*.

## [7. Port Binding](https://12factor.net/port-binding)
>**Export services via port binding**

Web application không nên phụ thuộc vào webserver container như Tomcat, Apache. Application nên export service của mình trên một hoặc nhiều port để service khác có thể call đến.

## [8. Concurrency](https://12factor.net/concurrency)
>**Scale out via process model**

Application có thể được phân chia thành nhiều loại *processes* khác nhau để take care workload khác nhau, và các processes có khả năng span thành multiple instance running on multiple machine.

## [9. Disposability](https://12factor.net/disposability)
>**Maximize robustness with fast startup and graceful shutdown**

Application sẽ bao gồm các processes có thời gian startup càng ngắn càng tốt. Short startup time sẽ phục vụ việc fast scaling, rapid deployment.

*Graceful shutdown* là quá trình process thực thi khi nhận được SIGTERM signal. Ví dụ:
* Webapp sẽ gracefully shutdown bằng việc từ chối new request, cho phép các request hiện tại hoàn tất sau đó mói exit app.
* Worker processes sẽ gracefully shutdown bằng việc đẩy current job vào queue.

## [10. Dev/prod parity](https://12factor.net/dev-prod-parity)
>**Keep development, staging, and production as similar as possible**

Quy tắc này mong muốn môi trường dev, staging và production càng giống nhau càng tốt, cần tránh 3 sự khác biệt về:
* Khác biệt về mặt thời gian (**time gap**): Người developer phát triển hàng tháng trời sau đó mới triển khai.
* Khác biệt về mặt con người (**personel gap**): Người developer phát triển, người ops triển khai.
* Khác biệt về mặt tools (**tools gap**): Người develop sử dụng stack phát triển lại khác với stack sử dụng để triển khai.
 
Vì vậy để giảm bớt 3 sự khác biệt này, người developer sẽ vừa là người phát triển và có tham gia vào việc triển khai trên môi trường production. Hơn nữa người developer sẽ phải làm cho môi trường dev và production càng gần sát nhau càng tốt.

## [11. Logs](https://12factor.net/logs)
>**Treat logs as event streams**

Logs của application sẽ được ghi ra `stdout`. The event stream có thể được routing bởi các open-source log routers như Fluentd, Logplex

## [12. Admin processes](https://12factor.net/admin-processes) 
>**Run admin/management tasks as one-off processes** 

