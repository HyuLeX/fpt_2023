# Docker volume

[Docker volume và cơ chế](https://blog.hien.app/tong-quan-ve-docker-volume-va-cac-loai-volume-co-san-trong-docker)

- Docker volume là cơ chế để duy trì dữ liệu được tạo bởi các docker container. Giúp tạo ra không gian lưu trữ riêng biệt để quản lý dữ liệu độc lập của container. Option `-v` được dùng để mount volume trong container
- Một số loại volume trong docker:
  1. `Bind mount`: cơ chế để chia sẻ folder trực tiếp từ host cho container, volume trong docker được ánh xạ trực tiếp tới một file/folder nằm trong host (tức file trong host được edit thì sẽ lưu thẳng lên container)

  > Dùng `docker run -v <local_dir>:<container_dir> <image_name>` để tạo container mới + ánh xạ folder container tới folder của host

  2. `Anonymous volume`: volume này được tạo ra khi run 1 container, volume này sẽ bị xóa khi container bị xóa

  > Dùng `docker run -v <container_dir> <image_name>`

  3. `Named volume`: volume được đặt tên và không bị xóa khi container bị xóa

  > `docker run -v <volume_name>:<container_dir> <image_name>`

  4. `tmpfs mount`: file temp system memory tạm thời của container được lưu trữ trong host 

VD: docker run -v pgdata:/var/lib/postgresql/data -p 8080:80 postgre

- Tạo volume riêng không attach với container nào: `docker volume create <volume_name>`
- Với để gán volume đã được tạo vào container chưa được tạo, dùng ``

# Tại sao cần docker volume
- Do container có tính stateless -> các volume đi kèm để lưu trữ dữ liệu của container (thành trạng thái stateful)
  - Các volume dễ di chuyển sang các giữa các container khác nhau dễ dàng hơn việc bind mount trực tiếp vào ở đĩa local
  - Quản lý các khói lượng trong các volume bằng CLI docker hoặc API Docker
  - Hoạt động trên cả vùng chứa linux và window
  - Các volume có thể được chia sẻ và dùng giữa các container
  - Các tập mới có thể được điền trước nội dung của chúng bằng một vùng chứa.
  - Các ổ đĩa trên Docker Desktop có hiệu suất cao hơn nhiều so với các ổ gắn kết từ máy chủ Mac và Windows.
  - Volume không làm tăng kích thước của container và volume là độc lập so với container

![](https://docs.docker.com/storage/images/types-of-mounts-volume.webp?w=450&h=300)


# Populate a volume using a container
