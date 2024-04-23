# NAT là gì?

[NAT là gì?](https://www.geeksforgeeks.org/network-address-translation-nat/)

- Network Address Translation (NAT) là service cho phép IP private sử dụng internet và cloud. NAT cho phép dịch từ private IP sang public IP trước khi packet được phép truyền sang các network khác và ngược lại
- NAT hoạt động trên router hoặc firewall
- Với NAT, cả hệ thống internal network chỉ cần một địa chỉ public IP đại diện để có thể kết nối internet
- `Port Address Translation (PAT)` cho phép nhiều máy chủ chia sẻ một IP duy nhất bằng cách sử dụng dịch địa chỉ IP và cổng.
- NAT giúp cho:
  - Bảo vệ IP nội bộ khỏi các nguồn tiếp cận từ internet
  - Quản lý hiệu quả địa chỉ IP (do IPv4 hạn chế)

# Tại sao NAT mask port?
- Mask port trong NAT có tác dụng tránh vấn đề: NAT khi nhận packet phản hồi về host trong internal network thì NAT không thể biết được reply này thuộc host nào, cũng như số cổng ở trên các host có thể giống nhau. Vì vậy NAT `đánh dấu số port cùng với public IP để có thể phân biệt được các private IP đang kết nối ra ngoài`

# Các loại NAT

[Sự khác nhau giữa Static NAT và dynamic NAT và overload](https://ipwithease.com/nat-types-static-dynamic-and-overload/)

1. `Static NAT (SNAT)`:
  - Một `private IP address được đăng ký với một public IP address` và `duy trì địa chỉ public IP này liên tục` do được config bằng tay cố định
  - Được sử dụng khi cần duy trì sự ổn định duy trì ra mạng bên ngoài, `có thể được dùng với web server, email server hoặc một số dịch vụ cần sử dụng với địa chỉ IP nhất định và liên tục` (nói cách khác là để cho các server dễ được tìm kiếm hơn và duy trì kết nối ổn định trong external network)
  
![](https://i1.wp.com/ipwithease.com/wp-content/uploads/2017/05/STATIC-NAT.jpg?resize=600%2C343&ssl=1)

2. `Dynamic NAT (DNAT)`:
  - Cho phép nhiều thiết bị trong mạng nội bộ sử dụng một nhóm địa chỉ IP công cộng từ một "pool" định sẵn khi chúng cố gắng truy cập mạng bên ngoài. Ví dụ: trong trường hợp có 2 public IP trong `pool` (bảng có chứa số lượng public IP nhất định), nếu đã có 2 private IP chiếm sử dụng 2 public IP trong pool mà có packet từ một host thứ 3 trong internal network, packet này sẽ bị drop (tức là host này không thể kết nối với internet cho đến khi có host nào đó ngắt kết nối và không sử dụng IP public)
  - Yêu cầu:
    - Số `IP public ít nhất bằng số lượng private IP` (tức là các private IP chỉ có thể được sử dụng số IP public nhất định trong pool)
    - `Chỉ dịch các địa chỉ IP` (không bao gồm số port)
    - Mỗi một IP private được map với một public IP trong pool `(quan hệ 1-1)`
  - Tác dụng: giới hạn số lượt truy cập đến Internet trong cùng một thời điểm

![](https://i1.wp.com/ipwithease.com/wp-content/uploads/2017/05/DYNAMIC-NAT.jpg?resize=768%2C439&ssl=1)

3. `Port address translation (PAT)`: [PAT hoạt động như thế nào?](https://study-ccna.com/port-address-translation-pat-configuration/)
  - Hay còn được gọi là `overload` - loại NAT được sử dụng phổ biến nhất
  - Có tác dụng `ánh xạ nhiều private IP thành một public IP`, đặc biệt là overload có thể `phân biệt các nguồn private IP bằng cách mask port` như hình bên dưới (vừa sử dụng tiết kiệm IP address và tránh việc NAT không phân biệt được reply thuộc về host nào)

![](https://study-ccna.com/wp-content/uploads/2018/08/pat_explanation.jpg)
