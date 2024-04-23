# DCHP là gì?

[DHCP là gì?](https://www.geeksforgeeks.org/dynamic-host-configuration-protocol-dhcp/)

- DHCP là viết tắt của Dynamic Host Configuration Protocol. Đây là tính năng quan trọng mà người dùng mạng doanh nghiệp giao tiếp. DHCP giúp quản lý phân bổ IP qua việc cung cấp các:
  - Option 1: Subnet Mask (255.255.255.0)
  - Option 3: Router Address - gateway (ví dụ 192.168.1.1)
  - Option 6: DNS Address - địa chỉ DNS server (ví dụ 8.8.8.8)
  - Option 43: Vendor Class Identifier
  và một số option khác trong packet của DHCP

- DHCP hoạt động dựa trên client-server model và dựa trên discover, offer, request và ACK
- Nếu thời gian cho mượn, hay còn gọi lại `lease time` hết thì DHCP sẽ cung cấp lại cho máy tính này một địa chỉ khác từ DHCP server (tức là địa chỉ này không hoàn toàn thuộc về một thiết bị)
- Port DHCP hoạt động:
  - Client: 68
  - Server: 67

# Tại sao cần DHCP?
- DHCP dùng trong một mạng doanh nghiệp lớn, tránh việc các IP address giữa các máy không bị do có quá nhiều máy và không thể sử dụng cách thủ công để gán IP cho các máy
dưới 

# Các component trong DHCP
- `DHCP server`: DHCP Server về cơ bản là một máy chủ chứa Địa chỉ IP và các thông tin khác liên quan đến cấu hình.
- `DHCP client`: thiết bị nhận thông tin cấu hình từ máy chủ
- `DHCP Relay`: là kênh liên lạc giữa DHCP client và DHCP server
- `IP Address Pool`: Đây là nhóm hoặc vùng chứa các Địa chỉ IP do Máy chủ DHCP sở hữu, dùng để phân bổ địa chỉ cho các thiết bị yêu cầu IP trong network
- `Subnet`: mạng con
- `Lease`: thời gian thiết bị được sử dụng IP address đó, hết thời gian thì IP từ thiết bị đó cần phải được trả về IP address pool
- `DNS Servers`: cung cấp thông tin máy chủ DNS để resolve domain thành IP
- `Default Gateway`: gửi các packet ra ngoài local network
- `Option`: các thông tin tùy chọn bổ sung mà DHCP có thể cung cấp
- `Renewal`: gia hạn thêm thời gian sử dụng IP address
- `Failover`: khi có nhiều DHCP server nhằm đảm bảo cho thiết bị luôn có IP khi có một DHCP server gặp lỗi
- `Dynamic Updates`: DHCP server cũng có thể được cấu hình để cập nhật động các bản ghi DNS với địa chỉ IP của máy khách DHCP
- `Audit Logging`: ghi log của DHCP server

# Cách DHCP hoạt động

> Lưu ý: mọi hoạt động xảy ra giữa DHCP client và DHCP server đều được gửi dưới dạng broadcast

1. STEP 1 - Gửi DHCP discover: Các `PC được chạy DHCP client` có thể bắt đầu `hỏi về địa chỉ IP từ DHCP server` để được cung cấp IP (DHCP có thể nằm ở bất cứ đâu trên network - router, switch, máy chủ window,etc)
2. STEP 2 - gửi DHCP offer:  Một `host cần địa chỉ IP sẽ gửi thông báo broadcast trên toàn mạng để tìm DHCP server`, nếu không phải DHCP server, thông báo này sẽ bị drop
3. STEP 3 - trả về theo offer: `DHCP server gửi lại offer cùng với địa chỉ IP đã được lựa chọn` (trong trường hợp có nhiều DHCP server trong cùng một network, sẽ có nhiều offer được gửi về cùng một máy, máy nhận được IP của DHCP server nào trước thì sẽ sử dụng và drop offer còn lại của DHCP server kia)
4. STEP 4 - gửi request từ host: `host gửi về cho DHCP server một request để báo rằng sẽ lấy địa chỉ IP đó`
5. STEP 5 - gửi DHCP acknowledgement: `DCHP server gửi IP cùng với các thông tin khác như subnet mask, DNS address, gateway, etc về cho host`