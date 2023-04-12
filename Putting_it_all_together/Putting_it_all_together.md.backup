# Putting It All Together

---

## Task 1: Putting It All Together (Overview)

- Tóm lại, khi bạn yêu cầu một trang web, máy tính của bạn cần biết địa chỉ IP của máy chủ mà nó cần giao tiếp; đối với điều này, nó sử dụng DNS. Sau đó, máy tính của bạn giao tiếp với máy chủ web bằng cách sử dụng một bộ lệnh đặc biệt được gọi là giao thức HTTP; sau đó máy chủ web trả về HTML, JavaScript, CSS, Hình ảnh, v.v. mà trình duyệt của bạn sau đó sẽ sử dụng để định dạng chính xác và hiển thị trang web cho bạn.

![](https://github.com/vinhxinh/tryhackme/blob/main/Putting_it_all_together/task1_pic1.png?raw=true)


## Task 2: Other Components

### Load Balancers (Cân bằng tải)

- Khi lưu lượng truy cập của một trang web bắt đầu trở nên khá lớn hoặc đang chạy một ứng dụng cần có tính khả dụng cao, một máy chủ web có thể không thực hiện được công việc nữa. Bộ cân bằng tải cung cấp hai tính năng chính, đảm bảo các trang web có lưu lượng truy cập cao có thể xử lý tải và cung cấp khả năng chuyển đổi dự phòng nếu máy chủ không phản hồi. Khi bạn yêu cầu một trang web có bộ cân bằng tải, bộ cân bằng tải sẽ nhận yêu cầu của bạn trước rồi chuyển tiếp đến một trong nhiều máy chủ đằng sau nó.
- Những bộ cân bằng tải sẽ sử dụng những thuật toán khác nhau để quyết định máy chủ nào tốt nhất để xử lý yêu cầu, một trong những thuật toán thông dụng nhất là **_Round-Robin_** (thuật toán quay vòng).
- Bộ cân bằng tải cũng thực hiện kiểm tra định kỳ với từng máy chủ để đảm bảo chúng đang chạy chính xác; đây được gọi là **_health check_**. Nếu máy chủ không phản hồi thích hợp hoặc không phản hồi, bộ cân bằng tải sẽ ngừng gửi lưu lượng truy cập cho đến khi nó phản hồi lại một cách thích hợp.

![](https://github.com/vinhxinh/tryhackme/blob/main/Putting_it_all_together/task2_pic1.png?raw=true)

### Content Delivery Networks (CDN)

- CDN có thể là một nguồn tài nguyên tuyệt vời để cắt giảm lưu lượng truy cập vào một trang web bận rộn. Nó cho phép bạn lưu trữ các tệp tĩnh từ trang web của mình, chẳng hạn như JavaScript, CSS, Hình ảnh, Video và lưu trữ chúng trên hàng nghìn máy chủ trên toàn thế giới. Khi người dùng yêu cầu một trong các tệp được lưu trữ, CDN sẽ tìm ra vị trí thực tế của máy chủ gần nhất và gửi yêu cầu ở đó thay vì lấy từ máy chủ gốc có khả năng là bên kia thế giới.


### Databases 

- Thông thường các trang web sẽ cần một cách lưu trữ thông tin cho người dùng của họ. Máy chủ web có thể giao tiếp với cơ sở dữ liệu để lưu trữ và gọi lại dữ liệu từ chúng. Cơ sở dữ liệu có thể bao gồm từ một tệp văn bản thuần túy đơn giản cho đến các cụm phức tạp gồm nhiều máy chủ.
- Bạn sẽ bắt gặp một số cơ sở dữ liệu phổ biến: `MySQL, MSSQL, MongoDB, GraphQL, Postgres, v.v` mỗi cái đều có các tính năng cụ thể của nó.

### Web Application Firewall (WAF)

- WAF nằm giữa yêu cầu web của bạn và máy chủ web; mục đích chính của nó là bảo vệ máy chủ web khỏi bị hack hoặc tấn công từ chối dịch vụ. Nó phân tích các yêu cầu web để biết các kỹ thuật tấn công phổ biến, cho dù yêu cầu đó là từ một trình duyệt thực chứ không phải bot.
- Nó cũng kiểm tra xem có quá nhiều yêu cầu web được gửi hay không bằng cách sử dụng thứ gọi là `rate limiting`, điều này sẽ chỉ cho phép một lượng yêu cầu nhất định từ một IP mỗi giây. Nếu một yêu cầu được coi là một cuộc tấn công tiềm ẩn, nó sẽ bị loại bỏ và không bao giờ được gửi đến máy chủ web.

![](https://github.com/vinhxinh/tryhackme/blob/main/Putting_it_all_together/task2_pic2.png?raw=true)

1. What can be used to host static files and speed up a clients visit to a website?: `CDN`.
2. What does a load balancer perform to make sure a host is still alive?: `health check`.
3. What can be used to help against the hacking of a website?: `WAF`.


### Task 3: How Web Servers Work

### Web Server

- Máy chủ web là một phần mềm lắng nghe các kết nối đến và sau đó sử dụng giao thức HTTP để cung cấp nội dung web cho các máy khách của nó. Phần mềm máy chủ web phổ biến nhất mà bạn sẽ gặp là _Apache_, _Nginx_, _IIS_ và _NodeJS_. Một máy chủ Web cung cấp các tệp từ cái được gọi là thư mục gốc của nó, được xác định trong cài đặt phần mềm.

### Virtual host

- Máy chủ web có thể lưu trữ nhiều trang web với các tên miền khác nhau; để đạt được điều này, họ sử dụng máy chủ ảo(virtual host). Phần mềm máy chủ web kiểm tra tên máy chủ được yêu cầu từ các tiêu đề HTTP và khớp với tên máy chủ ảo của nó (máy chủ ảo chỉ là các tệp cấu hình dựa trên văn bản). Nếu tìm thấy kết quả phù hợp, trang web chính xác sẽ được cung cấp. Nếu không tìm thấy kết quả phù hợp, trang web mặc định sẽ được cung cấp để thay thế.
- Không có giới hạn về số lượng trang web khác nhau mà bạn có thể lưu trữ trên máy chủ web.

### Static Vs Dynamic Content

- Nội dung tĩnh (Static Content), như tên cho thấy, là nội dung không bao giờ thay đổi. Các ví dụ phổ biến về điều này là hình ảnh, javascript, CSS, v.v., nhưng cũng có thể bao gồm HTML không bao giờ thay đổi. Hơn nữa, đây là những tệp được cung cấp trực tiếp từ máy chủ web mà không có thay đổi nào đối với chúng.
- Mặt khác, nội dung động (Dynamic Content) là nội dung có thể thay đổi theo các yêu cầu khác nhau. Lấy ví dụ, một blog. Trên trang chủ của blog, nó sẽ hiển thị cho bạn các mục mới nhất. Nếu một mục mới được tạo, thì trang chủ sẽ được cập nhật với mục mới nhất hoặc ví dụ thứ hai có thể là một trang tìm kiếm trên blog. Tùy thuộc vào từ bạn tìm kiếm, các kết quả khác nhau sẽ được hiển thị.
- `BackEnd` là những thứ được xử lý ở đằng sau, bạn sẽ không thể xem được cái gì đang xảy ra và không thể xem được source HTML
- `FrontEnd` là tất cả những gì bạn có thể thấy được như là kết quả xử lý của `BackEnd` hoặc trên trình duyệt.

Một ví dụ PHP rất cơ bản về điều này sẽ là nếu bạn yêu cầu trang web `http://example.com/index.php?name=adam`
- Có đoạn `index.php` được xây dựng như sau:
 
  ``` 
  <html> <body>Hello <?php echo $_GET["name"]; ?></body></html>
  ```
- Nó sẽ xuất ra như thế này cho người dùng thấy được: 
  ```
  <html><body>Hello adam</body></html>
  ```
  
- Lưu ý rằng người dùng không thể thấy bất cứ code PHP nào vì nó ở trong `BackEnd`.


1. What does web server software use to host multiple sites?: `Virtual Host`.
2. What is the name for the type of content that can change?: `Dynamic`.
3. Does the client see the backend code? Yay/Nay: `Nay`.


## Task 4: Quiz

- Thứ tự hoạt động của một Request đối với trang web:	

1. Yêu cầu Domain Name ở trình duyệt của bạn.
2. Kiểm tra Local Cache ở trình duyệt nếu như bạn đã từng truy cập vào tên miền này rồi, nó sẽ lưu lại những thông tin, thói quen ở lần truy cập trước.
3. Tìm kiếm những Domain Name phù hợp cho địa chỉ IP đó. 
4. Truy vấn từ server gốc xem những Domain Name nào mà người dùng có thẩm quyền được truy cập.
5. Những DNS có thẩm quyền sẽ đưa lại 1 địa chỉ IP để truy cập website.
6. Request sẽ phải thông qua được WAF(Web Application Firewall).
7. Tiếp theo Request sẽ phải thông qua bộ cân bằng tải (Load Balancer).
8. Kết nối đến server thông qua port 80 hoặc 443.
9. Máy chủ web nhận được yêu cầu `GET` request.
10. `Web Application` giao tiếp với `Databases`.
11. Trình duyệt của bạn sẽ xuất HTML ra hình ảnh mà con người có thể xem được web.
	



