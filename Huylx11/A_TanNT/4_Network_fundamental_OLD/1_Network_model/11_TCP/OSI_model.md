# OSI model là gì?

[OSI model](https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/)

[OSI model và các concept liên quan](https://www.freecodecamp.org/news/osi-model-networking-layers-explained-in-plain-english/)

- Open System Interconnection: OSI là một mô hình khái niệm được đưa ra để thể hiện tiêu chuẩn giao tiếp giữa các hệ thống máy tính. Với mỗi một tầng cụ thể, các lớp làm một nhiệm vụ riêng biệt nhưng đều có liên kết với lớp bên trên và bên dưới chính nó.
- Mỗi một tầng (layer) là một phân loại chức năng và các hành vi của network

![OSI_model](https://i.ytimg.com/vi/qwBcZnhZM5c/maxresdefault.jpg)

<!-- - Các node khi giao tiếp với nhau các day được các thiết bị thực hiện lần lượt các thao tác với data. Các data được gắn các các header khi di chuyển từ máy gửi (di chuyển từ tầng 7 -> tầng 1) đến mxáy nhận (di chuyển từ tầng 1 -> tầng 7) và ngược lại các header sẽ được gỡ dần ra. -->

# OSI model và cách dịch chuyển dữ liệu

![OSI data moving](https://media.geeksforgeeks.org/wp-content/uploads/20210220204638/cn1.png)

![OSI model data flow](https://www.omnisecu.com/images/tcpip/data-flow-osi-model.jpg)

[How OSI model works?](https://www.geeksforgeeks.org/open-systems-interconnection-model-osi/)

<!-- GIẢI THÍCH THEO LUỒNG DATA ĐƯỢC GỬI ĐẾN (L1 - L7)
1. Dữ liệu dưới L1 ở dạng bit (0,1) để truyền data dưới dạng tín hiệu điện sang host khác. Sau đó, các data lúc này sẽ được chia ra thành các frame (nhóm bit data)
2. L2 nhận frame. Lúc này, 2 sub-layer trong L2 hoạt động
  - LLC: framing, addressing và flow control (các công việc này liên quan tới đóng gói các frame thành package, giải địa chỉ)
  - MAC: chứa thông tin đối chiếu với địa chỉ MAC từ bit data (data do L1 nhận)
3. L3 nhận package từ L2. L3 đối chiếu IP address trong package. Nếu phù hợp thì chuyển tiếp lên L4
4. L4 nhận segment (package được đóng gói thành segment)  -->
---
---
# Các layer trong OSI model

> layer 1: PHYSIC LAYER (tầng vật lý)

[Tầng 1 OSI](https://www.freecodecamp.org/news/osi-model-networking-layers-explained-in-plain-english/)

- Nhắc tới tầng vật lý là bao gồm mọi thiết bị vật lý, từ hệ thống cáp, cách cáp kết nối với thiết bị. Nó mô tả phương thức truyền dẫn data `(chính xác là bit data dưới dạng tín hiệu điện 0 và 1, bit data là unit được truyền ở tầng này)` từ hệ thống này sang hệ thống khác dưới dạng vật lý (dây cáp hoặc các loại tín hiệu không dây) và hardware. Một số danh mục đề cập các loại công nghệ trong lớp 1:
  - Nodes (các loại device trong network topology) với các components khác liên quan đến network: đề cập đến các thiết bị như router, repeater, hub, computer, printer bao gồm các hardware components khác trong các thiết bị đó: network interface card, etc

  ![Node trong star network topology](https://upload.wikimedia.org/wikipedia/commons/8/84/Star_Topology.png)

  - Device interface mechanics (cách thức kết nối của các thiết bị): cáp kết nối với máy tính và các thiết bị khác như nào (số lượng chân kết nối socket, etc)? Kích thước và hình dạng của đầu kết nối các loại cáp
  - Chức năng và logic luồng thực hiện: chức năng của mỗi chân kết nối của cáp, gửi thông tin và nhận thông tin như nào? Một luồng logic bắt đầu thực hiện các event như thế nào để các node có thể giao tiếp đươc với nhau trên tầng 2 OSI
  - Các giao thức và thông số kỹ thuật: nhắc đến các loại kết nối và công nghệ truyền dẫn khác nhau như Ethernet (là công nghệ mạng cục bộ-LAN và sử dụng cáp để truyền dẫn thông tin giữa các thiết bị trong local area), USB (một giao thức truyền dữ liệu phổ biến truyền dữ liệu giữa các device) hoặc là DSL (Digital subscriber line - đường dây thuê bao kỹ thuật số sử dụng trong việc kết nối máy tính và các thiết bị khác với Internet thông qua đường dây điện thoại)
  - Loại cáp: Các loại dây cáp mạng
  - Loại tín hiệu: chẳng hạn như baseband (dùng toàn bộ băng thông cho một tín hiệu duy nhất, thường được sử dụng trong LAN) và broadband (dùng băng thông chia sẻ cho nhiều tín hiệu, thường được dùng trong hệ thống mạng rộng hơn)
  - Phương thức truyền tín hiệu khác

> layer 2: DATA LINK LAYER (tầng liên kết dữ liệu)

[Tầng 2 OSI](https://www.freecodecamp.org/news/osi-model-networking-layers-explained-in-plain-english/)

[Cách hoạt động giữa layer2 và layer3](https://youtu.be/LkolbURrtTs?si=CdZjIldTF1q1CzPg)

- Tầng liên kết dữ liệu xác định dữ liệu được định dạng như thế nào, lượng dữ liệu được truyền giữa các node và các lỗi được detect như thế nào trong data flow đó. Switch là thiết bị hoạt động chính trong tầng này. Có 3 term được nhắc đến trong tầng 2 này `(unit data trong tầng này là frame)`
  - Line discipline: các node có thể truyền thông tin trong bao lâu
  - FLow control: lượng dữ liệu được truyền bao nhiêu
  - Error control - phát hiện và sửa lỗi: tầng 2 chủ yếu liên quan đến việc phát hiện lỗi, phục vụ báo cho admin biết để sửa lỗi trên tầng tiếp theo

- Cấu trúc của một frame:

![Cấu trúc của frame](https://www.freecodecamp.org/news/content/images/size/w1000/2021/11/5-Frame-Example.jpeg)

  - Phần data đi kèm với phần header và trailer. Được dùng để giao tiếp với các phần layer trên và dưới
  - Phần header gồm thông tin được layer hiện tại thêm vào frame
  - Phần Trailer chỉ có frame trong L2 mới có, chỉ với tác dụng là error detection

- Có 2 sub-layer tồn tại trong tầng 2:
  
  ![2 sub-layer](https://www.ictshore.com/wp-content/uploads/2016/11/1012-02-MAC_and_LLC.png)

  - Media access control (MAC): MAC chịu trách nhiệm gán địa chỉ phần cứng (MAC address number, được đánh số từ lúc sản xuất)
  - Logical Link Control (LLC): Điều khiển liên kết logic chịu trách nhiệm xử lý bao gồm: framming (tạo và giải các frame, frame là package gồm có thông tin về địa chỉ, kiểm tra lỗi, kiểm soát luồng), addressing (gán và giải các địa chỉ, thường là MAC address) và flow control (sắp xếp gói dữ liệu phù hợp) [How does LLC do?](https://www.geeksforgeeks.org/logical-link-control-llc-protocol-data-unit/)
  - `Vậy có 3 việc chính mà 2 sub-layer chịu trách nhiệm:`
    - Framming giải/đóng gói data trong tầng này được  theo từng frame trước khi gửi/nhận đến hệ thống khác, đồng thời addressing gán/phân tích địa chỉ frame
    - Flow control sẽ quản lý các thứ các packet để đảm bảo dữ liệu không bị sai lệch trong quá trình ghép các bit data/tách các frame data
    - Error control sẽ kiểm tra các lỗi của các frame
    [A descent example about how LLC in DLL works](https://fossbytes.com/llc-logical-link-control-layer-osi-model/)

> layer 3: NETWORK LAYER (tầng network)

[Tầng 3 OSI](https://www.freecodecamp.org/news/osi-model-networking-layers-explained-in-plain-english/)

[Packet và Frame](https://www.baeldung.com/cs/osi-packets-vs-frames)

- Tầng 3 gửi thông tin giữa và qua nhiều các network thông qua bộ định tuyến. Thay vì trao đổi thông tin giữa các node trong một network, bây giờ có thể trao đổi thông tin giữa các network. Router là thiết bị chính hoạt động trong tầng này và sẽ gửi các data packet `(data packet là data unit di chuyển trong tầng này)`
- Để đưa data di chuyển, L3 cũng thêm header giống như L2, thêm địa chỉ IP vào packet

![Packet structure](https://www.baeldung.com/wp-content/uploads/sites/4/2021/10/datagram.png)

  - Phần header gồm thông tin được layer hiện tại thêm vào frame để gửi cho đầu end
  - Destination address: địa chỉ nhận
  - Source address: địa chỉ gửi
  - Data

> layer 4: TRANSPORT LAYER (tầng vận chuyển)

[Tầng 4 OSI](https://www.freecodecamp.org/news/osi-model-networking-layers-explained-in-plain-english/)

![TCP & UDP](https://www.microchipdeveloper.com/local--files/tcpip:tcp-vs-udp/TCP_vs_UDP.JPG)

- Tầng 4 sẽ đi qua 2 cái tên: `TCP (transmision control protocol) và UDP (User datagram protocol)`
  - TCP
    - Ưu tiên chất lượng của data (data được nhận có đầy đủ không) được nhận hơn là tốc độ nhận/gửi của data (kết nối cần phải được thiết lập trước)
    - TCP thiết lập 1 kết nối chắc chắn giữa 2 node (thiết bị nhận và thiết bị gửi), sẽ có thông báo (handshake - để confirm đã nhận được đầy đủ data) được gửi đến khi data được nhận/gửi đầy đủ. Nếu không, TCP sẽ gửi yêu cầu gửi lại.
    - TCP đồng thời cũng đảm nhận packet phải được sắp xếp theo đúng trật tự.
  - UDP
    - Ngược lại với TCP, UDP ưu tiên tốc độ nhận/gửi hơn chất lượng của data được nhận vào
    - Không đảm bảo data được truyền đầy đủ (tuy nhiên lại hữu ích trong video, voice streaming)
    - Không đảm bảo packet tiếp nhận được sắp xếp theo đúng trật tự

- `Data unit trong L4 là segment/datagram`
  - Với Segment: TCP sẽ chia nhỏ data trong các packet ở tầng 3 thành segment
  - Với datagram: UDP chia nhỏ data trong các packet ở tầng 3 thành datagram và đánh số các datagram (khi cần sắp xếp lại, UDP cũng sắp xếp nhưng not sure có đúng hay không)

> layer 5: SESSION LAYER (tầng phiên)

[Tầng 5 OSI](https://www.freecodecamp.org/news/osi-model-networking-layers-explained-in-plain-english/)

- Tầng 5 thiết lập, duy trì và hủy session, cũng như đảm bảo tính bảo mật trong đó
- Session ở đây được hiểu là sự kết nối giữa 2 người dùng app cụ thể và bên được yêu cầu thông tin (requested information) là server. Có thể được coi như là mô hình trao đổi thông tin 2 chiều sau:
  - Client và server model
  - Request và response model
- 2 protocol thường thấy ở L5 là NetBIOS (Network basic input output system) và RPC (Remote Procedure Call Protocol)

- Có thể nói L5 như một câu cầu thiết lập liên kết giữa tầng trên và tầng dưới

> layer 6: PRESENTATION LAYER (tầng phiên)

[Tầng 6 OSI](https://www.freecodecamp.org/news/osi-model-networking-layers-explained-in-plain-english/)

[OSI model with plain explain](https://medium.com/@igordr3/osi-model-session-presentation-and-application-layer-5-6-and-7-a7e6b0360380)

- Tầng 6 chịu trách nhiệm format data (mã hóa, chuyển đổi data). Xử lý dữ liệu đến từ L5 và có thể được định dạng và hiểu theo nghĩa cho người dùng cuối có thể hiểu, ngược lại dịch dữ liệu từ L7 cho L5 và L4 hiểu và đồng thời làm dữ liệu dễ truyền tải hơn
- Có 1 vài phương pháp định dạnh dữ liệu tiêu chuẩn như: ASCII (mã hóa ký tự), Unicode (thường được sử dụng để mã hóa ký tự của các ngôn ngữ khác nhau)
- Và 1 vài phương pháp mã hóa giúp nâng cao bảo mật dữ liệu: Như giao thức SSL (secure socket layer) và TLS (transport layer security - phiên bản cải tiến của SSL) sẽ mã hóa các dữ liệu tránh các tác nhân gây ảnh hưởng xấu đến dữ liệu đang được truyền đi

> layer 7: APPLICATION LAYER

[Tầng 7 OSI](https://www.freecodecamp.org/news/osi-model-networking-layers-explained-in-plain-english/)

- Lớp duy nhất người dùng tương tác trực tiếp với các phần mềm, hỗ trợ các dịch vụ cung cấp các giao thức cho phần mềm gửi/nhận và hiển thị các thông tin có ý nghĩa cho người dùng. Cung cấp giao diện và sự liên kết giữa những ứng dụng và mạng mà data phải di chuyển giữa mạng 
- Một số giao thức hoạt động ở tầng này bao gồm FTP (File tranfer), SSH (secure shell), SMTP (simple internet message access protocol), DNS (dịch vụ tên miền).