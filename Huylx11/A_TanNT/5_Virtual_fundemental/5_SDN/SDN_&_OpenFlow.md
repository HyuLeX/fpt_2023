# What is SDN

[SDN là gì?](https://www.geeksforgeeks.org/software-defined-networking/)

[SDN là gì #2](https://www.howtoforge.com/tutorial/software-defined-networking-sdn-architecture-and-role-of-openflow/)

- SDN (Software defined network) là một phương pháp tiếp cận kiến trúc mạng. `Nó cho phép kiểm soát và quản lý mạng bằng các ứng dụng phần mềm`. Thông qua SDN, toàn bộ mạng và các thiết bị mạng được kiểm soát tập trung thông qua các ứng dụng API mở. SDN hỗ trợ tạo mạng ảo hoặc hỗ trợ điều khiển mạng truyền thống với sự trợ giúp của phần mềm [Xem thêm](https://www.geeksforgeeks.org/difference-between-software-defined-network-and-traditional-network/)
- Trong SDN có
  - `Data plane`: tất cả các hoạt động liên quan cũng như thông tin, kết quả từ các packet gửi bởi những người dùng cuối ở các host đều nằm tại đây (tóm lại là lưu data)
    - Chuyển tiếp các packet
    - Phân đoạn và tập hợp các packet
    - Sao chép các gói cho multicast
  - `Control plane`: tất cả các hoạt động cần thiết để thực hiện các hoạt động trên data  (chứa các action để thao tác với các data trên data plane - nói cách khác là bộ não của network)
    - Tạo routing table
    - Thiết lập các policy để xử lý các packet
- SDN hoạt động trong `Switch`

![](https://media.geeksforgeeks.org/wp-content/uploads/20230405132159/Software-Defined-Networking.png)

- Các thành phần trong SDN:
  - `SDN application`: chuyển tiếp các yêu cầu mạng qua SDN controller
  - `SDN controller`: thu thập thông tin mạng từ phần cứng và gửi thông tin đến các ứng dụng
  - `SDN networking device`: giúp chuyển tiếp và xử lý dữ liệu

# Why SDN important?
1. Giúp chia sẻ các packet nhanh hơn
2. Deploy các ứng dụng tốt hơn
3. Giúp bảo mật tốt hơn
- Các DN dùng để triển khai ứng dụng nhanh và hiệu quả hơn, giảm chi phí

# Architecture và cách hoạt động
- Trong truyền thống, `mỗi switch đều có data plane và control plane`. Các control plane trong các switch trao đổi các thông tin liên quan đến topology và xây dựng bảng routing. Trong phương pháp sử dụng SDN, `control plane được lấy khỏi switch và được đặt trong một unit trung tâm là SDN controller`. Việc này giúp các admin xử lý các traffic thông qua console tập trung mà không cần phải động đến chỉnh sửa từng switch. 
- `Data plane vẫn còn trong switch`, và data plane sẽ chọn forward activity dựa chọn số liệu đầu vào trên flow table, bảng được pre-assigned bởi controller
- Các packet đi vào được so sánh khớp với các thông tin trong flow table, các packet ra/vào được gán/gỡ các header... _Nếu các thông tin trong packet không tương xứng với thông tin trong flow table, switch sẽ gửi query lại cho controller hoặc loại bỏ packet đó_
- Control plane nằm ở giữa và 2 đầu để giao tiếp với layer trên và dưới bằng: `Northbound` (giao tiếp bằng REST API) và `Southbound` (thông qua các giao thức như Openflow, netconf...)

- SDN architecture gồm 3 phần:
  - `Application layer`: chứa các ứng dụng network intrusion detection (phát hiện xâm nhập), firewall và load balancing (cân bằng)
  - `Control layer`: chứa `SDN controller` được coi như là network brain. 
    - Trong SDN controller chứa: Topology service, Inventory service, Statistic service, Host tracking (các service hỗ trợ điều khiển)
  - `Infrastructure layer`: chứa các switch vật lý, nơi hình thành các data plane và di chuyển các data packet

  ![](![Alt text](image.png))

_Coi Control layer là trung tâm, việc giao tiếp với Application layer được gọi là north-bound API và south-bound API đối với Infrastrucutre layer_

![](https://media.geeksforgeeks.org/wp-content/uploads/20230330153804/archi.jpg)

# Sự khác nhau giữa traditional network và SDN
- Nhìn chung:
  - cả SDN và traditional network đều hướng tới kết nối mạng các thiết bị với nhau
  - Dùng các giao thức tiêu chuẩn như TCP/IP để giao tiếp

[difference between SDN & traditional network](https://www.geeksforgeeks.org/difference-between-software-defined-network-and-traditional-network/)

| nd | SDN | Mạng truyền thống |
|:---------|:--------:|:---------:|
| Cách quản lý     | Quản lý tập trung   | Quản lý riêng lẻ   |
| Data plane và control plane phân phối trong network như nào     | đưa về dùng 1 control plane và mỗi switch chỉ đóng vai trò là data plane (do phần mềm tách)  | mỗi switch chứa 1 control plane và data plane riêng |
| Khả năng mở rộng network     | Dễ mở rộng   | Khó  |
| Mạng | Được dùng trong mạng ảo (cả mạng vật lý)  | Được dùng trong mạng thông thường  |

Ngoài ra còn có các yếu tố khác giúp SDN có ưu điểm: chi phí, khả năng mở rộng, tính dễ config, dễ lập trình theo hướng mong muốn, dễ trace các lỗi trong network

# Các model SDN
- Có một vài model được sử dụng trong SDN:
  - `Open SDN`: sử dụng OpenFlow switch. Một cách triển khai SDN đơn giản. Trong mô hình này, controller giao tiếp tới các switch bằng south-bound API với sự trợ giúp của protocol OpenFlow
  - `SDN via APIs`: giao tiếp trong SDN via APIs sử dụng các phương pháp giao tiếp bằng SNMP, CLI hoặc modern API như REST API
  - `SDN via Hypervisor-based overlay network`: trong model này, cấu hình của các thiết bị vật lý không thay đổi. Thay vào đó, các mạng lớp phủ dựa trên Hypervisor được tạo qua mạng vật lý. Chỉ các thiết bị ở rìa mạng vật lý mới được kết nối với mạng ảo hóa, do đó che giấu thông tin của các thiết bị khác trong mạng vật lý.
  - `Hybrid SDN`: sự kết hợp giữa SDN và traditional network

![](https://media.geeksforgeeks.org/wp-content/uploads/20230330131800/open-sdn.jpg)

![](https://media.geeksforgeeks.org/wp-content/uploads/20230330131927/sdn-supervisor.jpg)

# What is openflow

[Open flow là gì?](https://www.techtarget.com/whatis/definition/OpenFlow)

- Open Networking Foundation (ONF) - một tổ chức chuyên quảng bá và áp dụng SDN định nghĩa OpenFlow là giao diện truyền thông hướng nam tiêu chuẩn đầu tiên giữa lớp điều khiển và lớp chuyển tiếp trong kiến trúc SDN và chuẩn hóa OpenFlow.
- Là một tiêu chuẩn mở được cung cấp bỏi các nhà cung cấp khác nhau, là giao thức điều khiển SDN (software defined networking). Nó tách `(control plance và forward)` 
- Để điều khiển các bộ chuyển mạch mạng, bộ điều khiển SDN controller sẽ đẩy các quy tắc vào các bộ chuyển mạch để chúng có thể đưa ra quyết định khi lưu lượng truy cập mạng đến chúng. Các action đó có thể là loại bỏ gói, chuyển tiếp gói đó ra một cổng khác, flood the packet hoặc gửi gói đến bộ điều khiển để kiểm tra thêm. Switch cần duy trì các quy tắc như vậy trong bảng Openflow. Theo Openflow, các quy tắc như vậy được gọi là `'flow'` và chúng được lưu trữ trong `'flow table'`.

- Các trường của flow mang theo:
  - Match field: xác định các packet khớp dựa trên header khi đi qua các tầng
  - Actions: các action thực hiện với packet khi đã thỏa mãn được các header (chuyển, sửa packet, etc)
  - Counters: đếm số pacet phù hợp với flow

![](https://download.huawei.com/mdl/image/download?uuid=427b16bacba749febcbb53acc8bc8a0a)

- Openflow hoạt động trên giao thức TCP (6633 đối với OF ver 1.0 và 6653 đối với ver 1.3)
- Kênh OF được hình thành sau khi TCP bắt tay 3 bước thành công
  1. Switch gửi gói HELLO đến controller để bắt đầu hình thành kênh OF
  2. Switch gửi packet "feature request" thông báo đến switch phiên bản OF mà nó hỗ trợ 

# Tạo SDN với Promox hypervisor bare metal