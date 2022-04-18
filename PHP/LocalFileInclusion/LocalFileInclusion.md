# WRITE UP

**Challenge:** [Local File Inclusion](https://www.root-me.org/en/Challenges/Web-Server/Local-File-Inclusion)

Website có rất nhiều tab và gây confuse khi làm:

<img src="./media/image1.png" style="width:6.5in;height:1.82222in" alt="Graphical user interface, text Description automatically generated" />

Câu query URL có dạng [challenge01.root-me.org/web-serveur/ch16/?files=sysadm&f=index.html](http://challenge01.root-me.org/web-serveur/ch16/?files=crypto&f=index.html) với files sẽ chỉ định folder và f sẽ chỉ định tệp hoặc folder con mà ta chọn:

<img src="./media/image2.png" style="width:6.5in;height:1.81875in" alt="Shape Description automatically generated with low confidence" />

<img src="./media/image3.png" style="width:6.5in;height:1.71806in" alt="Graphical user interface, text, application Description automatically generated" />

Chuyển qua mò tab Admin thì website bắt login. Biết gì đâu mà login :v. Tắt promt login thì ta nhận được dòng text:

<img src="./media/image4.png" style="width:6.5in;height:0.69444in" alt="Graphical user interface, text, application, website Description automatically generated" />

Như vậy, website sử dụng backend là PHP. Thử mò file source code của nó dựa theo query ở trên:

<img src="./media/image5.png" style="width:6.5in;height:1.60417in" alt="Graphical user interface, text, application Description automatically generated" />

Lỗi trả về là **file\_get\_contents()** không tìm được filename. Sau khi thử fuzz một lúc thì phát hiện ra website không block **‘../’.** Đã đến lúc ta dùng Path Traversal.

Thử với **files=../**:

<img src="./media/image6.png" style="width:6.5in;height:1.85417in" alt="Graphical user interface, text, application, email Description automatically generated" />

Lúc này, ta thấy được các thư mục cha chứa thư mục files, trong đó, có folder admin. Đặc biệt, website có một file là index.php giống như ở homepage của website. Vậy hướng của ta là xem được các file có trong folder admin (như index.php). Thử trỏ **files=../admin** và **&f=index.php** thì ta đã truy cập thành công index.php:

<img src="./media/image7.png" style="width:6.5in;height:1.99306in" alt="Graphical user interface, text, application Description automatically generated" />

Dò source code ta thấy được 2 dòng code rất giá trị:

<img src="./media/image8.png" style="width:6.5in;height:2.48889in" alt="Graphical user interface, text, application, email Description automatically generated" />

Vậy là đã tìm được account của admin:

-   Username: admin

-   Password: OpbNJ60xYpvAQU8

<img src="./media/image9.png" style="width:6.5in;height:1.24653in" alt="Graphical user interface, text, application Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
