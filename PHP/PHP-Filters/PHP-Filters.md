# WRITE UP

**Challenge:** [PHP - Filters](https://www.root-me.org/en/Challenges/Web-Server/PHP-Filters)

Test payload trực tiếp đến /etc/passwd thì nhận được lỗi ràng buộc với /etc/passwd.

<img src="./media/image1.png" style="width:6.5in;height:1.93889in" alt="Graphical user interface, text, website Description automatically generated" />

Thật ra URL không filter keyword của mình nhưng mà không thể nào get nó theo cách này được. Chuyển qua dùng wrapper php với base64 để get source index.php:

<img src="./media/image2.png" style="width:6.5in;height:1.59444in" alt="Graphical user interface, text, application, website Description automatically generated" />

<img src="./media/image3.png" style="width:6.5in;height:2.47917in" alt="Graphical user interface, text, application Description automatically generated" />

Get source ch12.php:

<img src="./media/image4.png" style="width:6.5in;height:1.23958in" alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image5.png" style="width:6.5in;height:3.13889in" alt="Graphical user interface, text, application, email Description automatically generated" />

Vậy là website có config.php, get source config.php:

<img src="./media/image6.png" style="width:6.5in;height:1.5in" alt="Graphical user interface, text, application, website Description automatically generated" />

<img src="./media/image7.png" style="width:6.5in;height:2.02778in" alt="Graphical user interface, text, application, email Description automatically generated" />

-   Username: **admin**

-   Password: **DAPt9D2mky0APAF**

<img src="./media/image8.png" style="width:6.5in;height:2.19167in" alt="Graphical user interface, text, application, website Description automatically generated" />

<img src="./media/image9.png" style="width:6.5in;height:3.65625in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
