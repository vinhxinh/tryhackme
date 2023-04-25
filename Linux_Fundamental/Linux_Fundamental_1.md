# Linux Fundamental 1

## Task 1: Introduction

![](https://assets.tryhackme.com/img/modules/linux-fundamentals.png)

## Task 2: A Bit of Background on Linux

- `Linux` được cho là hệ điều hành nhẹ hơn so với `Windows` và đã được sử dụng ở một số vật trong cuộc sống hàng ngày như là:
  + Thiết bị thông minh của xe oto, một số điện thoại di động.
  + Website thông thường.
  + Bảng điều khiển tín hiệu đèn giao thông và tín hiệu của các khu công nghiệp.
- `Linux` là hệ điều hành mã nguồn mở dựa trên `UNIX`. Vì nó là hệ điều hành mã nguồn mở nên nó có thể phù hợp với mọi loại thiết bị.
- Yêu cầu tối thiểu để chạy hệ thống là 512MB RAM.

1. **_Research_**: What year was the first release of a Linux operating system?: `1991`.

## Task 3: Interacting With Your First Linux Machine (In-Browser)

## Task 4: Running Your First few Commands

- Trái ngược với sự gọn nhẹ của hệ điều hành này đó là một số bất lợi như thông thường sẽ không có GUI(Graphical User Interface). Giống như `Windows` ta chỉ việc tương tác với các file hoặc phần mềm trên máy tính bằng việc _Click_ còn với `Linux` hầu như ta phải tương tác bằng `Terminal`.

Một số command cơ bản của `Linux`:
- `echo`: In ra màn hình một thứ bất kì mà ta truyền vào.
- `whoami`: Thông báo user nào đang được đăng nhập.

1. If we wanted to output the text "TryHackMe", what would our command be?: `echo TryHackMe`.
2. What is the username of who you're logged in as on your deployed Linux machine?: `tryhackme`.

## Task 5: Interacting With the Filesystem!

Một vài command giúp ta di chuyển giữa các thư mục với nhau:

| Command | Full Name               |
|---------|-------------------------|
| ls      | list                    |
| pwd     | print working directory |
| cat     | concatenate             |
| cd      | change directory        |

### ls

> Pro tips: Ta có thể list chủ đề của một file mà không cần dẫn trực tiếp đến file đó như sau: ls Pictures.

### cat

> Pro tips: Thay vì việc phải sử dụng cd để dẫn trực tiếp đến file cần cat thông tin thì ta có thể sử dụng cat + đường dẫn file từ thư mục home: cat /home/ubuntu/Documents/todo.txt

1. On the Linux machine that you deploy, how many folders are there?: `4`.
2. Which directory contains a file?: `folder4`.
3. What is the contents of this file?: `Hello World!`.
4. Use the cd command to navigate to this file and find out the new current working directory. What is the path?: `/home/tryhackme/folder4`.

## Task 6: Searching for Files

- Mỗi đường dẫn có thể chứa trong nó hàng ngàn đường dẫn khác nên việc đi vào từng thư mục và tìm kiếm là không thể. Vậy nên `Linux` đã cung cấp cho ta lệnh `find`.

Một số tham số cơ bản để sử dụng với `find`:

- Nếu ta chỉ nhớ tên file, ta có thể tìm kiếm với option `-name`: find -name passwords.txt . Và nó sẽ trả về path dẫn đến file ta cần tìm kiếm.
- Nếu muốn tìm kiếm theo đuôi file như .txt ta sẽ sử dụng: find -name *.txt . Và nó sẽ trả về cho ta tất cả các path dẫn đến file có đuôi .txt

### **grep**
- Để tìm một thông tin cụ thể có trong file đó hay không ta có thể sử dụng `grep`. 
- Ví dụ: grep "THM" access.log

### **wc**
- `wc` viết tắt của Word Count sử dụng để ta đếm số lượng từ có trong file ta truyền vào.

1. Use grep on "access.log" to find the flag that has a prefix of "THM". What is the flag?: `THM{ACCESS}.`

## Task 7: An Introduction to Shell Operators

### Operator "&"
- Toán tử "&" sẽ thực thi chương trình ta và chạy nó dưới background của terminal.
### Operator "&&"
- Toán tử "&&" sẽ được sử dụng để tạo ra một list các command nối liền vào nhau để chạy tuy nhiên điều kiện là nếu command trước chạy được thì command sau mới được thực thi.
- Ví dụ: command1 && command2. Nó sẽ được hiểu rằng command2 chỉ chạy khi command1 đã chạy thành công.
### Operator ">"
- Toán tử ">" cho phép truyền output của command ta thực thi đến một file nào đó.
- Ví dụ: echo hello > test1.txt. Sau đó cat test1.txt ta sẽ được dòng text "Hello". Lưu ý nếu file  test1.txt đã được tạo thì nó sẽ không tạo mới file test1.txt nữa mà thay vào đó viết đè nội dung lên luôn.
### Operator ">>"
- Toán tử ">>" có chức năng khá giống toán tử ">" tuy nhiên thay vì viết đè thông tin lên ta sẽ thêm thông tin đó và cuối của nội dung file đó.

1. If we wanted to run a command in the background, what operator would we want to use?: `&`.
2. If I wanted to replace the contents of a file named "passwords" with the word "password123", what would my command be?: `echo passwords > password123`.
3. Now if I wanted to add "tryhackme" to this file named "passwords" but also keep "passwords123", what would my command be: `echo tryhackme >> passwords`.

## Task 8:  Conclusions & Summaries





