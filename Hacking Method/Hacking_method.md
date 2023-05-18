# Hacking Methodology

## Task 1: Methodology Outline

Tất cả quá trình pentest được tổng hợp qua 6 bước:

1. Reconnaissance
2. Enumeration/Scanning
3. Gaining Access
4. Privilege Escalation
5. Covering Tracks
6. Reporting

1. What is the first phase of the Hacker Methodology?: `Reconnaissance`.

## Task 2: Reconnaissance Overview

Quá trình `Reconnaissance` sẽ thu thập thông tin ban đầu của mục tiêu mà không làm ảnh hưởng đến hệ thống hoặc hệ điều hành.

Một số công cụ sử dụng để tìm kiếm thông tin mục tiêu:
- Google
- Wiki
- Youtube
- Twitter
- LinkedIn
- PeopleFinder.com: Tìm thêm thông tin cá nhân khi có những thông tin cần thiết ban đầu như tên, địa chỉ, thành phố.
- who.is: Cung cấp thông tin về địa chỉ IP, tên miền, tổ chức và người sở hữu.
- sublist3r: Liệt kê toàn bộ subdomain của một tên miền cụ thể.
- hunter.io: Tìm kiếm có filter keyword.
- builtwith.com: Thông tin liên quan về website.
- wappalyzer: Cho biết web được build bằng ngôn ngữ nào và những ngôn ngữ nào được sử dụng bên cạnh nó.

1. Who is the CEO of SpaceX?: `Elon Musk`.
2. Do some research into the tool: sublist3r, what does it list?: `Subdomains`.
3. What is it called when you use Google to look for specific vulnerabilities or to research a specific topic of interest?: `Google Dorking`.

## Task 3: Enumeration and Scanning Overview

Đây là phần mà hacker sẽ tương tác với mục tiêu để liệt kê và xem xét tính khả thi của toàn bộ phương án tấn công.

`Attack Surface` xác định những gì mục tiêu có thể dễ bị tấn công trong giai đoạn `Exploit`. Các lỗ hổng bảo mật này có thể là nhiều thứ: bất kỳ thứ gì từ một trang web không được khóa đúng cách, một trang web rò rỉ thông tin, SQL Injection, Cross Site Scripting hoặc bất kỳ lỗ hổng nào khác.

Một vài tools hữu ích như:
- Nmap: Cho phép kiểm tra các port đang được mở và hệ điều hành sử dụng, dịch vụ nào đang được chạy và phiên bản của dịch vụ đó.
- dirb: Tìm kiếm tất cả các đường dẫn con của một website nào đó.
- dirbuster: giống dirb nhưng thiên về user interface
- enum4linux: Tool đặc biệt dành cho Linux để tìm kiếm lỗ hổng.
- metasploit: Tool để tìm kiếm lỗ hổng bên trong chứa rất nhiều tool hữu ích khác.
- Burp Suite: Kiểm soát lưu lượng mạng và thông tin truyền từ người dùng đến web server. Dùng để pentest.

1. What does enumeration help to determine about the target?: `attack surface`.
2. Do some reconnaissance about the tool: Metasploit, what company developed it?: `Rapid7`.
3. What company developed the technology behind the tool Burp Suite?: `PortSwigger`.

## Task 4: Exploitation

Bước này chỉ thực sự thành công khi bạn có một bước recon và scan thực sự tốt. Bởi nếu 2 bước trên bạn không đủ thông tin hay các phương thức tấn công, bạn sẽ bỏ qua nhiều cơ hội.

Một vài công cụ thường được dùng ở bước này:
- Metasploit
- Burp Suite
- SQLMap

1. What is one of the primary exploitation tools that pentester(s) use?: `Metasploit`.

## Task 5: Privilege Escalation

Leo quyền

Sau khi ta có quyền truy cập từ máy tính của nạn nhân, ta sẽ phải tìm cách để leo thang đặc quyền từ một lower user.
- Ở Window thường mục tiêu sẽ là: Admin hoặc System.
- Linux thường sẽ là `root` 

Việc tìm kiếm thông tin ban đầu về hệ điều hành là vô cùng quan trọng vì nó quyết định đến cách mà bạn leo quyền sau đó.

Một số cách leo quyền thông dụng:
- Cracking password hash để truy cập vào các user khác nhau.
- Tìm những lỗ hổng về dịch vụ hoặc phiên bản của dịch vụ để tiến hành khai thác.
- Password spraying.
- Attack by using credentials.
- Tìm kiếm secret keys để ssh sang những máy khác.
- Kiểm tra các thông tin cơ bản như `ifconfig`.
- Tìm những command hoặc file người dùng có thể truy cập dưới quyền `root` mà không cần xác minh.

1. In Windows what is usually the other target account besides Administrator?: `System`.
2. What thing related to SSH could allow you to login to another machine (even without knowing the username or password)?: `Keys`.

## Task 6: Covering Tracks

Xóa dấu vết.

## Task 7: Reporting

Viết báo cáo là bước cuối cùng của quá trình pentest

Đa phần nó sẽ phải đầy đủ các bước sau: 
- Tìm kiếm được gì và lỗ hổng gì.
- Những thông tin nghiêm trọng có được qua việc tìm kiếm
- Mô tả một cách tổng quan về cách phát hiện lỗi.
- Đề xuất cách khắc phục lỗi.

Một bản báo cáo bình thường sẽ có dạng: 

![](https://github.com/vinhxinh/tryhackme/blob/main/Hacking%20Method/pic1.png?raw=true)

1. What would be the type of reporting that involves a full documentation of all findings within a formal document?: `Full formal report`.
2. What is the other thing that a pentester should provide in a report beyond: the finding name, the finding description, the finding criticality: `Remediation Recommendation`.



