# Libvirt là gì?

![](https://hhb584520.github.io/kvm_blog/files/virt_others/libvirt.png)

[what is libvirt?](https://wiki.archlinux.org/title/Libvirt)

[libvirt - more detail and succinct](https://www.sobyte.net/post/2022-05/libvirt/)

- là bộ công cụ dược dùng để quản lý các nền tảng ảo hóa, bao gồm cả quản lý các máy ảo. libvirt sau đó đóng vai trò là cầu nối giữa VMM và các chức năng cấp cao, nhận yêu cầu của người dùng và sau đó gọi giao diện do VMM cung cấp để thực hiện công việc cuối cùng. Các trình ảo hóa được libvirt quản lý là KVM/QEMU, Xen, LXC, OpenVZ, VirtualBox

- Libvirt cung cấp:
  - API mã nguồn mở ổn định và thống nhất
  - libvirtd (libvirt daemon)
  - virsh tool - công cụ quản lý VM và các lưu trữ ảo hóa khác
  etc

# Tại sao lại cần libvirt
- Hypervisor như qemu-kvm có nhiều tham số cho các công cụ quản lý máy ảo dòng lệnh và rất khó sử dụng.
- Có nhiều loại Hypervisor khác nhau và không có giao diện lập trình thống nhất để quản lý chúng
- Tạo sự thông nhất khi quản lý các object liên quan đến VM

# Một số các chức năng của libvirt
- Quản lý VM: Các hoạt động của máy ảo như start, stop, pause, save, restore, và migrate. Các hoạt động tương tác khác cho nhiều loại thiết bị bao gồm disk và network interfaces, memory, and CPUs.

- Hỗ trợ máy từ xa: Tất cả chức năng libvirt đều có thể truy cập được trên bất kỳ máy nào chạy trình nền libvirt, bao gồm cả các máy từ xa. Nhiều phương tiện truyền tải mạng được hỗ trợ để kết nối từ xa chẳng hạn như SSH.

- Quản lý lưu trữ: bất cứ host nào chạy libvirt daemon đều có thể đưuọc quản lý đa dạng các loại storage: tạo file image với format đa dạng, tạo volume, partition trên raw disk, etc

- Quản lý các network interface: có thể quản lý các network interface vật lý và logic, tạo các kết nối, tạo vlan, etc

- Quản lý các virtual NAT và route

_**Một số lưu ý trong libvirt**_
- Thay vì gọi 1 máy ảo là VM hay guest, trong libvirt máy ảo sẽ được gọi là 1 domain

# Libvirt daemon là gì?

[About libvirt daemon](https://libvirt.org/daemons.html#id2)

- Daemon là một chương trình chạy một service gì đó trong background => libvirtd là một chương trình giúp chạy ảo hóa trong background
