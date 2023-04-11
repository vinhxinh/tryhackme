# How websites work

---

## Task 1: How websites work

- Khi kết thúc phòng này, bạn sẽ biết cách các trang web được tạo và sẽ được giới thiệu về một số vấn đề bảo mật cơ bản.
- Khi bạn truy cập một trang web, trình duyệt của bạn (như Safari hoặc Google Chrome) sẽ gửi yêu cầu tới máy chủ web để yêu cầu thông tin về trang bạn đang truy cập. Nó sẽ phản hồi với dữ liệu mà trình duyệt của bạn sử dụng để hiển thị trang cho bạn; máy chủ web chỉ là một máy tính chuyên dụng ở một nơi khác trên thế giới xử lý các yêu cầu của bạn.

![](https://github.com/vinhxinh/tryhackme/blob/main/How_Website_Work/pic1_task1.png?raw=true)

- Có 2 thành phần chính để tạo nên 1 website:
  - **_Front-End_**(Client-Side): Cách mà trình duyệt của bạn hiển thị 1 trang web nào đó.
  - **_Back-End_**(Server-Side): Một máy chủ xử lý yêu cầu của bạn và trả về phản hồi.

- Có nhiều quy trình khác liên quan đến trình duyệt của bạn khi đưa ra yêu cầu tới máy chủ web, nhưng hiện tại, bạn chỉ cần hiểu rằng bạn đưa ra yêu cầu tới máy chủ và máy chủ sẽ phản hồi dữ liệu mà trình duyệt của bạn sử dụng để hiển thị thông tin cho bạn.


1. What term best describes the component of a web application rendered by your browser?: `front end`


## Task 2: HTML (Hypertext Markup Language)

- Một websites được tạo ra chủ yếu sử dụng:
  - **_HTML_**: để xây dựng trang web và xác định cấu trúc của chúng
  - **_CSS_**: Làm cho website trông đặc sắc hơn bởi việc thêm các tùy chọn `styling`
  - **_JavaScript_**: triển khai các tính năng phức tạp trên các trang bằng tính tương tác.

- *HyperText Markup Language* (HTML) is the language websites are written in. Elements(hay còn được gọi là `tags`) là các khối xây dựng của các trang HTML và cho trình duyệt biết cách hiển thị nội dung. 

![](https://github.com/vinhxinh/tryhackme/blob/main/How_Website_Work/pic1_task2.png?raw=true)

- Cấu trúc của HTML của ảnh trên dựa theo các thành phần như sau:
  - `<!DOCTYPE html>` định nghĩa rằng trang này là một trang tài liệu HTML5. Điều này giúp tiêu chuẩn hóa giữa các trình duyệt khác nhau và thông báo với trình duyệt rằng hãy sử dụng HTML5 để biểu diễn trang.
  - Thành phần `<html>` là một thành phần gốc của trang HTML, tất cả những thành phần khác đều xuất hiện sau thành phần này.
  - Thành phần `<head>` bao gồm thông tin về trang(thường sẽ là title của trang đó).
  - Thành phần `<body>` định nghĩa phần thân của một trang HTML. Chỉ những chủ đề bên trong `body` mới được hiện thỉ ở trình duyệt.
  - Thành phần `<h1>` hiện thị tiêu đề lớn.
  - Thành phần `<p>` định nghĩa một đoạn văn bản.
  - Còn rất nhiều thành phần (thẻ `tags`) khác được sử dụng cho nhiều mục đích khác nhau. Ví dụ, tags cho button `<button>`, tags cho ảnh `<image>`, ... 

- Các thẻ có thể chứa các thuộc tính, chẳng hạn như thuộc tính lớp có thể được sử dụng để tạo kiểu cho một phần tử (ví dụ: làm cho thẻ có màu khác) `<p class="bold-text">` hoặc thuộc tính src được sử dụng trên hình ảnh để chỉ định vị trí của một hình ảnh: `<img src="img/cat.png">`. Mỗi thành phần có thể có nhiêu thuộc tính trong nó tùy vào những mục đích khác nhau. Ví dụ `<p attribute1="value1" attribute2="value2">`.
- Các thành phần cũng có thuộc tính id `<p id="example">` để định danh thành phần đó. Thành phần id được sử dụng cho `styling` và nó được nhận dạng bởi JavaScript. Id giống như tên một hàm con được ta chỉ định vào trong từng thành phần muốn sử dụng hàm con đó. Còn hàm con đó sẽ được viết ở trong CSS.

1. One of the images on the cat website is broken - fix it, and the image will reveal the hidden text answer!: `HTMLHERO`.
2. Add a dog image to the page by adding another img tag (`<img>`) on line 11. The dog image location is img/dog-1.png. What is the text in the dog image?: `DOGHTML`.


## Task 3: JavaScript (JS)

- **_JavaScript_** (JS) là một trong những ngôn ngữ mã hóa phổ biến nhất trên thế giới và cho phép các trang trở nên tương tác. HTML được sử dụng để tạo cấu trúc và nội dung trang web, trong khi JavaScript được sử dụng để kiểm soát chức năng của các trang web - nếu không có JavaScript, một trang sẽ không có các yếu tố tương tác và sẽ luôn ở trạng thái tĩnh. JS có thể tự động cập nhật trang theo thời gian thực, cung cấp chức năng thay đổi kiểu nút khi một sự kiện cụ thể trên trang xảy ra (chẳng hạn như khi người dùng nhấp vào nút) hoặc để hiển thị hoạt ảnh chuyển động.

- JavaScript có thể được thêm vào trong source code của page và có thể được tải lên bởi thẻ `<script>` hoặc có thể được chỉ định bằng thuộc tính `src`.

> `<script src="/location/of/javascript_file.js"></script>`

- Nếu muốn chạy script mà không muốn để trong thẻ HTML thì ta phải sử dụng như sau:

> `<script> document.getElementById("demo").innerHTML = "Hack the Planet"; </script>`

- Nếu không muốn khai báo trong thẻ `<script>` thì ta phải sử dụng như thuộc tính trong thẻ thành phần của HTML như sau:  

> `<button onclick='document.getElementById("demo").innerHTML = "Hack the Planet";'> Click me! </button>`


1. Click the "View Site" button on this task. On the right-hand side, add JavaScript that changes the demo element's content to "Hack the Planet": `JSISFUN` (`document.getElementById("demo").innerHTML = "Hack the Planet";`).
2. Add the button HTML from this task that changes the element's text to "Button Clicked" on the editor on the right, update the code by clicking the "Render HTML+JS Code" button and then click the button. 
(`<button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>Click Me!</button>`)


## Task 4: Sensitive Data Exposure

- Lộ dữ liệu nhạy cảm xảy ra khi một trang web không bảo vệ (hoặc xóa) đúng cách thông tin văn bản rõ ràng nhạy cảm cho người dùng cuối; thường được tìm thấy trong mã nguồn lối vào của một trang web.
- Bây giờ chúng ta biết rằng các trang web được xây dựng bằng cách sử dụng nhiều phần tử HTML (thẻ), tất cả những phần tử này chúng ta có thể thấy chỉ bằng cách "xem nguồn trang". Nhà phát triển trang web có thể đã quên xóa thông tin xác thực đăng nhập, liên kết ẩn đến các phần riêng tư của trang web hoặc dữ liệu nhạy cảm khác được hiển thị bằng HTML hoặc JavaScript.

![](https://github.com/vinhxinh/tryhackme/blob/main/How_Website_Work/pic1_task4.png?raw=true)

1. View the website on this task. What is the password hidden in the source code?: `testpasswd`.


## Task 5: HTML Injection

- **HTML Injection** là một lỗ hổng xảy ra khi đầu vào của người dùng chưa được lọc được hiển thị trên trang. Nếu một trang web không làm sạch đầu vào của người dùng (lọc bất kỳ văn bản "độc hại" nào mà người dùng nhập vào một trang web) và thông tin đầu vào đó được sử dụng trên trang, thì kẻ tấn công có thể đưa mã HTML vào một trang web dễ bị tấn công.

![](https://github.com/vinhxinh/tryhackme/blob/main/How_Website_Work/pic1_task5.png?raw=true)

- Hình ảnh trên cho thấy cách một biểu mẫu xuất văn bản ra trang. Nội dung người dùng nhập vào trường "Tên bạn là gì" sẽ được chuyển đến một hàm JavaScript và xuất ra trang, nghĩa là nếu người dùng thêm HTML hoặc JavaScript của riêng họ vào trường, thì nó được sử dụng trong hàm sayHi và được thêm vào trang - điều này có nghĩa là bạn có thể thêm HTML của riêng mình (chẳng hạn như thẻ `<h1>`) và nó sẽ xuất đầu vào của bạn dưới dạng HTML thuần túy.

1. View the website on this task and inject HTML so that a malicious link to http://hacker.com is shown.: `HTML_INJ3CTI0N`. (`<a href="http://hacker.com"> Vinh </a>`)

