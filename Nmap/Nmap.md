# Nmap

---

## Task 1: Deploy

## Task 2: Introduction

- Khi nói đến hack, kiến ​​thức là sức mạnh. Bạn càng có nhiều kiến ​​thức về hệ thống hoặc mạng mục tiêu, bạn càng có nhiều tùy chọn hơn. Điều này buộc phải thực hiện việc liệt kê thích hợp trước khi thực hiện bất kỳ nỗ lực khai thác nào.

![](https://i.imgur.com/3XAfRpI.png)

- Như trong ví dụ trước, sơ đồ hiển thị điều gì sẽ xảy ra khi bạn kết nối với nhiều trang web cùng một lúc. Máy tính của bạn mở ra một cổng khác, được đánh số cao (ngẫu nhiên), cổng này sử dụng cho tất cả các giao tiếp với máy chủ từ xa.

- Mỗi máy tính có tổng cộng 65535 cổng khả dụng; tuy nhiên, nhiều trong số này đã được đăng ký làm cổng tiêu chuẩn. Ví dụ: Dịch vụ web HTTP hầu như luôn có thể được tìm thấy trên cổng 80 của máy chủ. Có thể tìm thấy Dịch vụ web HTTPS trên cổng 443. Có thể tìm thấy Windows NETBIOS trên cổng 139 và SMB có thể tìm thấy trên cổng 445. Điều quan trọng cần lưu ý là; tuy nhiên, đặc biệt là trong cài đặt CTF, không có gì lạ khi ngay cả những cổng tiêu chuẩn này cũng bị thay đổi, khiến chúng tôi càng cần phải thực hiện phép liệt kê thích hợp trên mục tiêu.

- Nếu chúng tôi không biết máy chủ nào đã mở cổng nào trong số này, thì chúng tôi không có hy vọng tấn công thành công mục tiêu; do đó, điều quan trọng là chúng tôi bắt đầu bất kỳ cuộc tấn công nào bằng cách quét cổng. Điều này có thể được thực hiện theo nhiều cách khác nhau – thường là sử dụng một công cụ gọi là nmap, là trọng tâm của căn phòng này. Nmap có thể được sử dụng để thực hiện nhiều loại quét cổng khác nhau – loại phổ biến nhất trong số này sẽ được giới thiệu trong các tác vụ sắp tới; tuy nhiên, lý thuyết cơ bản là thế này: nmap sẽ lần lượt kết nối với từng cổng của mục tiêu. Tùy thuộc vào cách cổng phản hồi, nó có thể được xác định là đang mở, đóng hoặc lọc (thường là do tường lửa). Khi chúng tôi biết cổng nào đang mở, chúng tôi có thể xem liệt kê dịch vụ nào đang chạy trên mỗi cổng – theo cách thủ công hoặc thông thường hơn là sử dụng nmap.

- Vì vậy, tại sao nmap? Câu trả lời ngắn gọn là hiện tại nó là tiêu chuẩn công nghiệp vì một lý do: không có công cụ quét cổng nào khác sánh được với chức năng của nó (mặc dù một số người mới hiện đang bắt kịp nó về tốc độ). Nó là một công cụ cực kỳ mạnh mẽ -thậm chí còn mạnh mẽ hơn nhờ công cụ viết kịch bản của nó, có thể được sử dụng để quét các lỗ hổng và trong một số trường hợp, thậm chí thực hiện khai thác trực tiếp! Một lần nữa, điều này sẽ được đề cập nhiều hơn trong các nhiệm vụ sắp tới.

1. What networking constructs are used to direct traffic to the right application on a server?: `ports`.
2. How many of these are available on any network-enabled computer?: `65535`.
3. **[Research]** How many of these are considered "well-known"? (These are the "standard" numbers mentioned in the task): `1024`.

## Task 3: Nmap Switches

- Giống như mọi công cụ `pentest` khác thì `Nmap` cũng được chạy thông qua `Terminal`. Có một số phiên bản cho Windows và Linux.
- `Nmap` được truy cập với việc gõ `nmap` vào Terminal Command Line, tiếp theo ta phải truyền cho nó một vài `agrument`.

1. What is the first switch listed in the help menu for a 'Syn Scan' (more on this later!)?: `-sS`.
2. Which switch would you use for a "UDP scan"?: `-sU`.
3. If you wanted to detect which operating system the target is running on, which switch would you use?: `-O`.
4. Nmap provides a switch to detect the version of the services running on the target. What is this switch?: `-sV`.
5. The default output provided by nmap often does not provide enough information for a pentester. How would you increase the verbosity?: `-v`.
6. Verbosity level one is good, but verbosity level two is better! How would you set the verbosity level to two?: `-vv`.
(**Note**: it's highly advisable to always use at least this option)
7. We should always save the output of our scans -- this means that we only need to run the scan once (reducing network traffic and thus chance of detection), and gives us a reference to use when writing reports for clients.
What switch would you use to save the nmap results in three major formats?: `-oA`.
8. What switch would you use to save the nmap results in a "normal" format?: `-oN`.
9. A very useful output format: how would you save results in a "grepable" format?: `-oG`.
10. Sometimes the results we're getting just aren't enough. If we don't care about how loud we are, we can enable "aggressive" mode. This is a shorthand switch that activates service detection, operating system detection, a traceroute and common script scanning.
How would you activate this setting?: `-a`.
11. Nmap offers five levels of "timing" template. These are essentially used to increase the speed your scan runs at. Be careful though: higher speeds are noisier, and can incur errors! How would you set the timing template to level 5?: `-T5`.
12. We can also choose which port(s) to scan. How would you tell nmap to only scan port 80?: `-p 80`.
13. How would you tell nmap to scan ports 1000-1500?: `-p 1000-1500`.

**_A very useful option that should not be ignored:_** 

1. How would you tell nmap to scan all ports: `-p-`.
2. How would you activate a script from the nmap scripting library (lots more on this later!)?: `--script`.
3. How would you activate all of the scripts in the "vuln" category?: `--script=vuln`. (There are two variants of this switch. One with a space, one with the equals sign.)

## Task 4: (Scan Types) Overview

- Khi mà scan với `Nmap`, có 3 loại scan cơ bản. Đó là:
	+	TCP Connect Scans `-sT`
	+	SYN "Half-open" Scans `-sS`
	+	UDP Scans `-sU`

- Bên cạnh đó còn có một số scan port không phổ biến như:
	+	TCP Null Scans `-sN`
	+	TCP FIN Scans `-sF`
	+	TCP Xmas Scans `-sX`

- Ngoại trừ `UDP scans`, tất cả những cách scan còn lại đều có mục đích gần giống nhau.

## Task 5: (Scan Types) TCP Connect Scans

- `TCP` scans: `-sT`.

- `TCP` scan port theo cơ chế `TCP` three-way handshake.

![](https://muirlandoracle.co.uk/wp-content/uploads/2020/03/image-2.png)

Với phương thức kết nối này, Nmap sẽ gửi yêu cầu tạo kết nối `SYN`. Nếu cổng đó được mở nó sẽ gửi lại tín hiệu `SYN/ACK` còn nếu cổng đó đóng nó sẽ gửi lại tín hiệu `RST` (Reset).

> Tuy nhiên còn một trường hợp chúng ta phải lưu ý đó là nếu một cổng được mở tuy nhiên nó được bảo vệ bảo FireWall. Tức nếu ta gửi yêu cầu `SYN` đến cổng đó thì yêu cầu sẽ bị `Drop` và không nhận được tín hiệu phản hồi gì.

- Ta có thể cấu hình tường lửa để gửi phản hồi với `RST` bằng cách sử dụng `IPtables` trong `Linux`. Điều này làm đối tượng tấn công khó xác định được cổng mục tiêu.

> iptables -I INPUT -p tcp --dport <port> -j REJECT --reject-with tcp-reset

1. Which RFC defines the appropriate behaviour for the TCP protocol?: `RFC 793`.
2. If a port is closed, which flag should the server send back to indicate this?: `RST`.

## Task 6: SYN Scans

- `SYN` scan: `-sS`.

`SYN` scan sẽ quét một hoặc nhiều cổng có thể kết nối của mục tiêu. Tuy nhiên, so với `TCP` scan thì nó khác nhau về cách hoạt động. Thay vì thực hiện full Three-way handshake giống như `TCP` thì `SYN` sẽ chỉ gửi đi một yêu cầu `SYN`, sau khi được chấp nhận và được phía mục tiêu gửi lại tín hiệu `SYN/ACK` thì nó sẽ gửi lại 1 `RST` request chứ không phải `ACK` giống như Three-way handshake.

![](https://i.imgur.com/cPzF0kU.png)

![](https://i.imgur.com/bcgeZmI.png)

Một số ưu điểm của `SYN` scans:

- Nó dễ dàng cho hacker bypass được những hệ thống IDS(Intrusion Dectection System) cũ.
- Quá trình quét SYN thường không được ghi lại bởi các ứng dụng đang nghe trên các cổng mở, vì thông lệ tiêu chuẩn là ghi lại kết nối sau khi kết nối được thiết lập đầy đủ.
- Thay vì hoàn thành kết nối và sau đó phải ngắt kết nối như `TCP` scans thì `SYN` scans nhanh hơn đáng kể.

Một vài nhược điểm của `SYN` scans:

- Nó yêu cầu `sudo` permission để thực hiện chính xác trên `Linux`. Bởi vì nó yêu cầu khả năng tạo `raw packet` điều mà chỉ có đặc quyền của `root` user làm được.
- Đôi khi `SYN` scans có thể làm sập một dịch vụ không ổn định.

Nó chỉ khác với `TCP` scans ở việc thực hiện các cổng mở còn các cổng đóng hoặc các yêu cầu bị `drop` bởi tường lửa thì đều giống `TCP` scans.

1. There are two other names for a SYN scan, what are they?: `Half-open,stealth` (mở một nửa/ tàng hình).
2. Can Nmap use a SYN scan without Sudo permissions (Y/N)?: `N`.

## Task 7: UDP Scans

- Khác với `TCP`, `UDP` là một kết nối "**_không trạng thái_**". 
- Nó sẽ gửi tín hiệu đến mục tiêu và mong nhận lại được phản hồi. Có 2 trường hợp sẽ xảy ra.
  - Nếu packet được gửi đến `UDP` port, thông thường sẽ không có tín hiệu phản hồi. Từ đó `Nmap` sẽ nhận định đó là một cổng `open|filtered`. Nó sẽ tiếp tục gửi yêu cầu lần thứ 2 nếu chưa nhận được phản hồi, nếu vẫn tiếp tục không có phản hồi thì kết quả trả về là `open|filtered`. Nếu nhận lại được `UDP` response thì cổng đó chắc chắn `open`.
  - Nếu gửi tín hiệu đến một cổng `UDP` đón, mục tiêu sẽ trả về phản hồi `ICMP` (ping).

`UDP` scan có tốt độ chậm hơn hẳn so với `TCP` scan bởi vì `UDP` khó xác định một cổng bất kì có mở hay không. Vì vậy thông thường ta sẽ chạy `Nmap` với 20 cổng `UDP` thông dụng nhất:

> nmap -sU --top-ports 20 <`target`>

1. If a UDP port doesn't respond to an Nmap scan, what will it be marked as?: `open|filtered`.
2. When a UDP port is closed, by convention the target should send back a "port unreachable" message. Which protocol would it use to do so?: `ICMP`.

## Task 8: NULL, FIN and Xmas

- `NULL`, `FIN` và `Xmas` không phổ biến giống như các loại scan còn lại.

Nó có cơ chế gần giống như `SYN` scans.

- `NULL` scans (-sN) khi gửi request sẽ gửi cùng `NULL` flags. Nó sẽ nhận được tín hiệu `RST` (reset) nếu như cổng đó đóng. 

![](https://i.imgur.com/ABCxAwf.png)

- `FIN` scans (-sF) khi gửi request sẽ gửi cùng `FIN` flags. Nó sẽ nhận được tín hiệu `RST` (reset) nếu như cổng đó đóng.

![](https://i.imgur.com/gIzKbEk.png)

- `Xmas` scans (-sX) khi gửi request sẽ gửi kèm một flag khá kì dị. Nó sẽ nhận được tín hiệu `RST` nếu như cổng đó đóng.
  - Nó được gọi là quét "**_Giáng sinh"_** vì các cờ mà nó đặt (PSH, URG và FIN) khiến nó trông giống cây thông Noel nhấp nháy khi được xem dưới dạng chụp gói trong Wireshark.
