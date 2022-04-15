# WRITE UP

**Challenge: [SQL Injection - Blind](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-blind)**

Thử fuzz với payload **admin'\-- -** ta đã access thành công qua Authentication v 0.02. Tuy vậy, website chẳng trả về cho thông tin password gì cả:

![Graphical user interface, application Description automatically generated](./media/image1.png){width="6.5in" height="2.464583333333333in"}

Mở burpsuite và tìm kiếm thôi. Thử thay đổi payload bằng cách sử dụng union select thì phát hiện ra website đã filter các keyword chông SQL Injection với thông báo **"Injection detected"**:

![](./media/image2.png){width="6.5in" height="2.466666666666667in"}

Với blind injection, ta thực hiện mò thử với các cấu trúc mà server database hay tạo, fuzz thôi:

![Graphical user interface, text, website Description automatically generated](./media/image3.png){width="6.5in" height="2.6569444444444446in"}

Với payload:

*username=admin%27+AND+(select+username+from+sqlite_master)=\'admin\'\--+-&password=admin%27\--+-*

Server trả về là TRUE fuzz tìm password bằng substr() thôi!

1.  **Tìm length(password):**

![Graphical user interface, application Description automatically generated](./media/image4.png){width="6.5in" height="3.176388888888889in"}

-   Length(password) == 8

2.  **Tìm password:**

Payload để fuzz:

*username=admin%27+AND+substr((select+password+from+sqlite_master),1,1)=\'a\'\--+-&password=admin%27\--+-*

![Table Description automatically generated with medium confidence](./media/image5.png){width="6.5in" height="4.190972222222222in"}

Sau một khoảng thời gian, ta đã ghép được password: **e2azO93i**

![A picture containing text, screenshot, monitor, computer Description automatically generated](./media/image6.png){width="6.5in" height="3.9034722222222222in"}

**Flag:** e2azO93i
