# DNS là gì?
- Có tác dụng dịch các địa chỉ IP thành các tên dễ nhớ (việc nhớ các địa chỉ IP để kết nối với các trang web là rất khó nên chuyển thành các địa chỉ chữ để dễ nhớ đối với con người)

# Các terms trong DNS
1. `Domain name`: là các tên mà con người có thể đọc được, đại diện cho một nguồn trên internet, một tên miền bao gồm 3 phần:
  - http://www.example.com/
    - www là `subdomain`
    - example là `second-level domain`
    - com là `top-level domain`

2. `Top-level domain server`: là cấp cao nhất trong phân cấp hệ thống tên miền DNS. ICANN là tổ chức chịu trách nhiệm quản lý việc cấp phát TLD

3. `Recursive Resolver`: đây là các DNS server được các ISP hoặc nhà cung cấp dịch vụ DNS vận hành. Họ chịu trách nhiệm nhận các truy vấn từ client và thực hiện các truy vấn này trên authoritative name servers

4. `Authoritative name servers`: các DNS server chứa các DNS record cho những domain riêng biệt

5. `Root Name Servers`: Ở đầu hệ thống phân cấp DNS là 13 root name server được duy trì bởi nhiều tổ chức khác nhau trên toàn thế giới. Các máy chủ này chứa thông tin về TLD và cung cấp các con trỏ quan trọng tới máy chủ định danh có thẩm quyền cho mỗi TLD.

6. `Caching DNS Servers`: Bộ nhớ đệm DNS server tạm thời lưu trữ các bản ghi DNS mà đã tra cứu gần đây. Khi người dùng truy vấn một domain, các máy chủ này sẽ kiểm tra bộ nhớ đệm trước khi truy vấn các máy chủ DNS có thẩm quyền, điều này giúp giảm tải truy vấn DNS

7. `Forwading DNS Servers`: các DNS server chuyển các truy vấn cho các DNS server khác

8. `Load Balancing DNS Servers`: các server này phân phối các queries DNS trên nhiều địa chỉ IP hoặc nhiều phiên bản server để cân bằng traffic load

# Toàn bộ process cách DNS hoạt động
- `Web server` (là các máy tính được sử dụng để lưu trữ các tệp HTTP tạo ra một trang web) `sử dụng các IP address` để lấy định danh khi lưu trữ các thông tin của các trang web. Và `DNS tham gia để dịch các IP address thành những cái tên dễ nhớ` đối với con người.

![](https://media.geeksforgeeks.org/wp-content/uploads/20230921115433/dns-image-(1).png)

> Các quá trình DNS tham gia trong việc search web:
  1. Khi mới tìm kiếm tên một trang web, máy tính tìm kiếm `Caching DNS Servers` trước xem có `IP address` của trang web này được tìm kiếm trước đó hay không (giảm tải truy vấn không cần thiết qua những DNS server)

  2. Nếu không có, máy tính sẽ `gửi một query tới DNS recursive resolver` để tìm kiếm địa chỉ IP cho trang web đó. Tại đây, `DNS resolver sẽ tiếp tục tìm kiếm trong cache của nó` xem có IP address của trang web đó không.

  3. Nếu không có, `DNS resolver sẽ truyền request này đến Root Name Servers để truy vấn các TLD` (nếu như trang web đang tìm kiếm có dạng example.com thì sau khi truy vấn, `root sẽ cung cấp bạn TLD server cho .com`)

  4. Sau đó, `TLD server nhận query`, nhưng `TLD không biết địa chỉ IP cần tìm`, nhưng `TLD biết vị trí mà .com extension (tên miền mở rộng) của trang web cần tìm ở Authoritative name servers (ANS) nào`. `TLD sau đó sẽ gửi query đến cho chính xác ANS đó`. 

  5. Khi đã tìm được IP address ở các ANS, `DNS resolver gửi lại kết quả về cho client`. Máy tính hiện tại đã có thể kết nối trực tiếp đến một trang web mà người dùng muốn

> Lưu ý: 
  - chỉ DNS resolver thực hiện query tới các root name server, TLD server và Authoritative name servers
  - có thể setting DNS resolver tại chính máy tính cá nhân

# Lab creating DNS server

> Tại sao cần tạo DNS server? : để giảm sự phụ thuộc vào các cơ sở hạ tầng khác đồng thời tăng tốc độ phản hồi của mạng

> Trước khi setting DNS server: 
- `Primary server`: DNS resolver chính mà request trỏ tới đầu tiên trước khi sang secondary server
- `Secondary server`: DNS resolver phụ được sử dụng khi primary server gặp vấn đề
- `Caching server`: DNS server lưu trữ các kết quả truy vấn trước đó để phục vụ giải quyết các request của người dùng nhanh hơn

## Set DNS server trên local network (máy ảo ubuntu)

[Setting DNS server trên local network với Dnsmasq trên Linux](https://www.howtogeek.com/devops/how-to-run-your-own-dns-server-on-your-local-network/)

- dnsmasq là một máy chủ DNS nhẹ có hầu hết trong các distro của linux


