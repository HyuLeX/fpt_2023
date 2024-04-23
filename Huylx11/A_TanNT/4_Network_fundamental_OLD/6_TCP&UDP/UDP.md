# UDP là gì?

[UDP protocol](https://www.geeksforgeeks.org/user-datagram-protocol-udp/)

- UDP ngược lại so với giao thức TCP, UDP là giao thức không hướng kết nối, tức UDP không ưu tiên thiết lập kết nối ổn định trước rồi mới gửi packet như TCP
- TCP là giao thức được sử dụng đa số trên mạng nhưng ngược lại đối với các hội nghị trực tiếp, game, music streaming,... các ứng dụng liên quan đến thời gian thực này cần UDP và cho phép các packet bị loại bỏ, ưu tiên thiết lập kết nối độ trễ thấp
- Trong đó Datagram: là gói tin độc lập, chứa các thông tin từ nguồn đến đích
- UDP vừa có thể được dùng cho broadcast và multicast

# UDP header?
- Header của UDP đơn giản và cố định trong 8 byte (64 bit), trong khi đó TCP có thể trong range 20 byte - 60 byte

![](https://media.geeksforgeeks.org/wp-content/uploads/UDP-header.png)

![](https://media.geeksforgeeks.org/wp-content/uploads/20210308175958/UDP.png)

1. `Source port (16 bit)`: thông tin số cổng port đầu ra
2. `Destination port (16 bit)`: thông tin số cổng port cần đến
3. `Length (16 bit)`: chiều dài của một packet UDP, bao gồm cả UDP header và UDP data
4. `Checksum (16 bit)`:  sử dụng để kiểm tra tính toàn vẹn của gói dữ liệu (cũng giống như trong TCP). Kiểm tra checksum giúp đảm bảo rằng dữ liệu không bị thay đổi trong quá trình truyền tải. Tuy nhiên, checksum trong UDP không bắt buộc, UDP lại phụ thuộc vào 2 giao thức khác là IP và ICMP để check lỗi. Bên cạnh đó là UDP cũng dựa vào port để phân biệt các yêu cầu khác nhau.

# UDP pseudo header và TCP pseudo header (checksum activity)
- UDP pseudo header là header giả của UDP giúp những packet do UDP xác nhận đã đến chính xác đích đến (Chính xác ở đây là chính xác về số thiết bị đang giao tiếp và số port cần đến trên mỗi thiết bị)
- Pseudo header ở đây bao gồm:
  - 3 trường từ IP: protocol number, source IP và destination IP và 
  - UDP length field: Độ dài của trường UDP

> Thường, trong các packet được gửi đến thì header tầng nào được xử lý tại tầng đó. Với UDP protocol, UDP header sẽ lấy thêm 3 field từ IP để thực hiện hoạt động checksum nhằm xác minh các thông tin: data trong packet có đầy đủ hay không, packet có đến được đúng đích IP hay không?

- Bao gồm:
  - UDP chỉ bao gồm thông tin các port, nhằm xác định các đích đến của packet UDP, checksum cũng cần phải có được thông tin IP đích cho các UDP packet
  - Ở đích đến cuối cùng, UDP đánh giá checksum. Nếu checksum hợp lệ, UDP đã đến đúng cổng và địa chỉ