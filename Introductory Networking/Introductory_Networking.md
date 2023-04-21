# Introductory Networking

--- 

## Task 1: Introduction

> <p> Mục đích của căn phòng này là cung cấp cho người mới bắt đầu những nguyên tắc cơ bản của mạng. Mạng là một chủ đề lớn  , vì vậy đây thực sự sẽ chỉ là một tổng quan ngắn gọn; tuy nhiên, nó hy vọng sẽ cung cấp cho bạn một số kiến ​​thức cơ bản về chủ đề mà bạn có thể tự xây dựng dựa trên đó . </p>

- The OSI Model
- The TCP/IP Model
- How these models look in practice
- An introduction to basic networking tools

## Task 2: The OSI Model: An Overview

- OSI (Open Systems Interconnection) Model là một mô hình được chuẩn hóa để mô tả về mạng máy tính.
- Trên thực tế nó là mô hình `TCP/IP` nhỏ gọn hơn.

![](https://muirlandoracle.co.uk/wp-content/uploads/2020/02/OSI-Table.png)

![](https://res.cloudinary.com/practicaldev/image/fetch/s--1bRgOplD--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/eiq51lb9mtuynx48gje0.jpeg)

### Layer 7: Application 

- Tầng `Application` của OSI model cung cấp những tùy chọn mạng thiết yếu cho chương trình mà máy tính đang chạy. Nó chỉ làm việc với duy nhất với các ứng dụng, cung cấp giao diện cho chúng sử dụng để truyền dữ liệu.
- Tầng này sẽ tiếp nhận những yêu cầu từ người dùng.
- Khi dữ liệu được gửi cho tầng `Application`, nó sẽ được truyền lại xuống cho tầng `Presentation`.

### Layer 6: Presentation

- Tầng `Presentation` nhận dữ liệu từ tầng `Application`.
- Dữ liệu thường được để ở dạng mà ứng dụng có thể hiểu được, tuy nhiên nó không cần thiết phải để ở dạng dữ liệu mà tầng `Application` ở máy tính nhận có thể hiểu được.
- Vậy nên tầng `Presentation` chuyển dữ liệu về dạng tiêu chuẩn hóa, cũng có thể xử lý dữ liệu như mã hóa, nén dữ liệu. Sau khi hoàn thành, nó gửi dữ liệu xuống cho tầng `Session`.

### Layer 5: Session

- Tầng `Session` khi nhận đúng dạng dữ liệu từ tầng `Presentation`, nó sẽ xem xét có thể thiết lập kết nối đến với đến máy tính khác thông qua mạng không. 
- Nếu không thể nó sẽ gửi lại lỗi và không thể tiến xa hơn. Nếu `Session` có thể thiết lập được kết nối thì công việc tiếp theo sẽ là duy trì nó. Cũng như là việc hợp tác với máy tính còn lại để đồng bộ hóa dữ liệu giữa 2 máy tính. 
- Tầng `Session` đặc biệt quan trọng vì nó tạo ra sự kết nối như đã đề cập. Đây là điều cho phép bạn thực hiện đồng thời nhiều yêu cầu đến các điểm cuối khác nhau mà không làm xáo trộn dữ liệu. 
- Khi tầng `Session` hoàn thành, dữ liệu sẽ được tiếp tục chuyển xuống tầng `Transport`.

### Layer 4: `Transport` 

- Tầng `Transport` là một tầng rất thú vị vì nó có nhiều chức năng quan trọng. 
- Đầu tiên nó sẽ chọn ra phương thức (protocol) được sử dụng để truyền dữ liệu đi. Ở đây có 2 phương thức phổ biến nhất đó là `TCP` (Transmission Control Protocol) và `UDP` (User Datagram Protocol).
	+ Với TCP là phương thức tryền dữ liệu dựa trên kết nối. Hai máy tính phải được thiết lập và duy trì kết nối trong suốt thời gian yêu cầu. Điều này cho phép truyền thông tin một cách tin cậy vì nó luôn được đảm bảo dữ liệu được gửi đến đúng địa chỉ. Kết nối TCP cho phép hai máy tính duy trì liên lạc liên tục để đảm bảo rằng dữ liệu được gửi ở tốc độ chấp nhận được và mọi dữ liệu bị mất sẽ được gửi lại.
	+ Với UDP thì ngược lại. Các gói dữ liệu được ví như được ném vào máy tính nhận. Nếu nó không theo kịp thì cũng không quan tâm. Điều này giải thích cho việc vì sao call video qua các nền tảng sẽ bị hình ảnh pixel nếu như kết nối kém.
- Điều này có nghĩa là TCP thường được chọn cho các tình huống trong đó độ chính xác được ưu tiên hơn tốc độ (ví dụ: truyền tệp hoặc tải trang web) và UDP sẽ được sử dụng trong các tình huống mà tốc độ quan trọng hơn (ví dụ: truyền phát video).
- Với giao thức được chọn, máy tính sẽ chia dữ liệu thành các phần có kích thước vừa phải (TCP là segments còn UDP là datagram).

### Layer 3: Network

- Tầng `Network` chịu trách nghiệm xác định vị trí đích của yêu cầu của bạn. Nó sẽ lấy địa chỉ IP của trang web bạn yêu cầu và tìm ra route kết nối ổn định nhất. 
- Tầng `Network` sẽ làm việc với những địa chỉ `Logical`. Phổ biến nhất của địa chỉ logic là IPv4 (ví dụ 192.168.1.1 là địa chỉ phổ biến cho bộ định tuyến của gia đình bạn).

### Layer 2: Data Link

- Tầng `Data Link` tập trung vào địa chỉ `Physical`. Nó sẽ nhận dữ liệu từ tầng `Network` (địa chỉ IP của máy tính khác) và thêm vào địa chỉ vật lý (physical) của điểm cuối nhận. 
- Bên trong mỗi máy tính có hỗ trợ mạng đều có một NIC (Network Interface Card) đi kèm với một địa chỉ MAC (Media Access Control) duy nhất để nhận dạng nó.
- Địa chỉ MAC được thêm bởi nhà sản xuất và ghi vào thẻ, không thể thay đổi nó, mặc dù nó có thể giả mạo. Khi thông tin được gửi qua mạng nó sẽ sử dụng, địa chỉ vật lý MAC được sử dụng để xác định chính xác nơi để gửi thông tin.
- Ngoài ra tầng `Data Link` cũng trình bày dữ liệu ở dạng phù hợp để truyền đi. Nó có vai trò kiểm tra dữ liệu có bị hỏng khi bị truyền đi hay không, điều mà có thể xảy ra ở tầng `Physical`.

### Layer 1: Physical

- Tầng `Physical` nằm ngay dưới phần cứng của máy tính.
- Tầng này có tác dụng chuyển các dữ liệu nhị phân thành tín hiệu để gửi đi cũng như nhận các tín hiệu được gửi đến và chuyển thành dữ liệu nhị phân.
- Tầng này có tác dụng truyền và nhận dữ liệu.

1. Which layer would choose to send data over TCP or UDP?: `4`
2. Which layer checks received information to make sure that it hasn't been corrupted?: `2`.
3. In which layer would data be formatted in preparation for transmission?: `2`.
4. Which layer transmits and receives data?: `1`.
5. Which layer encrypts, compresses, or otherwise transforms the initial data to give it a standardised format?: `6`.
6. Which layer tracks communications between the host and receiving computers?: `5`.
7. Which layer accepts communication requests from applications?: `7`.
8. Which layer handles logical addressing?: `3`.
9. When sending data over TCP, what would you call the "bite-sized" pieces of data?: `segments`.
10. *[Research]* Which layer would the FTP protocol communicate with?: `7`.
11. Which transport layer protocol would be best suited to transmit a live video?: `UDP`.


## Task 3: Encapsulation

![](https://muirlandoracle.co.uk/wp-content/uploads/2020/02/image.jpeg)

- Khi thông tin được truyền xuống từng tầng, nó sẽ được bổ sung thông tin của tâng nó đi qua trước khi được truyền xuống các tầng còn lại.
- Tầng `Data Link` còn có thêm một phần ở cuối quá trình truyền, được dùng để xác minh tính toàn vẹn, điều này còn bổ sung thêm về tính bảo mật vì dữ liệu không thể bị chặn hoặc giả mạo khi mà nó đã làm hỏng `Trailer`.
- Toàn bộ quá trình này gọi là `Đóng gói`, quá trình mà dữ liệu được gửi từ máy tình này qua máy tính khác.
- Ở tầng 7,6 và 5 dữ liệu vẫn được thể hiện ở dạng `data`. Tuy nhiên ở tầng 4 nó đã được thể hiện ở dạng `Segments` hoặc `Datagram`. Ở tầng 3 thể hiện ở dạng `Packet`. Ở tầng 2 có dạng `Frames` và ở tầng cuối khi được truyền thông qua internet nó sẽ có dạng `Bits`.
- Khi máy tính thứ hai nhận được thông báo, nó sẽ đảo ngược quá trình -- bắt đầu từ tầng `Physical` và hoạt động cho đến khi đến tầng `Application`, loại bỏ thông tin được thêm vào khi nó di chuyển. Điều này được gọi là giải đóng gói (de-encapsulation). Như vậy tất cả các máy tính đều tuân theo cùng một quy trình đóng gói để gửi dữ liệu và giải mã khi nhận dữ liệu bất kể chúng đến từ cùng một nhà sản xuất; sử dụng cùng một hệ điều hành; hoặc bất kỳ yếu tố nào khác.

1. How would you refer to data at layer 2 of the encapsulation process (with the OSI model)?: `frames`.
2. How would you refer to data at layer 4 of the encapsulation process (with the OSI model), if the UDP protocol has been selected?: `datagram`.
3. What process would a computer perform on a received message?: `de-encapsulation`.
4. Which is the only layer of the OSI model to add a trailer during encapsulation?: `Data-Link`.
5. Does encapsulation provide an extra layer of security (Aye/Nay)?: `Aye`.

## Task 4: The TCP/IP Model

- TCP/IP Model thực chất là tương đồng như OSI Model. Tuy nhiên nó có kết cấu ngắn gọn và không cứng nhắc như của OSI Model. Mặc dù có tuổi đời lâu hơn tuy nhiên TCP/IP vẫn có tính thực tế so với thế giới mạng hiện nay.

- TCP điều khiển dòng chảy dữ liệu giữa 2 thiết bị còn IP kiểm soát cách mà các gói dữ liệu được xử lý và gửi đi. TCP dựa trên phương thức _connection-based_ ngược lại so với UDP.

- TCP/IP Model chỉ có 4 tầng thay vì 7 tầng như của OSI Model.
	+ Application.
	+ Transport.
	+ Internet.
	+ Network Interface.

![](https://muirlandoracle.co.uk/wp-content/uploads/2020/02/image-4.png)

- Các tầng của 2 Model có liên hệ với nhau thông qua bảng sau:

![](https://muirlandoracle.co.uk/wp-content/uploads/2020/02/image-3.png)

- Cách thức đóng gói và giải đóng gói đều tương tự nhau không có gì thay đổi. Thêm header ở phần đóng gói và xóa đi ở phần giải đóng gói.

- TCP/IP được lấy tên viết tắt của 2 phương thức truyền dữ liệu phổ biến: TCP (Transmission Control Protocol) và IP (Internet Protocol).
- Như đã đề cập phần trước, TCP cần có kết nối ổn định giữa 2 máy tính trước khi tạo kết nối để dữ liệu được truyền đi. Quá trình hình thành kết nối giữa 2 máy tính được gọi là `bắt tay 3 bước` (**_three-way handshake_**).

### Three-way handshake

- Khi bạn cố gắng tạo kết nối, trước tiên máy tính của bạn sẽ gửi một yêu cầu đặc biệt đến máy chủ từ xa cho biết rằng nó muốn khởi tạo kết nối. Yêu cầu này chứa một thứ gọi là bit SYN (viết tắt của đồng bộ hóa), về cơ bản, đây là liên hệ đầu tiên khi bắt đầu quá trình kết nối. Sau đó, máy chủ sẽ phản hồi bằng một gói chứa bit SYN, cũng như một bit "xác nhận" khác, được gọi là ACK. Cuối cùng, máy tính của bạn sẽ tự gửi một gói chứa bit ACK, xác nhận rằng kết nối đã được thiết lập thành công. Khi quá trình bắt tay ba bước hoàn tất thành công, dữ liệu có thể được truyền một cách đáng tin cậy giữa hai máy tính. Bất kỳ dữ liệu nào bị mất hoặc bị hỏng khi truyền đều được gửi lại, do đó dẫn đến kết nối dường như không mất dữ liệu.

![](https://muirlandoracle.co.uk/wp-content/uploads/2020/03/image-2.png)

1. Which model was introduced first, OSI or TCP/IP?: `TCP/IP`.
2. Which layer of the TCP/IP model covers the functionality of the Transport layer of the OSI model (Full Name)?: `Transport`.
3. Which layer of the TCP/IP model covers the functionality of the Session layer of the OSI model (Full Name)?: `Application`.
4. The Network Interface layer of the TCP/IP model covers the functionality of two layers in the OSI model. These layers are Data Link, and?.. (Full Name)?: `Physical`.
5. Which layer of the TCP/IP model handles the functionality of the OSI network layer?: `Internet`.
6. What kind of protocol is TCP?: `Connection-based`.
7. What is SYN short for?: `SYNchronise`.
8. What is the second step of the three way handshake?: `SYN/ACK`.
9. What is the short name for the "Acknowledgement" segment in the three-way handshake?: `ACK`.


## Task 5: (Networking Tools) Ping

- Lệnh `Ping` được sử dụng để kiểm tra xem ta có thể kết nối với máy chủ từ xa hay không. Thông thường sẽ là kết nối đến với một website nào đó hoặc đến thiết bị trong mạng nội bộ gia đình xem đã cấu hình đúng hay chưa.
- `Ping` sử dụng giao thức ICMP, ít phổ biến hơn TCP/IP protocol. ICMP làm việc ở tầng `Network` của OSI model và ở tầng `Internet` của TCP/IP.
> Syntax: Ping < target >
- Lưu ý `Ping` trả về địa chỉ IP của server ta đang ping tới, ta có thể tận dụng điều này để tìm địa chỉ IP của máy chủ.

1. What command would you use to ping the bbc.co.uk website?: `ping bbc.co.uk`.
2. Ping muirlandoracle.co.uk What is the IPv4 address?: `217.160.0.152`.
3. What switch lets you change the interval of sent ping requests?: `-i`.
4. What switch would allow you to restrict requests to IPv4?: `-4`.
5. What switch would give you a more verbose output?: `-v`.


## Task 6: (Networking Tools) Traceroute

- `Traceroute` có thể được sử dụng để biểu diễn tất cả các máy chủ mà requests của bạn đi qua trước khi đi đến máy chủ chỉ định.

- Internet được tạo thành từ rất nhiều máy chủ và điểm cuối khác nhau, tất cả đều được nối mạng với nhau. Điều này có nghĩa là, để có được nội dung bạn thực sự muốn, trước tiên bạn cần đi qua một loạt các máy chủ khác. Traceroute cho phép bạn xem từng kết nối này -- nó cho phép bạn xem mọi bước trung gian giữa máy tính của bạn và tài nguyên mà bạn yêu cầu.

- `Traceroute` sử dụng phương thức UDP protocol.

> syntax: traceroute < destination >

![](https://muirlandoracle.co.uk/wp-content/uploads/2020/03/image-15.png)

- Bạn có thể thấy ở ví dụ trên để đi từ `gateway` của bạn đến với máy chủ google chỉ định cần đi qua 13 máy chủ khác nhau.

1. What switch would you use to specify an interface when using Traceroute?: `-i`.
2. What switch would you use if you wanted to use TCP SYN requests when tracing the route?: `-T`.
3. Which layer of the TCP/IP model will traceroute run on by default (Windows)?: `Internet`.


## Task 7: (Networking tools) Whois

- `Whois` dùng để tìm một số thông tin về Domain nào đó như tên miền, công ty đăng kí tên miền đó, thời gian sửa đổi gần nhất, vv.

![](https://muirlandoracle.co.uk/wp-content/uploads/2020/03/image-16.png)

> syntax: whois < domain >

1. What is the registrant postal code for facebook.com?: `94025`.
2. When was the facebook.com domain first registered (Format: DD/MM/YYYY)?: `29/03/1997`.
3. Which city is the registrant based in?: `Redmond`.
4. What is the name of the golf course that is near the registrant address for microsoft.com?: `Bellevue Golf Course`.
5. What is the registered Tech Email for microsoft.com?: `msnhst@microsoft.com`.

## Task 8: (Networking tools) Dig

- `Dig` cho ta truy vấn thủ công đến các máy chủ đệ quy DNS để ta có thể biết thêm thông tin về nó.

> syntax: dig < domain > @ < dns-server-ip >

![](https://muirlandoracle.co.uk/wp-content/uploads/2020/03/dig-demo.png)

- Ta cần phải quan tâm đến một vài thông tin cơ bản như:
	+ `ANSWER` nó sẽ cho ta biết ta đã gửi đi 1 truy vấn và sẽ nhận được một câu trả lời đầy đủ bao gồm Domain Name và IP address của của lệnh truy vấn.
	+ `TTL` (Time To Live) của DNS record. Khi máy tính của ta thực hiện 1 truy vấn nào đó, nó sẽ lưu lại kết quả ở `local cache` và TTL sẽ cho ta biết thời gian tồn tại tối đa của dữ liệu được lưu trong `local cache`. Nếu quá thời gian, nó sẽ thực hiện lại yêu cầu đến dữ liệu cần truy vấn thay vì sử dụng lại bản sao được ghi ở `cache`. Đơn vị của TTL được tính bằng giây (biểu thị vùng khoanh đỏ).
	
![](https://muirlandoracle.co.uk/wp-content/uploads/2020/03/TTL.png)

1. What is DNS short for?: `Domain Name System`.
2. What is the first type of DNS server your computer would query when you search for a domain?: `Recursive`.
3. What type of DNS server contains records specific to domain extensions (i.e. .com, .co.uk*, etc)*? Use the long version of the name.: `Top-Level Domain`.
4. Where is the very first place your computer would look to find the IP address of a domain?: `Local cache`.
5. **_[Research]_** Google runs two public DNS servers. One of them can be queried with the IP 8.8.8.8, what is the IP address of the other one?: `8.8.4.4`.
6. If a DNS query has a TTL of 24 hours, what number would the dig query show?: `86400`.


























