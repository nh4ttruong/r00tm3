# WRITE UP

**Challenge:** [SQL injection – File reading](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-file-reading)

<img src="./media/image1.png" style="width:6.5in;height:2.16458in" alt="Graphical user interface, text, application Description automatically generated" />

Ở tab Members, ta tìm được thông tin cơ bản của admin. Từ đây, thử fuzz với URL bằng burpsuite để tìm kiếm điều khác biệt:

<img src="./media/image2.png" style="width:6.5in;height:3.1375in" alt="Graphical user interface, text, application, email Description automatically generated" />

Bắt đầu tìm kiếm số cột:

<img src="./media/image3.png" style="width:6.5in;height:2.17361in" alt="Graphical user interface, text, application, email Description automatically generated" />

-   Có 4 cột

Sau một hồi fuzz, ta đã tìm được các bảng của dtb:

<img src="./media/image4.png" style="width:6.5in;height:2.86944in" alt="Graphical user interface, text Description automatically generated" />

*id=1+and+0=1+union+select+group\_concat(table\_name),1,1,1+from+information\_schema.tables--+-*

Ta thấy, có table ‘member’, tiến hành tìm column của nó. Tuy nhiên, dtb đã filter mất tiêu:

<img src="./media/image5.png" style="width:6.5in;height:2.83819in" alt="Graphical user interface, text, email Description automatically generated" />

Thử convert ‘member’ hex value: **0x6D656D626572**

<img src="./media/image6.png" style="width:6.5in;height:2.87917in" alt="Graphical user interface, text, email Description automatically generated" />

-   member\_id,member\_login,member\_password,member\_email

Tìm password thôi. Tuy nhiên, đến lúc này database k constaint table\_name nữa, ta có payload:

*id=1+and+0=1+union+select+member\_login,member\_password,1,1+from+member*

<img src="./media/image7.png" style="width:6.5in;height:2.70417in" alt="Graphical user interface, text, application, email Description automatically generated" />

Đến đây, ta nhận được một chuỗi base64 nhưng decode ra không phải password. Sau khi mò mẫm vô ích, nhìn lại tên bài là file reading, ta có thể đoán rằng, tất cả sẽ nằm trong source code tại index.php. Ta sẽ sử dụng sqlmap để tìm ra source web:

<img src="./media/image8.png" style="width:6.5in;height:2.44514in" alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image9.png" style="width:6.5in;height:2.36389in" alt="Text Description automatically generated" />

Source code cho ta thấy, password đã bị hash bằng **SHA1**, sau đó bị **stringxor** với base64 của chính nó.

<img src="./media/image10.png" style="width:6.5in;height:3.32778in" alt="Text Description automatically generated" />

Giờ thì hiểu nó rồi, ta sử dụng python để stringxor ngược lại thành SHA1:

<img src="./media/image11.png" style="width:6.5in;height:3.33611in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

-   SHA1 password: **77be4fc97f77f5f48308942bb6e32aacabed9cef**

<img src="./media/image12.png" style="width:6.14672in;height:2.72006in" alt="Graphical user interface, text, website Description automatically generated" />

-   Password: **superpassword**

<img src="./media/image13.png" style="width:6.5in;height:2.14722in" alt="Graphical user interface, text, application Description automatically generated" />

<img src="./media/image14.png" style="width:5.80648in;height:3.09369in" alt="A screenshot of a computer Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
