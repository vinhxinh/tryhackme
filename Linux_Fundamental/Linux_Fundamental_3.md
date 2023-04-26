# Linux  Fundamental 3

--- 

## Task 1: Introduction

## Task 2: Deploy Your Linux Machine

## Task 3: Terminal Text Editors

- Ở phần trước ta đã được thấy một số cách để lưu thông tin vào file bằng cách sử dụng `echo` và `>` hoặc>>` tuy nhiên đối với những file dài hoặc nhiều dòng ta khó có thể sử dụng cách này.
- `Linux` có một công cụ text editor sử dụng trực tiếp trên terminal đó là `nano`.
- Ta có thể thao tác với một file bằng cách `nano` + filename. Nếu file đó chưa được tạo nó sẽ tạo mới file đó.
- Mọi tính năng của `nano` đều phải sử dụng kết hợp với dấu "Ctrl".

- Ngoài ra ta còn có công cụ rất mạnh đó là `VIM`. Nó là một text editor nâng cao (Ta sẽ tìm hiểu sau).

1. Edit "task3" located in "tryhackme"'s home directory using Nano. What is the flag?: `THM{TEXT_EDITORS}`.

## Task 4: General/Useful Utilities

### Dowloading Files

- Khi mà bạn muốn Download một chương trình hoặc một đoạn scripts, hoặc 1 bức ảnh trên mạng. Ta có nhiều cách để thực hiện nó.
- Ta có thể sử dụng `wget` để tải file từ web thông qua `HTTPS`.

> `wget` https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt

### Transfer file from Your Host - SCP (SSH)

- `SCP` viết tắt của Secure Copy. Không giống như lệnh `cp` thông thường SCP sử dụng giao thức `SSH` protocol để truyền file giữa 2 thiết bị cung cấp tính bảo mật và mã hóa.
- `SCP` cho phép người dùng Copy file và Dicrectory từ máy tính hiện tại đến máy tính từ xa hoặc ngược lại.
- Tuy nhiên để sử dụng `SCP` ta cần biết một số thông tin sau:

| Variable                                             | Value         |
|------------------------------------------------------|---------------|
| IP address of the remote system                      | 192.168.1.30  |
| User on the remote system                            | ubuntu        |
| Name of the file on the remote system                | documents.txt |
| Name that we wish to store the file as on our system | notes.txt     |

Command sẽ có dạng như sau: 
> scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt

### Serving Files From Your Host - WEB (Cung cấp tệp từ máy chủ của bạn)

- Các máy Ubuntu được đóng gói sẵn với python3. Python cung cấp một mô-đun nhẹ và dễ sử dụng có tên là "HTTPServer" một cách hữu ích. Mô-đun này biến máy tính của bạn thành một máy chủ web nhanh chóng và dễ dàng mà bạn có thể sử dụng để phục vụ các tệp của riêng mình, sau đó chúng có thể được tải xuống bởi một máy tính khác bằng cách sử dụng các lệnh như `curl` và `wget`. 

- "HTTPServer" của Python3 sẽ phục vụ các tệp trong thư mục mà bạn chạy lệnh, nhưng điều này có thể được thay đổi bằng cách cung cấp các tùy chọn có thể tìm thấy trong các trang hướng dẫn. Đơn giản, tất cả những gì chúng ta cần làm là chạy `python3 -m  http.server` để khởi động mô-đun.

![]()

- Ta có thể sử dụng `wget` để tải xuống file bằng địa chỉ IP của máy tính và tên của file. Tuy nhiên với cách này bạn cần phải biết chính xác tên và đường dẫn chính xác của file để sử dụng. Thay vì điều đó ta có thể sử dụng [Updog](https://github.com/sc0tfree/updog) để thay thế những nhược điểm trên.

![]()

- Trong ví dụ trên ta có thể thấy được `wget` đã tải thành công một tệp file từ server về máy tính. Yêu cầu này được `SimpleHTTPServer` ghi lại.

![]()

1. Download the file http://10.10.144.234:8000/.flag.txt onto the TryHackMe AttackBox. What are the contents?: `THM{WGET_WEBSERVER}`.

## Task 5: Processes 101 (quy trình)

- Tất cả process đang chạy đều được quản lý bởi kernel. Và mỗi process đều có ID riêng của nó.

### Viewing Process

- Để xem danh sách các quy trình đang chạy của một user ta sử dụng `ps`.

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/ps1.png)

- Để xem danh sách các quy trình đang chạy của cả các người dùng khác ta sẽ truyền thêm vào `ps` tham số `aux`.

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/ps2.png)

- Thay vì chế độ xem 1 lần, `Linux` cung cấp cho bạn lệnh `top` để xem các process dưới dạng thời gian thực (tất cả quy trình đang chạy được làm mới 10s một lần)

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/top1.png)

### Managing Processes

- Bạn có thể gửi tín hiệu để chấm dứt process. 
- Có rất nhiều kiểu tín hiệu về độ "cleanly" đối với 1 process khi nó được xử lý bởi kernel.
- Để chấm dứt một process ta sử dụng `kill` + PID của nó. Ngoài ra còn một số tín hiệu chúng ta có thể gửi đến process để chấm dứt nó.
  - `SIGTERM`: kill process + cho nó thực hiện một vài tác vụ cleanup.
  - `SIGKILL`: kill process + không làm thêm gì sau đó.
  - `SIGSTOP`: Stop/Suspend process.

### How do Processes Start?

- Khi máy tính bắt đầu khởi động, `systemd` là một trong những process được khởi tạo đầu tiên. Bất kì những process được khởi động sau nó đều được coi như là process con của `systemd`. 

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/process1.png)

### Getting Processes/Services to Start on Boot

- `Systemctl` là một tiện ích dòng lệnh, có nhiệm vụ điều khiển hệ thống systemd và service manager. Systemd là một bộ công cụ để quản lý hệ thống Linux, nó được sử dụng để khởi động máy, quản lý dịch vụ, hệ thống file tự động, ghi sự kiện, thiết lập tên máy chủ và các tác vụ hệ thống khác. Systemd sử dụng các khái niệm unit, package, service, socket.
- Với `Systemctl` bạn có thể kiểm tra được trạng thái của các service, khởi động và tắt service, gỡ rối hệ thống khi xảy ra sự cố.
- Để sử dụng `systemctl`: 
> `systemctl` + [option] + [service]

Trong đó Option có 4 lựa chọn đó là: Start, Stop, Enable, Disable. Start và Stop dùng để khởi động hoặc ngừng tiến trình nào đó, còn Enable và Disable dùng để cho phép 1 tiến trình khởi động cùng với lúc máy tính bắt đầu khởi động hay không.

- Ví dụ để apache2 khởi động khi máy tính bắt đầu chạy: `systemctl start apache2`.

### An Introduction to Backgrounding and Foregrounding in Linux

- Một process có thể chạy ở 2 vị trí: `Background` và `Foreground`.
- Ví dụ như `echo` sẽ trả về kết quả ở Foreground nơi mà người dùng có thể theo dõi trực tiếp. Tuy nhiên khi ta sử dụng `echo "HI THM" &` thì nó sẽ được chạy ở Background và trả về cho ta 1 PID của tiến trình đang chạy.

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/bg1.png)

Nếu một script đang được loops hoặc thực hiện mà bạn muốn nó tiếp tục chạy ở trong background để nó không làm đầy Terminal của bạn. Bạn có thể sử dụng "**_Ctrl + z_**".

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/bg2.png)

Khi ta sử dụng `ps aux` ta thấy tiến trình ./background.sh vẫn đang được chạy ở background. Ta có thể cho nó tiếp tục chạy ở Foreground bằng cách sử dụng `fg` ở Terminal.

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/bg4.png)

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/bg5.png)

1. If we were to launch a process where the previous ID was "300", what would the ID of this new process be?: `301`.
2. If we wanted to cleanly kill a process, what signal would we send it?: `SIGTERM`.
3. Locate the process that is running on the deployed instance (10.10.239.175). What flag is given?: `THM{PROCESSES}`.
4. What command would we use to stop the service "myservice"?: `systemctl stop myservice`.
5. What command would we use to start the same service on the boot-up of the system?: `systemctl enable myservice`.
6. What command would we use to bring a previously backgrounded process back to the foreground?: `fg`.

## Task 6: Maintaining Your System: Automation

Người dùng có thể muốn lên lịch cho một hành động hoặc tác vụ nào đó diễn ra sau khi hệ thống đã khởi động. Lấy ví dụ: chạy các lệnh, sao lưu tệp hoặc khởi chạy các chương trình yêu thích của bạn, chẳng hạn như Spotify hoặc Google Chrome.
- `crontabs` là một trong những processes được bắt đầu chạy khi máy khởi động, nơi mà quản lý các `cron` jobs.

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/cron1.png)

- Một crontab chỉ là một file đặc biệt mà có định dạng giúp `cron` nhận dạng và thực thi từng dòng một. 
- `Crontabs` yêu cầu 6 giá trị cụ thể như bảng sau: 

| Value | Description                               |
|-------|-------------------------------------------|
| MIN   | What minute to execute at                 |
| HOUR  | What hour to execute at                   |
| DOM   | What day of the month to execute at       |
| MON   | What month of the year to execute at      |
| DOW   | What day of the week to execute at        |
| CMD   | The actual command that will be executed. |

- Ví dụ về việc backup file. Bạn cần backup file "Document" ở đường dẫn /home/cmnatic sang /var/backups/ ta sẽ làm như sau

> 0 *12 * * * cp -R /home/cmnatic/Documents /var/backups/

- Với những giá trị mà ta không quan tâm đến hoặc không có điều kiện ta có thể để dấu hoa thị "*" vào.

Một số tool giúp bạn viết cron jobs một cách dễ dàng
[Crontab Generator](https://crontab-generator.org/),
[Cron Guru](https://crontab.guru/).

- `Crontab` có thể được edit bằng lệnh `crontab -e` và có thể dùng `nano` text editor để edit.

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/cron2.png)

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/cron3.png)

![]()


1. When will the crontab on the deployed instance (10.10.208.44) run?: `@reboot`.

## Task 7: Maintaining Your System: Package Management

### Introducing Packages & Software Repos

Ubuntu là 1 hệ điều hành thuộc nhánh `Debian Linux`. Nó sử dụng các dpkg package để đóng gói các chương trình, ứng dụng, dành để cài đặt vào hệ thống.

- Lệnh `APT` (Advanced Package Tool) là một công cụ dòng lệnh (Command Line Tool) được sử dụng để quản lý các dpkg package (phần mềm / ứng dụng) trên hệ thống của Ubuntu.

- Khi các nhà phát triển muốn gửi phần mềm tới cộng đồng, họ sẽ gửi phần mềm đó tới kho lưu trữ `apt`. Nếu được chấp thuận, các chương trình và công cụ của họ sẽ được tung ra thị trường. Hai trong số các tính năng đáng giá nhất của Linux tỏa sáng ở đây: Khả năng truy cập của người dùng và giá trị của các công cụ nguồn mở.

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/apt1.png)

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/apt2.png)

- Trong khi các nhà cung cấp Hệ điều hành sẽ duy trì các kho lưu trữ của riêng họ, bạn cũng có thể thêm các kho lưu trữ cộng đồng vào danh sách của mình! Điều này cho phép bạn mở rộng khả năng của hệ điều hành . Các kho lưu trữ bổ sung có thể được thêm vào bằng cách sử dụng `add-apt-repository` lệnh hoặc bằng cách liệt kê một nhà cung cấp khác! Ví dụ: một số nhà cung cấp sẽ có kho lưu trữ gần vị trí địa lý của họ hơn.

### Managing Your Repositories (Adding and Removing)

- Lệnh `apt` là một phần của phần mềm quản lý gói cũng có tên là `apt`. `Apt` chứa toàn bộ bộ công cụ cho phép chúng tôi quản lý các gói và nguồn phần mềm của chúng tôi, đồng thời cài đặt hoặc gỡ bỏ phần mềm.

- Mặc dù bạn có thể cài đặt phần mềm thông qua việc sử dụng các trình cài đặt gói chẳng hạn như `dpkg`, nhưng lợi ích của apt có nghĩa là bất cứ khi nào chúng tôi cập nhật hệ thống của mình -- kho lưu trữ chứa các phần mềm mà chúng tôi thêm vào cũng được kiểm tra các bản cập nhật.

## Task 8:  Maintaining Your System: Logs

- File `log` được lưu trữ trong đường dẫn `/var/log`. Nó bao gồm những file và thư mục chứa thông tin truy cập vào phần mềm hoặc dịch vụ trên máy tính của bạn.

![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/log1.png)

- Riêng về web server thì thông tin lại theo từng request riêng lẻ. Điều này cho phép các nhà phát triển và quản trị viên chuẩn đoán về các vấn đề đang xảy ra hoặc điều tra về kẻ xâm nhập. Có 2 loại log đó là
  - Access log
  - Error log

  ![](https://assets.tryhackme.com/additional/linux-fundamentals/part3/log2.png)

  1. What is the IP address of the user who visited the site?: `10.9.232.111`.
  2. What file did they access?: `catsanddogs.jpg`.

  ## Task 9:  Conclusions & Summaries

  






