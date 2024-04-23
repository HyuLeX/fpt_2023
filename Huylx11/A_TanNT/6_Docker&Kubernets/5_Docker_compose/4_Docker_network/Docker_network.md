# Docker network la gi

![](https://media.geeksforgeeks.org/wp-content/uploads/20230426184651/microsoft-azure-load-balancing.webp)

- Docker network giúp tạo mạng lưới container được quản lý bởi master node

> Note

- Nếu trên cùng một host thì các container không cần port để giao tiếp

# Giúp
- Các docker chia sẻ được các packet cho nhau

# Command

> 1 số note:
> - bridge: Nếu build container không cụ thể driver gì, bridge sẽ được tạo và kết nối với interface của host (default)
> - host: Container không chứa bất kỳ IP gì, sẽ được tạo trực tiếp trong network system tránh tạo ngăn cách giữa host và container
> - none: IP không được gán vào container, không được truy cập từ bên ngoài hoặc từ một container khác
> - overlay: được enable khi kết nối nhiều docker daemon và khiến nhiều docker swarm service giao tiếp được với nhau
> - ipvlan: sử dụng ipvlan driver và control được cả ipv4 và ipv6
> - macvlan: gán MAC vào container

![](https://media.geeksforgeeks.org/wp-content/uploads/20230419172809/Docker-network-1.webp)

- Check các docker network: `docker network ls`
- Tạo docker network: `sudo docker network create --driver <driver_name> <bridge_name>`

# Thuchanh docker network

[Link doc thuc hanh](https://github.com/JoinGame-A36664/docker-docs/blob/master/docs/docker-coban/docker-network.md)

[Vid](https://youtu.be/IBZp5NhwKlM?si=_19_7gsvi_IWeH37)

> 1. bật 2 container và ping: tự động tạo bridge và kết nối được ngay 2 container với nhau thông qua bridge

> 2. bật 2 container mở thông port HTTP để truyền packet giữa 2 container
- Xóa 1 trong 2 container đã chọn: `docker -rm <name_container>`
- Tạo lại container và expose port cho container còn lại nhìn thấy để chuyển file: `docker run -it --name B1 -p 5001:80 busybox`
- cd vào /var/www: `cd /var/www`
- Bật http: `httpd`
- Tạo file trong container này: `vi index.html`
- Kết nối với IP container kia để lấy file: `wget -o - <IP_other_container>` (dùng docker network inspect bridge để theo dõi các container trong window powershell)
- sử dụng `ls` để kiểm tra file vừa tải về từ container B1

> 3. sử dụng HTTP port để truyền file cho host (kết nối host với container)
...

