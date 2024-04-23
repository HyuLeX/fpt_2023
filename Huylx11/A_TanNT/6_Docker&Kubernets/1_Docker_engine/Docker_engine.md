# Docker?

[A friendly guide of docker](https://www.freecodecamp.org/news/a-beginner-friendly-introduction-to-containers-vms-and-docker-79a9e3e119b/)

- Docker là một công cụ để chạy các ứng dụng bên trong các thùng chứa (container), có thể có nhiều container trong cùng một docker, cũng như việc máy ảo có thẻ có nhiều VM do cùng hypervisor quản lý
- Docker là software nguồn mở dựa trên container của linux. `Docker sử dụng các feature của kernel` như namespace và điều khiển group để tạo container trên một hệ điều hành
- `Container package` bao gồm tất cả các dependencies và code của app để chạy trong một tệp duy nhất.
- Docker có cách quản lý hoạt động tương tự VM
- `Mỗi một container được coi là một image`

![](https://static1.howtogeekimages.com/wordpress/wp-content/uploads/csit/2019/06/bc4f8762.png?q=50&fit=crop&w=750&dpr=1.5)

# Tại sao cần Docker?
- Giảm rủi ro trong quá trình thử nghiệm app (có thể ảnh hưởng đến cả việc config lên máy)
- Quản lý việc deploy các app

# Container
- Không như VM được quản lý bởi , các container cung cấp ảo hóa cấp độ OS bằng cách sử dụng các `user space`. `Điểm khác biệt lớn nhất giữa VM và container là các container share kernel giữa các container khác`

![](https://cdn-media-1.freecodecamp.org/images/1*V5N9gJdnToIrgAgVJTtl_w.png)

# Docker engine

![](https://cdn-media-1.freecodecamp.org/images/1*K7p9dzD9zHuKEMgAcbSLPQ.png)

- Docker engine là một layer mà docker chạy trên đó., đóng vai như là ứng dụng client-server. Docker engine bao gồm:
  - `Docker daemon` chạy trong máy host, execute command như running, building, distributing container
  - `docker client` giúp chạy command để tuong tác với docker daemon
  - `REST API` giúp tương tác với docker daemon từ xa
- Trong đó `docker file` giúp user viết các instruction để build docker image



