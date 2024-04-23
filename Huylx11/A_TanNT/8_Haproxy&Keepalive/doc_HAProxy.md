# HAProxy?

[HAProxy và load balancing](https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts)

- High availability proxy, một phần mềm open source TCP/HTTP load balancer và là một proxy solution được sử dụng trên các hđh Linux
- Được sử dụng để tăng hiệu suất và tính tin cậy đối với nhiều server bằng cách phân chia workload

## No balance

![](https://assets.digitalocean.com/articles/HAProxy/web_server.png)

> Nếu không có load balancing, khi web server sập thì client không còn khả năng tiếp cận trang web nữa. 1 trường hợp nữa nếu có quá nhiều truy cập ko có load balance thì sẽ gâu tắc nghẽn và khiến trải nghiệm người dùng kém hiệu quả

> Load balancing là thuật toán cân bằng tải
> Load balancer là tool hoặc phần mềm giúp thực hiện cân bẳng tải

## Layer 4 Load Balancing

[Layer 4 load balance](https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts#layer-4-load-balancing)

- load balance được thực hiện ở layer 4 transport (dựa trên các thông tin được cung cấp ở tầng 4 - IP và Port)
- Nhẹ hơn
- Nhiều server cùng tồn tại nhưng không active cùng 1 lúc, đòi hỏi các server phải cung cấp nội dung giống hệt nhau và cùng kết nối với 1 DB

## Layer 7 Load Balancing

[layer 7 load balance](https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts#layer-7-load-balancing)

- Load balance được thực hiện ở tầng 7 - tầng application (load balancer còn xem xét thêm cả nội dung của packet để đưa ra quyết định cân bằng tải phù hợp)
- Nặng hơn
- Backend có thể được chia thành nhiều server backend, dựa trên thông tin request mà client gửi đến mà lựa chọn server phù hợp để điều packet đến server đó

![](https://assets.digitalocean.com/articles/HAProxy/layer_7_load_balancing.png)

## một số load balance algorithm
- round robin (Static): thuật toán default, gửi các request đến lần lượt mỗi server kiểu xoay vòng
- sticky round robin (static): thuật toán round robin mở rộng, gửi request của cùng một người để có relate data ở cùng 1 server
- weighted round robin (static): dựa trên tải của packet, các server sẽ chịu trách nhiệm nhận các request theo weight mà admin đã set
- IP/URL Hash (static) - sử dụng IP hash để đảm bảo một client luôn gửi request đến cùng server
- Least connections (dynamic): dựa trên số liệu request các server đang nhận được mà load balancer sẽ gửi request đến server đang có ít connection nhất
- Least time (dynamic): server nào có độ trễ thấp nhất thì request sẽ được phân phối đến đó

# ARCHITECTURE

- Front end - config bất cứu thứ gì trước HAproxy (có thể có nhiều front end)
  - Timeout client - thời gian client tự ngắt sau thời gian ilde
  - Bind - IP và port được chỉ định để kết nối với với server tới db
  - ACL - chỉ định các traffic nào được phép dc di chuyển qua HA proxy cùng với các quyền của nó khi mà nó đi qua

- Backend - config những thứ nằm sau HAproxy (có thể có nhiều backend)
  - Timeout connect - thời gian kết nối đến HAproxy
  - Timeout server - thời gian kết nối từ HAproxy đến server
  - loại thuật toán cân bằng tải được sử dụng

```
- front end có thể được bind vào 1 hoặc nhiều port
- một front end được kết nối với 1 back end

    eg:
    Frontend-http - binds 80 (forward to http backend)
    Frontend-https - binds 443

```
# HAproxy mode (TCP and HTTP)
- Tùy vào mode TCP hay HTTP được chọn mà HAproxy có thể hoạt động ở tầng
  - tầng 4 - TCP
  - tầng 7 - HTTP

# ACL - Access Control List
- Điều kiện được áp dụng để route traffic
- Áp dụng cho cả front end và back end