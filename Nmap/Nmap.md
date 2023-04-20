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







