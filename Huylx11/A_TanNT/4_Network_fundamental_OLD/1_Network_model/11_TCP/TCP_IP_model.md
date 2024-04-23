# TCP/IP là gì?

[TCP/IP Explain](https://www.techtarget.com/searchnetworking/definition/TCP-IP)

[TCP/IP model vs OSI model](https://www.fortinet.com/resources/cyberglossary/tcp-ip-model-vs-osi-model)

![TCP/IP vs OSI model](https://media.geeksforgeeks.org/wp-content/uploads/20230417045622/OSI-vs-TCP-vs-Hybrid-2.webp)

- TCP/IP là mô hình sử dụng bộ các giao thức để kết nối các thiết bị thông qua internet (máy gửi request và máy gửi thông tin)
- Trong TCP/IP gồm có nhiều giao thức khác.
- TCP - Transmission control protocol:
  - Là giao thức chịu trách nhiệm truyền tải thông tin an toàn giữa các ứng dụng và đảm bảo dữ liệu được gửi/nhận đầy đủ
- IP - Internet protocol
  - Là giao thức chịu trách nhiệm đánh địa chỉ và địa tuyến các packet đến đúng địa chỉ trong network

> Điểm giống OSI và TCP/IP:

[TCP/IP vs. OSI Model: Comparative Analysis](https://www.fortinet.com/resources/cyberglossary/tcp-ip-model-vs-osi-model)

- Đều phân lớp tách bạch để xử lý dữ liệu được gửi theo các phân lớp với các nhiệm vụ khác nhau

> Điểm khác OSI và TCP/IP:

- Các layer trong TCP/IP có thể chứa nhiều chức năng của các layer trong OSI model
- Việc xử lý lỗi khi áp dụng mô hình TCP/IP sẽ kém hiệu quả hơn so với việc sử dụng mô hình OSI

Tuy nhiên, TCP/IP lại là mô hình phổ biến hơn do sự dễ hiểu, có tính thực tiễn và được áp dụng rộng rãi trong internet toàn cầu trong khi OSI lại là mô hình có tính học thuật và giải thích cách hoạt động của một mô hình nói chung rất tốt

# Các TCP/IP layer:

![TCP/IP layers](https://api.bkhost.vn/uploads/2019/12/cau-truc-cua-cac-tang-trong-mo-hinh-tcp-ip.jpg)

> 1. LINK LAYER

[Link layer](https://www.geeksforgeeks.org/tcp-ip-model/)

[Link layer pt2](http://www.codesandtutorials.com/networking/tcpipmodel/link_layer.php)

- Link layer là một layer có chức năng kết hợp của data link layer và physic layer từ OSI model (cách hoạt động giống với 2 tầng OSI L1, L2)

> 2. NETWORK/INTERNET LAYER

[Network/Internet layer](https://www.geeksforgeeks.org/tcp-ip-model/)

- Lớp này định địa chỉ của các packet và IP address
- Có một số giao thức chính trong lớp này như sau:
  - IP: giao thức internet có nhiệm vụ gán/xem các địa chỉ IP trong header packet. Có IPv4 và IPv6
  - ICMP: giao thức được sử dụng để báo lỗi và vấn đề trong truyền tải dữ liệu, một giao thức để quản lý mạng
  - IGMP: giao thức được sử dụng để liên lạc đa hướng với mạng IP để truyền data packet (được sử dụng trong truyền phát video, hội nghị)

> 3. TRANSPORT LAYER

[Transport layer](https://www.geeksforgeeks.org/tcp-ip-model/)

- Lớp này đảm bảo các dữ liệu được vận chuyển được quản lý đúng thứ tự và không bị lỗi, TCP và UDP tồn tại ở lớp này (TCP và UDP giống với lớp transport của OSI model)

> 4. APPLICATION LAYER

[Application layer](https://www.geeksforgeeks.org/tcp-ip-model/)

- Lớp ứng dụng là lớp gần với người dùng nhất (người dùng giao tiếp với một ứng dụng), cung cấp giao diện và giao thức cần thiết cho user để các hệ thống đầu - cuối giao tiếp với nhau. Để so sánh với OSI model, lớp này là sự kết hợp của session layer, presentation layer và application layer
- Use:
  - Tạo điều kiện sử dụng các dịch vụ mạng
  - Phát triển các ứng dụng trên mạng
  - Cung cấp các dịch vụ cho user như: email, transfer of file, user login
- Có một số ptotocol xuất hiện trong tầng application của TCP/IP model
    - HTTP vs HTTPS:HTTP là giao thức truyền siêu văn bản, được world wide web (tập hợp các trang web và các nguồn được liên kết với nhau thông qua internet và web browser) sử dụng để quản lý các thông tin trên web browser và server. HTTPS là giao thức HTTP kết hợp với SSL (secure socket layer), cung cấp thêm các mẫu điền trong trình duyệt, đăng nhập hoặc xác thực 
    - SSH: SSH protocol là giao thức giúp đăng nhập từ thiết bị này sang thiết bị khác từ xa với giao diện dòng lệnh
    - FTP: dựa vào mô hình client-server để truyền file trong network
    - SMTP: giao thức truyền thư điện tử một cách đơn giản hóa qua mạng
    - DNS: giao thức đặt tên các thiết bị trong các networks, có service chuyển từ domain name sang địa chỉ IP
    - Telnet: như SSH, giao thức giúp thiết lập kết nối từ xa nhưng không có mã hóa như SSH
    - SMNP: giao thức quản lý thiết bị mạng được dùng để giám sát mạng và các thiết bị liên quan. 

> Giữa TCP/IP model và OSI model trong sử dụng thực tế. Tại sao mô hình OSI cũ mà vẫn được sử dụng?

[Why OSI model still be used theseday](https://www.geeksforgeeks.org/this-is-exactly-why-we-still-use-the-osi-model-when-we-have-tcp-ip-model/)

- Trong lý thuyết OSI model thường được dùng vào lý thuyết, không được áp dụng trong thực tế. Tuy nhiên, mô hình OSI là mô hình đủ logic, dùng để tham chiếu. Breakdown các thành phần nhỏ hơn so với mô hình TCP/IP để dễ quản lý hơn -> dễ dàng quản lý bảo mật và xử lý các rủi ro kỹ thuật