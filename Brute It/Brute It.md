# Brute It

---

## Task 1: About this box

## Task 2: Reconnaissance

Sau khi deploy machine từ Tryhackme, mình có được một địa chỉ IP. `$ip`.

Đầu tiên chúng ta sẽ sử dụng `nmap` để kiểm tra tất cả các cổng mở của địa chỉ IP trên. Mình sẽ sử dụng sript như sau: `sudo nmap -sV $ip`.

Giải thích thêm về đoạn script trên: `sudo nmap -sV $ip`.
- Đầu tiên mình sử dụng thêm quyền của user `root` với mục đích như sau:

![](pic1)

- Tiếp theo sử dụng scan option `-sV` để có thêm thông tin về cổng được mở, dịch vụ và phiên bản được sử dụng của nó.

![](pic2)

1. How many ports are open?: `2`.
2. What version of SSH is running?: `OpenSSH 7.6p1`.
3. What version of Apache is running?: `2.4.29`.
4. Which Linux distribution is running?: `Ubuntu`.

Để tìm được file ẩn trong bài tập này mình sẽ sử dụng `gobuster` để brute force tất cả đường dẫn cơ bản của một trang web. Scripts có dạng `gobuster -w $dir_to_wordlist dir -u http://$ip/`.

Trong đó 2 tham số truyền vào sẽ là `-w` tương ứng với wordlist để brute và `dir -u` tương ứng với đường dẫn trang web.

![](pic3)

5. What is the hidden directory?: `/admin`.

## Task 3: Getting a shell

![](pic4)

Sau khi mình truy cập vào đường dẫn ẩn `/admin` thì sẽ có một trang web đăng nhập hiện ra. Chưa có thông tin gì về thông tin đăng nhập nên mình thử `Inspect` để tìm một vài thông tin. Dev đã để quên credential trên chính code HTML của mình nên mình có thể biết tài khoản đăng nhập là `admin` còn mật khẩu là gì thì mình chưa rõ. 

![](pic5)

Ở đây mình có thể sử dụng `Burp Suite` hoặc `Hydra` tuy nhiên mình sẽ sử dụng `Hydra` vì đang có sẵn máy ảo. Script mình dùng là: `hydra -l admin -P $dir_to_wordlist $ip http-form-post "/admin/:user=^USER^&pass=^PASS^:Username or password invalid"`.

Giải thích rõ về đoạn script trên:
- Đối với việc đã biết username là `admin` mình sẽ truyền vào tham số `-l admin` để thông báo.
- Tiếp theo vì mật khẩu chưa biết cần phải brute nên mình sẽ truyền vào tham số `-P $dir_to_wordlist`.
- Tiếp theo sẽ là địa chỉ IP của trang web đăng nhập `$ip`.
- `http-form-post` thể hiện phương thức `POST` sẽ được sử dụng để gửi request đến server.
- Trong ngoặc "" mình sẽ phải truyền vào 3 tham số đó là `/admin/` cho biết đến đường dẫn ẩn của trang web. Phân cách bởi dấu `:`. Tiếp theo là `user=^USER^&pass=^PASS^` để chương trình hiểu nó sẽ sử dụng user là admin của biến trước đó và pass là phần dẫn đến file brute force. Cuối cùng là `Username or password invalid` thể hiện thông báo của web khi chưa đăng nhập thành công để chương trình tự hiểu chuyển sang trường hợp khác.

![](pic6)

Ta đã tìm được mật khẩu là `xavier`.

Tiếp theo ta sẽ cần xử lý file RSA key được cho từ trang web. Nó được thông báo rằng đây là key để ssh đến máy tính của john.

Vì nó được mã hóa dưới dạng `SHA256` nên mình sẽ sử dụng `john the ripper` để crack mật khẩu. Nhưng đầu tiên để sử dụng được `john` mình cần chuyển tất cả key RSA ban đầu từ server sang thứ mà john có thể hiểu được. Ở trong thư viện `john` đã có những đoạn code python giúp chuyển. Mình sẽ sử dụng `ssh2john.py` để làm điều đó.

Mình sẽ sử dụng script `python3 $dir_to_ssh2john.py id_rsa > sshhash`.
Giải thích cho đoạn command trên: 
- Mình sẽ lưu file key RSA ban đầu và file text có tên là id_rsa. Tiếp theo mình sẽ chạy chương trình `ssh2john` để chuyển nội dung file id_rsa đến file sshhash được tạo mới.

Tiếp theo mình sẽ sử dụng `john` với đoạn script như sau: `sudo john --wordlist=$dir_to_wordlist --format=ssh sshhash` trong đó `--format` để xác định loại key ban đầu.

![](pic7)

Sau khi đã tìm ra passphares của `id_rsa` là `rockinroll` mình tiến hành ssh lên server của John bằng chính file identify là file `id_rsa` ban đầu. Command mình dùng là: `ssh -i id_rsa john@$ip`. Trong đó -i chính là option truyền vào file identify để ssh lên server.

![](pic8)

Sau khi đã vào được server mình dễ dàng cat file `user.txt` để lấy được flag cần tìm.

1. What is the user:password of the admin panel?: `admin:xavier`.
2. What is John's RSA Private Key passphrase?: `rockinroll`.
3. user.txt: `THM{a_password_is_not_a_barrier}`.
4. Web flag: `THM{brut3_f0rce_is_e4sy}`.

## Task 4: Privilege Escalation

Đến bước leo thang đặc quyền việc đầu tiên mình nghĩ đến là kiểm tra các linux command nào được chạy dưới quyền root mà không cần password. Mình sẽ sử dụng lệnh: `sudo -l`. Kiểm tra mình thấy có sử dụng được lệnh `cat`. Mình sẽ sử dụng `cat` để đọc nội dung của file `passwd` hoặc `shadow`.

![](pic9)

Sau khi cat được file `shadow` mình có password đã được mã hóa của `root`. Làm như phần giải mã id_rsa bằng `john` mình thu được kết quả mật khẩu `root` là: `football`. Mình sẽ truy cập vào tài khoản root và làm nốt mấy task còn lại.

![](pic10)

1. What is the root's password?: `football`.
2. root.txt: `THM{pr1v1l3g3_3sc4l4t10n}`.












