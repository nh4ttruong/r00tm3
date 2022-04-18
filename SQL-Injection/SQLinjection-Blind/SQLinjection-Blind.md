# WRITE UP

**Challenge: [SQL Injection - Blind](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-blind)**

Thử fuzz với payload **admin’-- -** ta đã access thành công qua Authentication v 0.02. Tuy vậy, website chẳng trả về cho thông tin password gì cả:

<img src="./media/image1.png" style="width:6.5in;height:2.46458in" alt="Graphical user interface, application Description automatically generated" />

Mở burpsuite và tìm kiếm thôi. Thử thay đổi payload bằng cách sử dụng union select thì phát hiện ra website đã filter các keyword chông SQL Injection với thông báo **“Injection detected”**:

<img src="./media/image2.png" style="width:6.5in;height:2.46667in" />

Với blind injection, ta thực hiện mò thử với các cấu trúc mà server database hay tạo, fuzz thôi:

<img src="./media/image3.png" style="width:6.5in;height:2.65694in" alt="Graphical user interface, text, website Description automatically generated" />

Với payload:

*username=admin%27+AND+(select+username+from+sqlite\_master)='admin'--+-&password=admin%27--+-*

Server trả về là TRUE fuzz tìm password bằng substr() thôi!

1.  **Tìm length(password):**

<img src="./media/image4.png" style="width:6.5in;height:3.17639in" alt="Graphical user interface, application Description automatically generated" />

-   Length(password) == 8

1.  **Tìm password:**

Payload để fuzz:

*username=admin%27+AND+substr((select+password+from+sqlite\_master),1,1)='a'--+-&password=admin%27--+-*

<img src="./media/image5.png" style="width:6.5in;height:4.19097in" alt="Table Description automatically generated with medium confidence" />

Sau một khoảng thời gian, ta đã ghép được password: **e2azO93i**

<img src="./media/image6.png" style="width:6.5in;height:3.90347in" alt="A picture containing text, screenshot, monitor, computer Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
