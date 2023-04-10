# HTTP in detail

---

## Task 1: What is HTTP(S)?

- Giao thức truyền tải siêu văn bản `HyperText Transfer Protocol` (HTTP) là giao thức chỉ định cách trình duyệt web và máy chủ web giao tiếp với nhau. Ví dụ trình duyệt web của bạn yêu cầu nội dung từ máy chủ web TryHackMe bằng giao thức HTTP khi bạn đi qua phòng này.
- *HTTP* là thứ được sử dụng bất cứ khi nào bạn xem một trang web, được phát triển bởi Tim Berners-Lee và nhóm của ông trong khoảng thời gian 1989-1991. HTTP là tập hợp các quy tắc được sử dụng để liên lạc với các máy chủ web để truyền dữ liệu trang web, cho dù đó là HTML, Hình ảnh, Video, v.v.
- *HTTPS* `HyperText Transfer Protocol Secure` là phiên bản bảo mật của HTTP. Dữ liệu HTTPS được mã hóa để mọi người không chỉ nhìn thấy dữ liệu bạn đang nhận và gửi mà còn đảm bảo với bạn rằng bạn đang nói chuyện với đúng máy chủ web chứ không phải thứ gì đó mạo danh nó.

1. What does HTTP stand for?: `HyperText Transfer Protocol`
2. What does the S in HTTPS stand for?: `Secure`
3. On the mock webpage on the right there is an issue, once you've found it, click on it. What is the challenge flag?: `THM{INVALID_HTTP_CERT}`


## Task 2: Requests And Responses (Yêu cầu và phản hồi)

- Khi chúng ta truy cập một trang web, trình duyệt của bạn sẽ cần gửi yêu cầu tới máy chủ web cho các nội dung như HTML, Images, và tải xuống các phản hồi. Trước đó, bạn cần cho trình duyệt biết cụ thể cách thức và vị trí truy cập các tài nguyên này, đây là lúc `URL` sẽ trợ giúp.

- *Uniform Resource Locator* (URL) là một tham chiếu đến tài nguyên web chỉ định vị trí của nó trên một mạng máy tính và cơ chế để truy xuất nó.

- Hình ảnh bên dưới hiển thị giao diện của một URL với tất cả các tính năng của nó (nó không sử dụng tất cả các tính năng trong mọi yêu cầu).

