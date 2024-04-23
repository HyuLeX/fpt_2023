# Autonomous system là gì?
- Một mạng, nhóm mạng của tổ chức, doanh nghiệp mà tổ chức này có chính sách định tuyến riêng (routing policy)
- Các router hoạt động trong một khu vực AS như vậy giao tiếp với nhau bằng  interior gateway protocol (IGP) - thuật ngữ trong giao thức định tuyến để hạn chế trao đổi thông tin với nhau

# Phân loại các cách đo route trong mạng  

[Distance vetor and link state](https://www.geeksforgeeks.org/difference-between-distance-vector-routing-and-link-state-routing/)

![](https://media.geeksforgeeks.org/wp-content/uploads/20230501235620/intro-image.jpeg)

> 1. `Distance vector`
  - Một thuật toán định tuyến động, mỗi bộ định tuyến tính toán khoảng cách của nó đến từng láng giềng mà nó kết nối
  - Router chia sẻ kiến thức của chính nó cho các router láng giềng và việc chia sẻ này diễn ra `đều đặn` `(looping có thể xảy ra do việc truyền thông tin đều đặn - xử lý bằng splitting horizon)`
  - Sử dụng thuật toán Bellman Ford (cập nhật metric, giá trị nào nhỏ hơn thì bị thay)

> 2. `Link-state`: một thuật toán định tuyến động trong đó mỗi bộ định tuyến `chia sẻ kiến thức về các hàng xóm của nó với mọi bộ định tuyến khác trong mạng`. Một bộ định tuyến gửi thông tin về các hàng xóm của nó tới tất cả các bộ định tuyến thông qua `flooding (có thể gây ra loop - xử lý bằng TTL)`. Việc `chia sẻ thông tin chỉ diễn ra khi có sự thay đổi`.
  - `Route table`: giao thức sẽ chuyển tiếp route table trong các bảng cập nhật cho các router
  - `Topology map`: bảng này chứa thông tin liên kết trong một mạng
  - `Neighbors table`: bảng này chứa các thông tin của các router lân cận trên mỗi router
- Các bước khởi tạo diễn ra như sau:
  1. Gửi các gói hello giữa các router để "tìm hiểu" các router lân cận -> từ đó xây dựng bảng neighbor table
  2. Làm tràn thông tin ra khắp miền mạng (gửi thông tin bản cập nhật route toàn bộ miền mạng)
  3. Nhận các route từ các router khác -> để duy trì topology toàn mạng
  4. Xây dựng cây logic và lấy router hiện tại làm gốc để thực thi các thuật toán tính đường đi ngắn nhất như thuật toán Dijikstra