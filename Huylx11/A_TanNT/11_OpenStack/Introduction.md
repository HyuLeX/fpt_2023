# Openstack là gì?
- Một nền tảng open source mà sử dụng tập hợp các tài nguyên để xây dựng và quản lý private và public cloud
# Openstack components
- Nova (computer service): tạo, sửa, xóa và xử lý các lập lịch liên quan đến quản lý các tài nguyên máy tính.
- Neutron (network service): chịu quản lý tất cả các network trong openstack, service điều khiển bởi API để quản lý tất cả các network và IP address
- Swift (object storage): dịch vụ lưu trữ đối tượng, truy xuất các object phi cấu trúc với restful API
- Cinder (block storage): cung cấp block storage ổn định mà có thể truy cập bằng API (đây là self-service)
- Keystone (identity service provider): cung cấp tất cả các authentication và ủy quyền trong các openstack service, ánh xạ các service chính xác tới người dùng
- Glance (image service provider): chịu trách nhiệm đăng ký, lưu trữ và lấy virtual disk trong toàn bộ network. Các image có thể chứa rất nhiều các back end system
- Horizon (dashboard): web-based interface
- Ceilometer (telemetry): đo lường và bill các dịch vụ được sử dụng, cảnh báo khi có một ngưỡng nào đó vượt quá giới hạn cho phép
- Heat (orchestration): có khả năng tự mở rộng quy mô tài nguyên đám mây, được sử dụng phối hợp với ceilometer.

> Về cơ bản, các service sẽ quản lý storage, compute, networking, identity, etc

# Các tính năng của Openstack
- Kiến trúc theo module: cho phép user triển khai nhiều các thành phần họ cần, tùy chỉnh và mở rộng quy mô dễ dàng
- Hỗ trợ nhiều tenant: cho phép nhiều bên cùng tham gia truy cập vào cơ sở hạ tầng cloud mà vẫn duy trì tính private và bảo mật
- Openstack được điều khiển bằng API

# Openstack architecture

![](https://static.javatpoint.com/blog/images/openstack-architecture.png)

- 