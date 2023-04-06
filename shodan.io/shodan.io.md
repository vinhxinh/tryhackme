# Shodan.io

----

## Task 1: Introduction

- Shodan là một công cụ tìm kiếm cho IoT
- Shodan scan toàn bộ Internet và lập chỉ mục đến từng địa chỉ IP

#### Autonomous System Numbers  (ASN)

- ASN (Autonomous System Number) là số thường được dùng trong các thủ tục định tuyến động trên mạng Internet. Được thể hiện là một số nguyên có giá trị từ 1 đến 65535 (đối với số hiệu mạng 2 byte) và từ 65536 đến 4294967295 (đối với số hiệu mạng 4 byte) và mỗi ASN thường được kết hợp với một AS duy nhất.
- Có hai loại số hiệu mạng là số hiệu mạng chung (public ASN) và số hiệu mạng riêng (private ASN).

#### Khi nào cần thiết lập ASN
- Khi một tổ chức muốn sử dụng giao thức định tuyến động BGP4, có kết nối đa hướng đến nhiều hơn một nhà cung cấp dịch vụ (multi – homed) và có chính sách định tuyến riêng (policy routing) thì người quản trị mạng cần phải yêu cầu các tổ chức có quyền quản lý cấp phát cho một số hiệu mạng. Số hiệu mạng này phải là duy nhất trên Internet, và tuân thủ theo các quy định cấp phát của IANA và các tổ chức quản lý khu vực.

#### Banner
- Các thiết bị chạy các dịch vụ và Shodan lưu trữ thông tin về chúng. Thông tin được lưu trữ trong một `banner`. Đó là phần cơ bản nhất của Shodan.

```
  {
		"data": "Moxa Nport Device",
		"Status": "Authentication disabled",
		"Name": "NP5232I_4728",
		"MAC": "00:90:e8:47:10:2d",
		"ip_str": "46.252.132.235",
		"port": 4800,
		"org": "Starhub Mobile",
		"location": {
				"country_code": "SG"
		}
  }
  
```

- Ta đang quan tâm đến đầu ra của một single port, mang thông tin của `IP` và các thông tin định danh.


## Task 2: Filter

- Những truy vấn được tìm kiếm nhiều nhất của `Shodan` có thể kể đến là _webcams_ và _MySQL_
- Shodan có rất nhiều `filters` mạnh mẽ để tìm kiếm. Một trong số đố là vuln filter, cái mà cho chúng ta có thể tìm ra những lỗ hổng từ `IP addresses` và khai thác nó.
> Note: Tuy nhiên nó chỉ dành cho học tập và công việc, tránh lạm dụng nó để làm điều xấu !!

#### API

- `API` có thể cho phép ta sử dụng chương trình để khai thác 1 list các `IP addresses`. Nếu ta ở trong một công ty, ta có thể viết những đoạn _scripts_ để kiểm tra xem địa chỉ IP đó có lỗ hổng nào có thể bị khai thác hay không

1. How do we find Eternal Blue exploits on Shodan?: `vuln:ms17-010`


## Task 3: Google & Filtering

- Filter with Google.

1. What is the top operating system for MYSQL servers in Google's ASN?: `5.6.40-84.0-log`
2. What is the 2nd most popular country for MYSQL servers in Google's ASN?: `Netherlands`	
3. Under Google's ASN, which is more popular for nginx, Hypertext Transfer Protocol or Hypertext Transfer Protocol with SSL?: `Hypertext Transfer Protocol`
4. Under Google's ASN, what is the most popular city?: `Mountain View`
5. Under Google's ASN in Los Angeles, what is the top operating system according to Shodan?: `PAN-OS`
6. Using the top Webcam search from the explore page, does Google's ASN have any webcams?: `Nay`



## Task 4: Shodan Monitor

1. What URL takes you to Shodan Monitor? https://monitor.shodan.io/dashboard

## Task 5: Shodan Dorking

- Shodan có một vài trang web cho phép ta tìm mọi thứ
  - `has_screenshot:true encrypted attention` sử dụng nhận dạng kí tự bằng thị giác và máy tính từ xa để tìm kiếm các máy tính bị ransomware.
  - `screenshot.label:ics`
  - `vuln:CVE-2014-0160` các thiết bị dễ bị tấn công bằng phương pháp này (allow for academic and business)

1. What dork lets us find PCs infected by Ransomware?: `has_screenshot:true encrypted attention`

## Task 6: Shodan Extension

- Shodan có cả extension [extension](https://chrome.google.com/webstore/detail/shodan/jjalcfnidlmpjhdfepjhjbhnhkbgleap)
- Khi cài đặt nó có thể cho ta biết `IP address` của website đang chạy, port nào đang mở, nơi nó được đặt và thông báo nếu có lỗi bảo mật.

## Task 7: Exploring the API & Conclusion


