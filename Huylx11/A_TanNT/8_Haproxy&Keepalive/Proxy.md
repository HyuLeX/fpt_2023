
# Access control list

[ACL](https://youtu.be/vMshgkItW5g?si=RgOLo0osIHTLMfUO)

- ACL là danh sách dựa trên rule được đặt ra được sử dụng bởi switch và router dùng để quản lý các traffic (lọc các traffic)

# Proxy server

[How proxy works](https://www.geeksforgeeks.org/what-is-proxy-server/)

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200714200713/How-Does-The-Proxy-Server-Operates.jpg)

- Là một hệ thống hoặc router có khả năng cung cấp gateway giữa user và internet
- Use:
  - Ngăn chặn khả năng tấn công mạng (lá chắn cho local network, hide IP)
  - Được sử dụng như là một web filter hoặc firewalls

# Proxy type
- `Reverse proxy server`: thường nằm sau một mạng riêng và chuyển các yêu cầu của client đến máy chủ thích hợp

![](https://images.viblo.asia/ef40197e-ab26-4da5-81d2-759a4508d7e3.PNG)

- `Web proxy server`: chuyển các request HTTP từ máy khách đến máy chủ, loại default thường được thấy

- Anonymous Proxy Server
- Highly Anonymity Proxy
- Transparent Proxy
- CGI Proxy
- Suffix Proxy
- Distorting Proxy
- Tor onion Proxy
- 12P anomynous Proxy
- DNS Proxy

# Cách proxy work?
- Proxy hoạt động ở giữa computer và internet (thay mặt host để giao tiếp với internet), chuyển các request từ máy khách đến máy chủ. Đối với các trang web địa chỉ đang giao tiếp với chúng chỉ là IP của proxy và IP của host đã được ẩn

> Có thể gọi là forward proxy