# Linux Fundamental 2

---

## Task 1: Introduction

Ở phần 2 này chúng ta này sẽ:
- Tìm hiểu thêm về một số cách thao tác với file, filesystem và một số command để copy hoặc di chuyển file.
- Giới thiệu cách để bảo vệ file và thư mục an toàn.
- Nhận dạng được thứ gì đã được người dùng gần nhất truy cập vào.
- Thực thi một vài scripts.

## Task 2: Accessing Your Linux Machine Using SSH (Deploy)

What is SSH & how Does it Work?

- `ssh` (secure shell) là một giao thức giữa máy tính bằng cách sử dụng mã hóa thông tin trước khi được gửi lên Internet và chuyển thể thành một văn bản có thể đọc được trước khi đến máy tính được truy cập từ xa.
- `ssh` cho phép thực thi những command trên thiết bị từ xa.

## Task 3: Introduction to Flags and Switches

- Phần lớn các command của `Linux` cho phép ta truyền thêm các tham số vào. 
- Phần có gạch nối được gọi là flags/switches. Tiếp sau đó là tham số truyền vào.

- Ví dụ: Nếu ta chỉ sử dụng lệnh `ls` thì ta chỉ thấy được một số file. Nhưng nếu sử dụng `ls` -a (--all) thì ta có thể thấy được những file đang được ẩn đi (.hidden files).

- Sử dụng `-h` (command + -h) để xem hướng dẫn sử dụng của bất kì command nào hoặc sử dụng `man` + tên command để xem tài liệu đầy đủ về command đó.

1. What directional arrow key would we use to navigate down the manual page?: `Down`.
2. What flag would we use to display the output in a "human-readable" way?: `-h`.

## Task 4: Filesystem Interaction Continued

Một số command để thao tác với file system:

| Command | Full name      | Purpose                      |
|---------|----------------|------------------------------|
| touch   | touch          | Create file                  |
| mkdir   | make directory | Create a folder              |
| cp      | copy           | Copy a file or folder        |
| mv      | move           | Move a file or folder        |
| rm      | remove         | Remove a file or folder      |
| file    | file           | Determine the type of a file |

> Pro Tips: Tất cả các lệnh trên có thể dẫn full path giống như lệnh `cat` thay vì ngồi cd đến chính xác nơi lưu file đó.

- Để xóa đi một directory ta cần thêm -R.

1. How would you create the file named "newnote"?: `touch newnote`.
2. On the deployable machine, what is the file type of "unknown1" in "tryhackme's" home directory?: `ASCII text`.
3. How would we move the file "myfile" to the directory "myfolder": `mv myfile myfolder`.
4. What are the contents of this file?: `THM{FILESYSTEM}`.

## Task 5: Permissions 101

- Khi ta sử dụng lệnh `ls -l` hoặc `ll` ta sẽ thấy được một bảng đầy đủ trong đó có:
 
 ![]()

Trong đó ta cần quan tâm đến:
- Phần `-` đầu tiên nếu nó là dấu `-` thì có nghĩa nó là file còn nếu là `d` thì nó là đường dẫn (folder).
- 3 phần gạch `-` tiếp theo biểu thị cho permission của user sở hữu file đó đối với file đó 
  - `r` là có quyền đọc file.
  - `w` là có quyền chỉnh sửa file.
  - `x` là có quyền thực thi file.
  - Nếu ở vị trí tương ứng mà vẫn có dấu `-` thì nghĩa là nó không có quyền làm điều đó.
- 3 phần gạch `-` tiếp theo biểu thị cho permission của group mà có quyền sở hữu đối với file đó.
- 3 phần gạch `-` cuối cùng biểu thị cho permission của `other` tức các user còn lại đối với file đó.

> Ta có thể thêm quyền cho file bằng lệnh `chmod`. 

- Có hai cách thêm hoặc xóa quyền cho file đó là Numeric sử dụng số tương ứng với các quyền như:

| Number | Permission Type       | Symbol |
|--------|-----------------------|--------|
| 0      | No Permission         | —      |
| 1      | Execute               | –x     |
| 2      | Write                 | -w-    |
| 3      | Execute + Write       | -wx    |
| 4      | Read                  | r–     |
| 5      | Read + Execute        | r-x    |
| 6      | Read +Write           | rw-    |
| 7      | Read + Write +Execute | rwx    |

- Hoặc sử dụng `+` `-` `=` để set quyền cụ thể cho file.

- Sử dụng lệnh `su` để chuyển đổi giữa các user và `sudo` để sử dụng dưới quyền `root`.

1. On the deployable machine, who is the owner of "important"?: `user2`.
2. What would the command be to switch to the user "user2"?: `su user2`.
3. Output the contents of "important", what is the flag?: `THM{SU_USER2}`.

## Task 6: Common Directories

### /etc

- `etc` viết tắt của etcetera có ý nghĩa là vân vân. đường dẫn này chứa hầu hết các file cơ bản của hệ điều hành và những file cần thiết để hệ điều hành sử dụng.
- Trong đường dẫn này có những file nhạy cảm như `shadow password sudoers`.

### /var

- `var` viết tắt của variable data, là một trong những folder của `Linux`.
- Thư mục này lưu trữ dữ liệu thường xuyên được truy cập hoặc ghi bởi các dịch vụ hoặc ứng dụng đang chạy trên hệ thống.
- Ví dụ: các tệp nhật ký từ các dịch vụ và ứng dụng đang chạy được ghi ở đây.
- Một số file có trong nó như `log tmp backups opt`.

### /tmp

- `tmp` viết tắt của temporary, là một đường dẫn tạm thời mà trong nó lưu trữ những dữ liệu chỉ cần thiết sử dụng 1 đến 2 lần. Giống như bộ nhớ của máy tính, tất cả dữ liệu của thư mục này đều sẽ bị xóa đi khi máy tính khởi động lại.


