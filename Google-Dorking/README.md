# Google Dorking
*** 

## Task 1 

> **Ye Ol' Search Engine**

Google is arguably the most famous example of “Search Engines”, I mean who remembers Ask Jeeves? ~shudders~

Now it might be rather patronising explaining how these “Search Engines” work, but there’s a lot more going on behind the scenes then what we see. More importantly, we can leverage this to our advantage to find all sorts of things that a wordlist wouldn’t. Researching as a whole - especially in the context of Cybersecurity encapsulates almost everything you do as a pentester. [MuirlandOracle](https://tryhackme.com/p/MuirlandOracle) has created a [fantastic room](https://tryhackme.com/room/introtoresearch) on learning the attitudes towards how to research, and what information you can gain from it exactly.

"Search Engines" such as Google are huge indexers – specifically, indexers of content spread across the World Wide Web.

These essentials in surfing the internet use “Crawlers” or “Spiders” to search for this content across the World Wide Web, which I will discuss in the next task.

## Task 2

> **Let's Learn About Crawlers**

- **_Crawlers_** thu thập thông tin thông qua nhiều phương thức khác nhau. 
- Một cách tìm kiếm được sử dụng của **_Crawlers_** đó chính là nó sẽ tìm kiếm những thứ ta đã truyền vào từ ban đầu, nó có thể là `keyword` hoặc là `URLs`. Tất cả những thông tin liên quan đến việc tìm kiếm sẽ được nó lưu lại và tiếp tục đưa về thanh `SearchEngine` để tìm kiếm tiếp. Nó có thể được mô tả như việc virus phát tán mã độc mọi thứ mà nó đi qua. Ta có thể xem qua ảnh ví dụ bên dưới:
![](https://i.imgur.com/4nrDDa0.png)

- Nếu một đường dẫn `URL` có những `keyword` giống như tìm kiếm trước đó, nó sẽ cố gắng tiếp tục tìm kiếm và truy xuất những thứ đó trong `URL` mới đó. Một bức ảnh extended của việc tìm kiếm `Crawlers` hoạt động:
![](https://i.imgur.com/CIM2c6N.png)

- Tuy nhiên nếu người dùng search một keyword có nhiều hơn 1 `website` thỏa mãn vậy thứ tự các `website` sẽ được biểu thị mức độ như thế nào ?
1. Name the key term of what a "Crawler" is used to do: index
2. What is the name of the technique that "Search Engines" use to retrieve this information about websites?: crawling
3. What is an example of the type of contents that could be gathered from a website?: keywords

## Task 3

> **Enter: Search Engine Optimisation**

* Search Engine Optimisation hay SEO là chủ đề thực tế và được nhiều người tìm kiếm. Các công ty đều muốn tăng điểm SEO. Thanh công cụ tìm kiếm sẽ ưu tiên những domain dễ dàng tìm được index thỏa mãn. 
* Một vài tiêu chí để đánh giá điểm Optimisation:
  * Mức độ phản hồi của trang web đến với các loại thiết bị và trình duyệt khác nhau
  * Mức độ dễ dàng để `Crawling` trang web đó hoặc sự cho phép `Crawling` trên nó thông qua `Sitemap`
  * Từ khóa tìm kiếm của trang web đó có thông dụng hay không.
  
* Rất khó để đánh giá cách thức tính điểm để xếp hạng `domains` vì nó dựa vào thuật toán phức tạp và to lớn. Ta có thể sử dụng những công cụ đánh giá online như [link](https://pagespeed.web.dev/)

* Bên cạnh sự mong muốn tìm kiếm tất cả index có trong trong web nào đó, đôi khi trong một số trường hợp ta lại muốn ẩn đi như `login page` của Admin quản lý. Họ không muốn có thể tìm kiếm nó một cách dễ dàng bằng `Google search`


## Task 4

> **Beepboop - Robots.txt**

- File mà được chỉ mục đến đầu tiên của 1 website bởi `Crawlers` đó là file `robots.txt`.
- Tệp này được lưu trữ ở thư mục gốc do máy chủ web chỉ định. 
- `Robots.txt` có thể chỉ định những file và đường dẫn nào mà `Crawlers` có thể được chỉ mục và không muốn `Crawlers` được chỉ mục tới.
- Một dạng `robots.txt` cơ bản như sau:

  ![](https://i.imgur.com/wZ3lo4B.png)
 
| Keyword | Function |
|---|---|
| `User-agent` | Chỉ định thể loại của `Crawlers` có thể được dùng để chỉ mục đến trang (dấu hoa thị "*" asterisk biểu thị cho việc allow tất cả `User-agent`) |
| `Allow` | Chỉ định những đường dẫn và thư mục mà `Crawlers` có thể chỉ mục tới |
| `Disallow` | Chỉ định những đường dẫn và thư mục mà `Crawlers` không thể chỉ mục tới |
| `Sitemap` | Cung cấp danh sách các trang trong một trang website |

- Một vài ví dụ

	![](https://i.imgur.com/audlFn8.png)
	
	1. Any "Crawler" can index the site
	2. The "Crawler" can index every other content that isn't contained within "/super-secret-directory/". Crawlers also know the differences between sub-directories, directories and files. Such as in the case of the second "Disallow:" ("/not-a-secret/but-this-is/"). The "Crawler" will index all the contents within "**/not-a-secret/**", but will not index anything contained within the sub-directory "**/but-this-is/**".
	3. The "Sitemap" is located at http://mywebsite.com/sitemap.xml

	![](https://i.imgur.com/LxitBJs.png)
	
	1. The "Crawler" "Googlebot" is allowed to index the entire site ("Allow: /")
	2. The "Crawler" "msnbot" is not allowed to index the site (Disallow: /")
	
	![](https://i.imgur.com/mzDqFVY.png)
	
	1. Any "Crawler" can index the site
	2. However, the "Crawler" cannot index any file that has the extension of .ini within any directory/sub-directory using ("$") of the site.
	3. The "Sitemap" is located at http://mywebsite.com/sitemap.xml

> Note: Bạn có thể nhập thủ công cho mọi loại file (.txt,.ini) mà bạn không muốn bị chỉ mục, bạn sẽ phải cung cấp đầy đủ filename cùng với đường dẫn của nó. Tưởng tượng bạn có một file lớn, điều đó là rất khó. Vì vậy bạn có thể sử dụng [regexing](http://www.rexegg.com/regex-quickstart.html#ref)

1. Where would "robots.txt" be located on the domain "**ablog.com**": ablog.com/robots.txt
2. If a website was to have a sitemap, where would that be located?: /sitemap.xml
3. How would we only allow "Bingbot" to index the website?: user-agent: Bingbot
4. How would we prevent a "Crawler" from indexing the directory "/dont-index-me/"?: disallow: /dont-index-me/
5. What is the extension of a Unix/Linux system configuration file that we might want to hide from "**Crawlers**"?: .conf


## Task 5

> Sitemaps

* Giống như bản đồ ngoài đời thực, `Sitemaps` cũng là một dạng bản đồ dành riêng cho `websites`
* `Sitemaps` là một tài nguyên hữu ích giúp ta có thể chỉ mục thông tin một cách nhanh chóng nhờ các đường dẫn đã được chỉ định các tuyến đường `route` dẫn đến nội dung trên `domain`. Đây là cấu trúc của một `Sitemap`:
![](https://i.imgur.com/L5WqJU4.png) 

* Màu xanh dương biểu thị cho các đường dẫn `route` (similar to directory) còn màu xanh lá biểu thị cho các trang trên thực tế. File `Sitemap.xml` có dạng:

  ![](https://i.imgur.com/12Yxcn5.png)
  
* `Sitemaps` có ảnh hưởng lớn tới SEO vì nó giúp tìm kiếm thông tin một cách dễ dàng hơn rất nhiều.
* `Search Engine` có rất nhiều dữ liệu phải xử lý vậy nên `Sitemap` giúp `Crawlers` có được thông tin đường dẫn cần thiết để truy vấn đến dữ liệu cần tìm. `Crawlers` sẽ sử dụng `Sitemap` để tìm tệp thay vì đoán tên của nó.

1. What is the typical file structure of a "Sitemap"?: xml
2. What real life example can "Sitemaps" be compared to?: map
3. Name the keyword for the path taken for content on a website: route


## Task 6

> What is Google Dorking?

* Bởi vì Google có rất nhiều chỉ mục được `Crawlers`. Vậy nên ta cần thu hẹp phạm vi tìm kiếm và cụ thể nó.
* Một vài thuật ngữ cơ bản để tìm kiếm kết hợp bao gồm: 

| Term | Action |
|---|---|
| `site:` | chỉ định rõ site cần tìm kiếm trong đó |
| `filetype:` | Loại file cần tìm kiếm |
| `cache` | Xem phiên bản được lưu trong bộ nhớ cache của Google của một URL được chỉ định |
| `intitle` | Nội dung bắt buộc phải xuất hiện ở tiêu đề của trang |

- Ví dụ để tìm kiếm `PDF` trên site `bbc.co.uk`: 
  > site:bbc.co.uk filetype:pdf
 
	![](https://i.imgur.com/xoDtXnA.png)
	
* Ta cũng có thể sử dụng bất kì một dạng `file format` nào để truy cập những thông tin nhạy cảm. Vì vậy `Google Dorking` thật sự nguy hiểm.
  * Ta có thể sử dụng `intitle` để tìm kiếm như sau:
    > intitle: index of
    
	![](https://i.imgur.com/24OH1Kk.png)
	![](https://i.imgur.com/o0Cnm1P.png)

1. What would be the format used to query the site bbc.co.uk about flood defences: site: bc.co.uk flood defences
2. What term would you use to search by file type?: filetype:
3. What term can we use to look for login pages?: intitle: login

