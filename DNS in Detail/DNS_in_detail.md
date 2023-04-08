# DNS in detail

---

## Task 1: What is DNS?

- DNS là viết tắt của cụm từ Domain Name System, mang ý nghĩa đầy đủ là hệ thống phân giải tên miền. Hiểu một cách ngắn gọn nhất, DNS cơ bản là một hệ thống chuyển đổi các tên miền website mà chúng ta đang sử dụng, ở dạng `www.tenmien.com` sang một địa chỉ IP dạng số tương ứng với tên miền đó và ngược lại.
- Khi mà ta muốn truy cập website, chúng ta khó có thể nhớ chính xác dãy số của địa chỉ IP, điều mà DNS có thể giúp đỡ ta.
- Địa chỉ IP có dạng `104.26.10.229`, 4 bộ chữ số từ 0-255 được phân chia bởi dấu `"."`.
![](https://assets.tryhackme.com/additional/dnsindetail/ip2domaindrawing.png)

1. What does DNS stand for?: `Domain Name System`


## Task 2: Domain Hierarchy (Hệ thống cấp bậc Domain)

![](https://assets.tryhackme.com/additional/dnsindetail/domain_levels.png)

- Top-Level Domain(TLD) là phần bên phải ngoài cùng của tên miền. Ví dụ `tryhackme.com` thì nó sẽ là `.com`.
  - Có 2 loại TLD đó là gTLD (Generic) và ccTLD (Country code)
  - gTLD được dùng để cho người dùng biết mục đích của tên miền; ví dụ: .com sẽ dành cho mục đích thương mại, .org dành cho tổ chức, .edu dành cho giáo dục và .gov dành cho chính phủ. 
  - ccTLD đã được sử dụng cho các mục đích địa lý, ví dụ: .ca cho các trang web có trụ sở tại Canada, .co.uk cho các trang web có trụ sở tại Vương quốc Anh, v.v.

- Second-Level Domain là `tryhackme` trong `tryhackme.com`. Khi đăng kí tên miền, Second-Level Domain bị giới hạn 63 kí tự + TLD là chỉ có thể sử dụng `[a-z] 0-9 -` (không thể bắt đầu hay kết thúc bằng dấu gạch nối hoặc nhiều dấu gạch nối liên tục)

- Subdomain là phần nằm bên trái của `Second-Level Domain` sử dụng dấu "." để phân tách nó. Ví dụ `admin.tryhackme.com` thì `admin` chính là Subdomain . Subdomain khi tạo cũng sẽ có giới hạn giống như Second-Level Domain, tuy nhiên ta có thể nối nhiều subdomain bằng cách chia nó bằng các dấu ".", độ dài cũng không được vượt quá 253 kí tự. Ví dụ `jupiter.servers.tryhackme.com`.

1. What is the maximum length of a subdomain?: `63`
2. Which of the following characters cannot be used in a subdomain ( 3 b _ - )?: `_`
3. What is the maximum length of a domain name?: `253`
4. What type of TLD is .co.uk?: `ccTLD`


## Task 3: Record Types

DNS không chỉ dành cho các trang web mà nó tồn tại nhiều loại bản ghi DNS khác. Ta sẽ điểm qua một số bản ghi phổ biến nhất mà bạn có thể gặp phải.

- A Record: Bản ghi này phân giải thành địa chỉ IPv4 (104.26.10.229)
- AAAA Record: Bản ghi này phân giải thành địa chỉ IPv6 (2606:4700:20::681a:be5)
- CNAME Record: Là một bản ghi trỏ đến một tên miền khác chứ không trỏ trực tiếp đến một địa chỉ IP. Khi chỉnh sửa chỉ cần chỉnh sửa ở bản ghi A còn các CNAME sẽ tự thay đổi theo. Ví dụ bạn có 2 tên miền `vietnix.vn` và `www.vietnix.com`. Bản ghi A cho `vietnix.vn` sẽ trỏ đến địa chỉ IP của server của bản ghi CNAME cho `www.vietnix.vn` trỏ đến `vietnix.vn`.
- TXT Record: Bản ghi TXT cho phép bạn thêm các hướng dẫn cả người và máy có thể đọc được. Loại record này phục vụ nhiều mục đích khác nhau, bao gồm ngăn chặn spam email, xác minh quyền sở hữu miền và các chính sách khung, cũng như cung cấp thông tin chung và đầu mối liên hệ về miền.
- MX Record: Bản ghi MX là bản ghi thực hiện việc định vị máy chủ mail cho tên miền đó. Với mỗi tên miền ta có thể gắn nhiều MX Record. Những bản ghi này cũng sẽ được gắn cờ ưu tiên, khi máy chủ chính gặp sự cố và email cần được gửi vào backup server.

1. What type of record would be used to advise where to send email?: `MX`
2. What type of record handles IPv6 addresses?: `AAAA`


## Task 4: Making A Request

![](https://assets.tryhackme.com/additional/dnsindetail/dns.png)

Điều gì xảy ra khi bạn thực hiện một Request DNS

- Khi bạn yêu cầu một tên miền, trước tiên, máy tính của bạn sẽ kiểm tra bộ nhớ cache cục bộ của nó để xem gần đây bạn đã tra cứu địa chỉ chưa; nếu không, một yêu cầu tới Máy chủ DNS đệ quy của bạn sẽ được thực hiện.

- Máy chủ DNS đệ quy thường được cung cấp bởi ISP của bạn, nhưng bạn cũng có thể chọn máy chủ của riêng mình. Máy chủ này cũng có bộ đệm cục bộ chứa các tên miền được tra cứu gần đây. Nếu tìm thấy kết quả cục bộ, kết quả này sẽ được gửi trở lại máy tính của bạn và yêu cầu của bạn sẽ kết thúc tại đây (điều này phổ biến đối với các dịch vụ phổ biến và được yêu cầu nhiều như Google, Facebook, Twitter). Nếu không thể tìm thấy yêu cầu cục bộ, một hành trình sẽ bắt đầu tìm câu trả lời chính xác, bắt đầu với các máy chủ DNS gốc của internet.

- Các máy chủ gốc đóng vai trò là xương sống DNS của internet; công việc của họ là chuyển hướng bạn đến đúng Máy chủ miền cấp cao nhất, tùy thuộc vào yêu cầu của bạn. Ví dụ: nếu bạn yêu cầu `www.tryhackme.com` , máy chủ gốc sẽ nhận ra Miền cấp cao nhất của `.com` và ưu tiên bạn đến đúng máy chủ TLD xử lý các địa chỉ `.com`.

- Máy chủ TLD lưu giữ các bản ghi về nơi tìm máy chủ có thẩm quyền để trả lời yêu cầu DNS . Máy chủ có thẩm quyền thường còn được gọi là máy chủ định danh cho miền. Ví dụ: máy chủ định danh cho `tryhackme.com` là `kip.ns.cloudflare.com` và `uma.ns.cloudflare.com` . Bạn sẽ thường tìm thấy nhiều máy chủ định danh cho một tên miền để hoạt động như một phương án dự phòng trong trường hợp một máy chủ bị hỏng.

- Máy chủ DNS có thẩm quyền là máy chủ chịu trách nhiệm lưu trữ bản ghi DNS cho một tên miền cụ thể và là nơi thực hiện mọi cập nhật đối với bản ghi DNS tên miền của bạn. Tùy thuộc vào loại bản ghi, bản ghi DNS sau đó được gửi trở lại Máy chủ DNS đệ quy, nơi một bản sao cục bộ sẽ được lưu vào bộ nhớ cache cho các yêu cầu trong tương lai, sau đó được chuyển tiếp trở lại máy khách ban đầu đã thực hiện yêu cầu. Tất cả các bản ghi DNS đều có giá trị `TTL` (Time to live). Giá trị này là một số được biểu thị bằng giây mà phản hồi sẽ được lưu cục bộ cho đến khi bạn phải tra cứu lại. Bộ nhớ đệm giúp tiết kiệm việc phải thực hiện yêu cầu DNS mỗi khi bạn giao tiếp với máy chủ.

1. What field specifies how long a DNS record should be cached for?: `TTL`
2. What type of DNS Server is usually provided by your ISP?: `Recursive`
3. What type of server holds all the records for a domain?: `Authoritative`


## Task 5: Practical

1. What is the CNAME of shop.website.thm?: `shops.myshopify.com` (nslookup --type=CNAME shop.website.thm)
2. What is the value of the TXT record of website.thm?: `THM{7012BBA60997F35A9516C2E16D2944FF}` (nslookup --type=TXT website.thm)
3. What is the numerical priority value for the MX record?: `30` (nslookip --type=MX website.thm)
4. What is the IP address for the A record of `www.website.thm`?: `10.10.10.10`(nslookup --type=A `www.website.thm`)


