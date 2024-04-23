# Cloud computing

[Cloud computing là gì?](https://www.techtarget.com/searchcloudcomputing/definition/cloud-computing)

- Một thuật ngữ chung cho mọi thứ liên quan đến `việc cung cấp các dịch vụ được lưu trữ qua internet`. Các dịch vụ này được chia thành ba loại hoặc loại điện toán đám mây chính: cơ sở hạ tầng dưới dạng dịch vụ `(IaaS)`, nền tảng dưới dạng dịch vụ `(PaaS)` và phần mềm dưới dạng dịch vụ `(SaaS)`. 

- Cloud computing hoạt động bằng cách cho phép các thiết bị khách truy cập dữ liệu và ứng dụng đám mây qua internet từ các máy chủ, cơ sở dữ liệu và máy tính vật lý từ xa.
- Cloud computing hoạt động phụ thuộc chủ yếu vào virtualization

- IaaS: dịch vụ cung cấp các thành phần hạ tầng: web server (AWS), storage
- PaaS: dịch vụ cung cấp các công cụ phát triển trên hạ tầng của nhà cung cấp
- SaaS: dịch vụ cung cấp các ứng dụng, phần mềm qua Internet: microsoft 365, google drive

# Virtualization là gì?

[Công nghệ ảo hóa](https://thuanbui.me/hypervisor-hyper-v-kvm-vmware-vsphere-xen/)

[Virtualization](https://www.dnsstuff.com/what-is-vm-virtual-machine)

- Virtualization là tiến trình tạo ra một phiên bản ảo từ tài nguyên của máy chủ vật lý.

- Virtual machine là một máy tính ảo (Virtual machine) với các bộ riêng biệt: CPU, RAM, network interface, storage - tồn tại bên trong một `máy tính vật lý (bare metal)`
<!-- - Có 2 loại virtualization đang phổ biến hiện nay là:
  - `Full virtualization`
  - `OS-level virtualization` -->

- Các loại virtualization:
  - `Full virtualization`: trong đó OS-guest không biết rằng nó đang ở trong môi trường ảo hóa và do đó phần cứng được hệ điều hành chủ ảo hóa để khách có thể ra lệnh trực tiếp đến phần cứng thực (hay còn gọi là `bare-metal`) - hay có thể nói host tạo ra các phần cứng ảo để cho các máy ảo hoạt động dựa trên đó (Hardware Assisted Virtualization)

  - `Para virtualization`: ảo hóa trong đó hệ điều hành khách (hệ điều hành đang được ảo hóa) nhận thức được rằng nó là khách và do đó có các trình điều khiển, thay vì ra lệnh phần cứng, chỉ cần ra lệnh trực tiếp đến hệ điều hành chủ.

| Full virtualization | Paravirtualization |
| -------- | -------- |
| less secure | more secure |
| Dùng binary translation (nhìn chung là các mã chạy bên trong các máy ảo để giúp cho máy ảo có thể chạy trên phần cứng) và direct approach | Sử dụng các hypercalls, dùng để liên lạc với hypervisor để cung cấp các dịch vụ cụ thể |
| Ảo hóa full chậm hơn so với ảo hóa para | nhanh hơn |
| Dễ dàng chuyển dịch và tương thích hơn | ngược lại |
|

- Trên khía cạnh ứng dụng thì có những loại ảo hóa sau:
  - Application Virtualization
  - Network Virtualization
  - Desktop Virtualization
  - Storage Virtualization
  - Server Virtualization
  - Data virtualization

## Tại sao lại dùng virtual machine?
- Dùng hardware hiệu quả do có thể đặt nhiều máy chủ ảo trên một máy chủ vật lý
- Tránh việc tiêu tốn tài nguyên vào việc chi tiêu nâng cấp các phần cứng không cần thiết
- Sử dụng các phần mềm chỉ tương thích với 1 số HĐH nhất định
- Clone system sang 1 máy khác (restore data and system state), backup khẩn cấp khi có hệ thống gặp lỗi

> Yêu cầu không gian vật lý và nguồn chi tiêu có hạn nên virtual machine như là những không gian ảo thay thế cho không gian vật lý để phục vụ cho doanh nghiệp tổ chức vận hành hợp lý

> Vì vậy nhìn chung `máy ảo có thể phục tạo các thành phần ảo như là không gian lưu trữ (storage), mạng (network) hay máy chủ (server)`

---
---

# Hypervisor là gì?

[Sự khác biệt giữa 2 hypervisor](https://phoenixnap.com/kb/what-is-hypervisor-type-1-2)

[Hypervisor](https://www.redhat.com/en/topics/virtualization/what-is-a-hypervisor)

- Hypervisor là `phần mềm tạo, chạy và quản lý tài nguyên các máy ảo (VM)` và đôi khi còn được gọi là `Virtual machine monitor (VMM)`. Hypervisor cô lập giữa các máy ảo với nhau. Đặc điểm lớn nhất của các hypervisor là khả năng hoạt động mà không cần đến những hardware đặc biệt
- Máy tính vật lý mà cung cấp các tài nguyên phần cứng cho máy ảo hoạt động là `host`, còn các máy ảo thì là `guest`

- Có 2 loại hypervisor:
  - `Type 1`: được gọi là `native hypervisor hoặc bare metal hypervisor`, `chạy trực tiếp trên phần cứng của host` để quản lý các OS trong các guest (không cần OS của host)
    - Hyper-V (Microsoft)
    - KVM (Red Hat) - phổ biến nhất
    - Xen (Linux Foundation)
    - vSphere (VMware)
    etc
  
  ![](https://phoenixnap.com/kb/wp-content/uploads/2022/09/type-1-hypervisor-diagram-update.png)

  - `Type 2`: là `hosted hypervisor` và được chạy trên hệ điều hành thông thường dưới dạng lớp phần mềm hoặc ứng dụng (tức các máy ảo sẽ dưới sự quản lý của các hypervisor dưới sự quản lý của OS) - loại 2 này thường được người dùng sử dụng trên máy tính cá nhân
    - Windows virtual PC 
    etc

  ![](https://phoenixnap.com/kb/wp-content/uploads/2022/09/type-2-hypervisor-diagram-update.png)


# 1. Full Virtualization là gì?

- Full Virtualization giúp tạo ra các máy chủ ảo hoạt động với tài nguyên vật lý độc lập. Các máy ảo cùng chia sẻ tài nguyên phần cứng của máy chủ vật lý và được quản lý bởi lớp ảo hoá trung gian – được gọi là `Hypervisor`.

# 2. OS-level Virtualization là gì?

[OS-level virtualization](https://thuanbui.me/ao-hoa-he-dieu-hanh-lxc-vs-docker/)

![](https://www.serverwatch.com/wp-content/uploads/2021/07/SW.TypesofServerVirtualization-1068x779.png)

- là phương pháp ảo hoá được thực hiện trực tiếp trên nền hệ điều hành được cài đặt trên máy chủ vật lý. Công nghệ này tận dụng tính năng phân chia không gian người dùng `(user space) trong nhân của hệ điều hành`, tạo ra các hệ điều hành ảo riêng biệt.
- Các phần tử ảo được tạo ra được gọi là `container` hoặc `instance` nhằm phân biệt với virtual machine trong full virtualization
- Một số OS-level virtualization phổ biến là `Docker`, LXC, Rocket

# 3. Paravirtualization là gì?
- Paravirtualization cũng sử dụng hypervisor, nhưng các máy chủ ảo không mô phỏng hoàn toàn phần cứng của máy chủ vật lý. Thay vào đó, một API thường được tích hợp vào các máy chủ hiện đại – trao đổi trực tiếp các cuộc gọi đến hệ điều hành máy chủ và máy chủ ảo. Các máy chủ ảo kết quả nhận ra môi trường của chúng như một phần mở rộng tài nguyên của máy chủ và các máy chủ ảo lân cận.

# 4. Hybrid virtualization là gì?
- Kết hợp giữa full và para

# Disk image
- Disk image là một loại tệp là bản sao chính xác của một đĩa nhất định (có thể coi ISO image là một bản sao copy hoàn chỉnh mọi thức được lưu trữ trên đĩa CD, DVD hoặc blu-ray và các hệ thống tập tin)
  - là image ảo của một loại đĩa quang (optical disk)
  - ISO là một loại format phổ biến

# Image, backup và snapshot

## Image

[image trong VM](https://azure.microsoft.com/en-in/resources/cloud-computing-dictionary/what-is-a-virtual-machine/)

- Với docker, image Là gói executable chứa mọi thứ cần để chạy 1 ứng dụng [Docker image](https://www.geeksforgeeks.org/what-is-docker-images/)
- Với VM:
  - image là tệp chứa bản sao HDH disk, đi kèm với cả các dữ liệu đi kèm trong disk đó => image được dùng để tạo các VM giống hệt với VM gốc (bao gồm cả phần mềm và cấu hình)

## Snapshot

[Snapshot là gì?](https://www.oracle.com/webfolder/technetwork/data-quality/edqhelp/Content/concepts/snapshots.htm)

[Snapshot là gì #2](https://www.geeksforgeeks.org/storage-snapshot-technology/)

[Cách snapshot hoạt động](https://www.techtarget.com/searchdatabackup/feature/Everything-you-need-to-know-about-snapshotting)

![](https://cdn.ttgtmedia.com/rms/onlineImages/ST_1116_p9g1.jpg)

- là một tập hợp các điểm đánh dấu tham chiếu cho dữ liệu tại một thời điểm cụ thể, ví dụ giống như một danh mục chi tiết, cung cấp cho người dùng bản sao dữ liệu có thể truy cập mà họ có thể quay lại.
- Nếu có vấn đề xảy ra như mất toàn bộ data thì snapshot cũng không còn tác dụng

- Pros:
  - Chỉ yêu cầu rất ít dữ liệu qua các thao tác sửa đổi để tối ưu hóa việc sử dụng resource của hệ thống
  - Hồi phục data nhanh hơn backup
- Cons:
  - Nếu data bị bảo mật khỏi quá trình sản xuất, snapshot sẽ bị hạn chế tác dụng
  - Các snapshot sẽ lưu trữ tạm thời ở một kho đồng thời cũng sẽ chiếm nhiều dung lượng nếu quá trình sản xuất cần thiết phải lưu snapshot liên tục

- Cách snapshot hoạt động:
  - cơ bản nó tập hợp các khối đĩa thể hiện hình thức của hệ thống tệp hoặc ổ đĩa tại một thời điểm cụ thể
  - Nó lưu metadata mà metadata này liên kết với từng khối dữ liệu và sao chép dữ liệu vào một không gian chỉ định trước khi sửa đổi, snapshot được dùng cho VM, db và file.

> Trong thực tế, nên sử dụng snapshot kết hợp với backups

- Các loại snapshot:
  - `Copy-on-Write (CoW)`: sao chép dữ liệu khi nó được sửa đổi. Khi hành động write xảy ra, dữ liệu được sao chép vào snapshot và tách biệt với nguồn dữ liệu gốc - Cách này hiệu quả với dữ liệu không được sửa đổi thường xuyên [CoW là gì?](https://stackoverflow.com/questions/628938/what-is-copy-on-write)
  - `Redirect-on-Write (RoW)`: là một snapshot được tạo bằng cách chuyển hướng ghi dữ liệu đã được thay đổi sang các khối lưu trữ mới và cập nhật các con trỏ của hệ thống tệp đang hoạt động vào các khối đó. Dữ liệu gốc vẫn được giữ nguyên và dữ liệu mới được ghi vào một vị trí khác trên đĩa. Sau khi yêu cầu ghi được hoàn thành và xác nhận, dữ liệu gốc sẽ được liên kết với snapshot và dữ liệu mới được ghi sẽ được liên kết với tập chính (cách này nhanh hơn, nhưng dữ liệu sẽ không được liên tục)
  - `Server-side`: bản sao tại thời điểm hệ thống tệp của máy chủ khi đó (bao gồm dữ liệu và cấu hình)
  - `client-sided`: bản sao tại thời điểm hệ thống tệp của máy khách khi đó (bao gồm dữ liệu và cấu hình)
  - `split mirror snapshot`: là loại snapshot tạo bản sao đầy đủ của ổ lưu trữ gốc thay vì chỉ chụp nhanh các khối đã sửa đổi
# Backup & restore

[about backup](https://www.geeksforgeeks.org/backup-and-restore/)

- Back up là việc sao lưu toàn bộ DB bản sao hoàn chỉnh, khắc phục các thảm họa
- Có các loại backup sau đây:
  - `Full backup`: Sao lưu toàn bộ
  - `Differential backup`: Chỉ sao lưu các dữ liệu đã thay đổi kể từ lần sao lưu đầy đủ từ trước đó (có full backup từ trước đó)
  - `Incremential backup`: Chỉ sap lưu các dữ liệu đã thay đổi kể từ lần sao lưu đầu đủ trước đó (mỗi một back nhỏ thể hiện như 1 khối mỗi khi incremental backup được thực hiện)
  - `Network backup`: Sao lưu các thành phần mạng, các config, lịch backup và các dữ liệu liên quan đến network

![](https://learn.g2.com/hs-fs/hubfs/G2CR_B029_Incremental_vs._Differential_Backups_V1.png?width=2046&name=G2CR_B029_Incremental_vs._Differential_Backups_V1.png)

- Ngoài ra còn có các công cụ ngoại vi có khả năng lưu trữ bên ngoài phần cứng máy tính