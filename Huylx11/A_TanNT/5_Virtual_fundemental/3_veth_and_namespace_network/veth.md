# veth

[What is veth?](https://www.unix.com/man-page/linux/4/veth#:~:text=Linux%202018-02-02%20veth%20%284%29%20The%20veth%20devices%20are,be%20used%20as%20standalone%20network%20devices.%20veth%20devic)

- virtual ethernet device (veth)
- veth đevice còn được gọi là virtual ethernet device.
- veth device đóng vai trò như là đường hầm (tunnel) giữa các network namespace để tạo bridge đến một thiết bị mạng vật lý trong namespace khác, hoặc đó cũng có thể được dùng như thiết bị network độc lập
- veth luôn được tạo theo cặp để kết nối với nhau

# Tạo veth pair device
- Dùng command `ip link add <p1-name> type veth peer name <p2-name>`
- Trong đó:
  - p1-name và p2-name là 2 connected end points

> Khi một packet được truyền từ device này sang device kia ngay lập tức vì đã được tạo theo pair ngay từ đầu. Việc mất kết nối 1 trong 2 end point cũng khiến link state trên pair cũng bị down.