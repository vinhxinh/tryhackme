# OhSINT

--- 

# Task 1: OhSINT

> Nếu bạn đã nghe tên này rồi nhưng còn băn khoăn không biết nó nghĩa là gì, thì OSINT là viết tắt của từ open source intelligence, dùng để chỉ bất kỳ thông tin nào có thể được thu thập hợp pháp từ các nguồn công khai, miễn phí về một cá nhân hoặc tổ chức. Trên thực tế, điều đó có nghĩa là thông tin được tìm thấy trên internet, nhưng về mặt kỹ thuật, bất kỳ thông tin công khai nào đều thuộc OSINT cho dù đó là sách hoặc báo cáo, bài viết trên báo chí hay tuyên bố trong thông cáo báo chí.

![](https://github.com/vinhxinh/tryhackme/blob/main/Ohsint/WindowsXP.jpg?raw=true)

- Sau khi tải bức ảnh về và ấn vào ta sẽ có một cánh đồng rất xanh của WindowXP như trên. Không thể tìm được thêm thông tin gì. Ta có thể tìm thêm những thông tin của bức ảnh bằng cách xem metadata của nó.

![](https://github.com/vinhxinh/tryhackme/blob/main/Ohsint/pic1_task1.png?raw=true)

- Ta có thể thấy phần sở hữu bản quyền có tên của một người nào đó. Từ đó ta sẽ dùng google để tìm thông tin thêm: 

![](https://github.com/vinhxinh/tryhackme/blob/main/Ohsint/pic2_task1.png?raw=true)

- Có thể thấy ngay avatar người này sử dụng là con mèo. Vậy đáp án cho câu hỏi đầu tiên sẽ là `cat`.

1. What is this users avatar of?: `Cat`.


- Sau khi vào tìm hiểu thông tin README ở link github ta có thể thấy anh chàng này hiện đang sống ở London.

![](https://github.com/vinhxinh/tryhackme/blob/main/Ohsint/pic3_task1.png?raw=true)

2. What city is this person in?: `London`.

- Tìm trong link twitter của anh chàng này ta thấy có BSSID địa chỉ nhà của anh ta. Nên từ đó có thể tìm được WAP bằng cách dùng tool [wigle](https://wigle.net/).

![](https://github.com/vinhxinh/tryhackme/blob/main/Ohsint/pic4_task1.png?raw=true)

3. Whats the SSID of the WAP he connected to?: `UnileverWiFi`

- Trong README github ta còn có thể tìm thêm được thông tin về gmail của anh chàng này.

![](https://github.com/vinhxinh/tryhackme/blob/main/Ohsint/pic3_task1.png?raw=true)

4. What is his personal email address?: `OWoodflint@gmail.com`.
5. What site did you find his email address on?: `github`.

- Trong trang wordpress của anh này có nói đến việc anh ta đang ở New York và sẽ chụp những tấm ảnh ở đây và update lên wordpress nên mình đoán có thể anh này có kì nghỉ ở New York.

![](https://github.com/vinhxinh/tryhackme/blob/main/Ohsint/pic5_task1.png?raw=true)

6. Where has he gone on holiday?: `New York`.

- Câu cuối do không biết làm nên em đã xem solve trên mạng và biết sẽ tìm pasword được ẩn ở trong wordpress. Nó đã giấu password đi bằng cách thêm color `0xffffff` (màu trắng)  vào trong đoạn `<p>` chứa password.

![](https://github.com/vinhxinh/tryhackme/blob/main/Ohsint/pic6_task1.png?raw=true)

7. What is this persons password?: `pennYDr0pper.!`

