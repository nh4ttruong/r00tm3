# WRITE UP

**Challenge:** [File upload - MIME type](https://www.root-me.org/en/Challenges/Web-Server/File-upload-MIME-type)

Đề yêu cầu ta tìm .passwd. Thử check với .passwd tại **/ch21/.passwd** thì nhận được 404 Forbidden:

<img src="./media/image1.png" style="width:6.5in;height:1.04792in" alt="Graphical user interface, text, application Description automatically generated" />

Website có cung cấp một cổng upload và challenge có đề cập đến MIME type. ổng này sau khi nhận file của ta thì lưu trữ tại ./\[name\]. Bây giờ ta cần chèn payload vào để push lên server:

<img src="./media/image2.png" style="width:6.5in;height:1.95833in" alt="Graphical user interface, text Description automatically generated" />

<img src="./media/image3.png" style="width:6.5in;height:2.41667in" alt="Graphical user interface, text, application Description automatically generated" />

URL sau khi upload: <http://challenge01.root-me.org/web-serveur/ch21/galerie/upload/40ce7d3f3fe27d0d9c1970598b6d09a8//nh4ttruong.jpg>

Lúc đầu, ta đã biết .passwd nằm tại …/ch21/.passwd. Do đó, ta cần đi ngược folder 3 lần để đọc được.

Gắn [shell\_exec()](https://www.php.net/manual/en/function.mime-content-type.php) vào file nh4ttruong123.php.jpg:

&lt;?php  
$output = shell\_exec('cat ../../../.passwd');  
echo "&lt;pre&gt;$output&lt;/pre&gt;";  
?&gt;

Bởi vì server chỉ cho ta upload các file image (jpeg/png/gif), do đó, ta cần sử dụng BurpSuite để modify request convert .jpg sang .php:

<img src="./media/image4.png" style="width:6.5in;height:2.6625in" alt="Graphical user interface, text, application, email Description automatically generated" />

Mod thành công:

<img src="./media/image5.png" style="width:6.5in;height:1.75833in" alt="Graphical user interface, text, application Description automatically generated" />

Code đã chạy, ta get được password:

<img src="./media/image6.png" style="width:6.5in;height:0.96389in" alt="Graphical user interface, application Description automatically generated" />

<img src="./media/image7.png" style="width:6.5in;height:3.89792in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
