# What is openvswitch

![](https://www.openvswitch.org/assets/featured-image.jpg)

[What is openvswitch](https://www.openvswitch.org/)

- Open vSwitch là một switch ảo được xây dựng dưới license Apache 2.0
- Các hypervisor cần khả năng kết nối giữa các VM chúng quản lý với thế giới ngoài, chúng sẽ sử dụng cầu Linux (linux bridge) để truyền traffic, đó là lý do tại sao Open vSwitch được sử dụng

> Dùng kết hợp với các hypervisor để kết nối các VM trong cùng một host cũng như các VM ở các host khác

# Linux bridge cũng có chức năng tương tự, tại sao cần Open vSwitch

[open switch and linux bridge](https://docs.openvswitch.org/en/latest/intro/why-ovs/)

[The difference between linux bridge and Open vSwitch](https://ioflood.com/blog/linux-bridge-vs-openvswitch-how-to-improve-virtualization-network-performance/)

- Có một số trường hợp khiến cho linux bridge quá tải: 
  - Thiết lập yêu cầu kết nối mạng lớn (băng thông lớn)
  - Số lượng VM lớn

> Chúng tạo ra số lượng packet cao cũng như traffic dày đặc

- Open vSwitch không chỉ cung cấp nền tảng với hiệu suất hoạt động tốt hơn linux bridge mà còn cung cấp các tùy chọn phức tạp hơn và thích ứng với đa dạng OS và các nền tảng ảo hóa khác nhau, tăng tính ổn định cho VM

# Tạo connect giữa các netns qua Open vSwitch
1. Tạo 2 netns namespace với `sudo ip netns add <namespace>`
2. Tạo veth với `sudo ip link add <veth1> type veth peer name <veth2>` (tạo 2 peer veth cho mỗi một host khác nhau)
3. Kết nối từng đầu của veth với netns đã tạo với `sudo ip link set <veth1> netns <namespace1>` (tạo 2 cặp veth xong, cắm mỗi đầu 1 veth khác nhau cho các host ở trong đó)
4. Thêm IP và subnet mask cho veth `sudo ip netns exec <namespace1> ip addr add 10.10.10.1/24 dev <veth1>`
5. Tạo 1 vswitch với `sudo ovs-vsctl add-br <bridge name>`
6. Kết nối 2 đầu veth còn lại từ 2 host tới vswitch đã tạo `sudo ovs-vsctl add-port <bridge name> <veth name>`
7. Để trạng thái 2 đầu veth được kết nối đến switch trong state up `sudo ifconfig <veth name> up`
8. Check ping từ host này sang host kia `sudo ip netns exec <namespace> ping <IP address of other host>`