![](https://static-labs.tryhackme.cloud/sites/howhttpworks/newurl.png)

- *Scheme* (cơ chế): Phần này chỉ định đã sử dụng giao thức nào để truy cập tài nguyên, chẳng hạn như HTTP, HTTPS, FTP (Giao thức truyền tệp).
- User*: Một số dịch vụ yêu cầu xác thực để đăng nhập, bạn có thể đặt username và password vào URL để đăng nhập.
- *Host/Domain*: Tên Domain hoặc địa chỉ IP mà bạn muốn truy cập.
- *Port* (cổng): Port mà bạn chuẩn bị truy cập vào, thướng sẽ là 80 cho _HTTP_ và 443 cho _HTTPS_, nhưng chúng ta có thể thiết lập trong khoảng từ `0-65535`.
- *Path* (đường dẫn): Tên tệp hoặc vị trí của tài nguyên bạn đang cố truy cập.
- *Query String*: Bổ sung thêm thông tin ở đường dẫn yêu cầu. Ví dụ, `/blog?id=1` sẽ cho biết đường dẫn blog mà bạn muốn nhận bài viết trên blog với id là 1.
- *Fragment*: Đây là một tham chiếu đến một vị trí trên trang thực tế được yêu cầu. Điều này thường được sử dụng cho các trang có nội dung dài và có thể có một phần nhất định của trang được liên kết trực tiếp với nó để người dùng có thể xem được ngay khi họ truy cập trang.

### Making a Request

- Có thể gửi request tới máy chủ web chỉ bằng một dòng **"GET / HTTP/1.1"**
- Nhưng để có trải nghiệm web phong phú hơn, bạn cũng cần gửi các dữ liệu khác. Dữ liệu khác này được gửi trong cái được gọi là **_Header_**, trong đó tiêu đề chứa thông tin bổ sung để cung cấp cho máy chủ web mà bạn đang liên lạc.
![](https://static-labs.tryhackme.cloud/sites/howhttpworks/line.png)

#### Ví dụ 1:
```
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
```

Trong đó:
- Dòng 1: Yêu cầu đã gửi đi phương thức **GET**. yêu cầu truy cập home page với "/" và thể hiện với trang web rằng ta đang sử dụng giao thức HTTP phiên bản 1.1.
- Dòng 2: Cho biết web servers mà ta muốn.
- Dòng 3: Cho biết web brower nào đang được sử dụng.
- Dòng 4: Chúng tôi đang nói với máy chủ web rằng trang web đã giới thiệu chúng tôi đến trang này.
- Dòng 5: HTTP Request luôn kết thúc với một dòng trống để thông báo với web server rằng request đã hoàn thành.

#### Ví dụ 2:
```
HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98

<html>
<head>
    <title>TryHackMe</title>
</head>
<body>
    Welcome To TryHackMe.com
</body>
</html>
```

Trong đó:
- Dòng 1: HTTP 1.1 là phiên bản của giao thức HTTP mà máy chủ đang sử dụng và sau đó là Mã trạng thái HTTP trong trường hợp này là "200 Ok" cho chúng tôi biết yêu cầu đã hoàn tất thành công.
- Dòng 2: Điều này cho chúng tôi biết phần mềm máy chủ web và số phiên bản.
- Dòng 3: Ngày, giờ và múi giờ hiện tại của máy chủ web.
- Dòng 4: Tiêu đề Content-Type cho khách hàng biết loại thông tin nào sẽ được gửi, chẳng hạn như HTML, hình ảnh, video, pdf, XML.
- Dòng 5: Content-Length cho khách hàng biết thời gian phản hồi, bằng cách này, chúng tôi có thể xác nhận không có dữ liệu nào bị thiếu.
- Dòng 6: HTTP Request luôn kết thúc với một dòng trống để thông báo với web server rằng request đã hoàn thành.
- Dòng 7-14: Thông tin đã được yêu cầu, trong trường hợp này là trang chủ.

1. What HTTP protocol is being used in the above example?: `HTTP/1.1`
2. What response header tells the browser how much data to expect?: `Content-Length`


## Task 3: HTTP Methods

- **_HTTP methods_** là một cách để người dùng thể hiện hành động dự định của họ khi thực hiện HTTP request. Có rât nhiều HTTP methods nhưng chúng tôi sẽ đề cập đến những vấn đề phổ biến nhất, mặc dù hầu hết bạn sẽ giải quyết **GET** and **POST** method.

#### GET Request

- Được sử dụng để lấy thông tin từ một máy chủ web.

#### POST Request

- Điều này được sử dụng để gửi dữ liệu đến máy chủ web và có khả năng tạo bản ghi mới.

#### PUT Request

- Được sử dụng để gửi dữ liệu đến máy chủ web để cập nhật thông tin.

#### DELETE Request

- Được sử dụng để xóa thông tin/bản ghi khỏi máy chủ web.

1. What method would be used to create a new user account?: `POST`
2. What method would be used to update your email address?: `PUT`
3. What method would be used to remove a picture you've uploaded to your account?: `DELETE`
4. What method would be used to view a news article?: `GET`

## Task 4: HTTP Status Codes

### HTTP Status Codes:

- Trong nhiệm vụ trước, bạn đã biết rằng khi máy chủ HTTP phản hồi, dòng đầu tiên luôn chứa mã trạng thái thông báo cho máy khách về kết quả yêu cầu của họ và cũng có thể là cách xử lý yêu cầu đó. Các mã trạng thái này có thể được chia thành 5 phạm vi khác nhau:

|  |  |
|---|---|
| 100-199 - Information Response | Chúng được gửi để báo cho khách hàng biết phần đầu tiên của yêu cầu của họ đã được chấp nhận và họ nên tiếp tục gửi phần còn lại của yêu cầu. Những mã này không còn phổ biến nữa. |
| 200-299 - Success | Phạm vi mã trạng thái này được sử dụng để thông báo cho người dùng rằng yêu cầu của họ đã thành công. |
| 300-399 - Redirection | Chúng được sử dụng để chuyển hướng yêu cầu của khách hàng đến một tài nguyên khác. Đây có thể là một trang web khác hoặc một trang web khác hoàn toàn. |
| 400-499 - Client Errors | Được sử dụng để thông báo cho khách hàng rằng có lỗi với yêu cầu của họ. |
| 500-599 - Server Errors | Điều này được dành riêng cho các lỗi xảy ra ở phía máy chủ và thường chỉ ra một vấn đề khá lớn với máy chủ xử lý yêu cầu. |

### Common HTTP Status Codes:

- Có rất nhiều mã trạng thái HTTP khác nhau và chúng ta sẽ xem xét các phản hồi HTTP phổ biến nhất mà bạn có thể gặp phải:

|  |  |
|---|---|
| 200 - OK | Yêu cầu đã được hoàn thành thành công. |
| 201 - Created | Tài nguyên đã được tạo (ví dụ: người dùng mới hoặc bài đăng blog mới). |
| 301 - Permanent Redirect | Điều này chuyển hướng trình duyệt của khách hàng đến một trang web mới hoặc thông báo cho các công cụ tìm kiếm rằng trang này đã được chuyển đến một nơi khác và thay vào đó hãy tìm ở đó. |
| 302 - Temporary Redirect | Tương tự như chuyển hướng vĩnh viễn ở trên, nhưng đúng như tên gọi, đây chỉ là thay đổi tạm thời và nó có thể thay đổi lại trong thời gian tới. |
| 400 - Bad Request | Điều này cho trình duyệt biết rằng có điều gì đó sai hoặc thiếu trong yêu cầu của họ. Điều này đôi khi có thể được sử dụng nếu tài nguyên máy chủ web đang được yêu cầu mong đợi một tham số nhất định mà máy khách không gửi. |
| 401 - Not Authorised | Bạn hiện không được phép xem tài nguyên này cho đến khi bạn đã ủy quyền với ứng dụng web, phổ biến nhất là bằng tên người dùng và mật khẩu. |
| 403 - Forbidden | Bạn không có quyền xem tài nguyên này cho dù bạn có đăng nhập hay không. |
| 405 - Method Not Allowed | Tài nguyên không cho phép yêu cầu phương thức này, bạn gửi yêu cầu GET tới tài nguyên /create-account khi nó mong đợi một yêu cầu POST thay thế. |
| 404 - Page Not Found | Trang/tài nguyên bạn yêu cầu không tồn tại. |
| 500 - Internal Service Error | Máy chủ đã gặp một số loại lỗi với yêu cầu của bạn khiến nó không biết cách xử lý đúng cách. |
| 503 - Service Unavailable | Máy chủ này không thể xử lý yêu cầu của bạn vì nó bị quá tải hoặc ngừng hoạt động để bảo trì. |

1. What response code might you receive if you've created a new user or blog post article?: `201`
2. What response code might you receive if you've tried to access a page that doesn't exist?: `404`
3. What response code might you receive if the web server cannot access its database and the application crashes?: `503`
4. What response code might you receive if you try to edit your profile without logging in first?: `401`


## Task 5: Headers

- **_Header_** đề cập đến dữ liệu bổ sung được đặt ở đầu khối dữ liệu đang được lưu trữ hoặc truyền đi. Trong truyền dữ liệu, dữ liệu theo sau tiêu đề đôi khi được gọi là tải trọng hoặc nội dung.
- 