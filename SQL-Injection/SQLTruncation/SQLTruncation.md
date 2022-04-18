# WRITE UP

**Challenge: [SQL Truncation](https://www.root-me.org/en/Challenges/Web-Server/SQL-Truncation)**

<img src="./media/image1.png" style="width:6.5in;height:1.93403in" alt="Graphical user interface, application Description automatically generated" />

**SQL Truncation** là lỗ hổng xảy ra khi user input vượt qua các điều kiện của database khiến database xung đột và gây ra hiện tượng thiếu xác thực.

Ở challenge này, ta phải mạo danh admin và login vào tab của admin. Đầu tiên, ta kiếm tra sources code và thấy được comment về các query khi register:

<img src="./media/image2.png" style="width:6.5in;height:3.08403in" alt="Graphical user interface, text, application Description automatically generated" />

Ở username và password, ta có thể thấy, database giới hạng length = 12 (login) và length = 32 (password). Như vậy, ta thử attack vào username với payload:

-   **Username:** admin hehehehe (7 whitespace)

-   **Password:** somethinghere

<img src="./media/image3.png" style="width:4.44205in;height:1.73348in" alt="Graphical user interface, text, application, email Description automatically generated" />

Khi này, ta nhận được thông báo “User saved”. Theo SQL Truncations, lúc này, thông tin login của ta sẽ bị truncate thành:

-   **Username**: admin

-   **Password (new)**: somethinghere

Ta chuyển qua tab Administrator, login vào bằng password vừa tạo:

<img src="./media/image4.png" style="width:6.08386in;height:2.44188in" alt="Graphical user interface, text, application, website Description automatically generated" />

Ta nhận được flag sau khi login!

**Flag:** J41m3Qu4nD54Tr0nc

\- Flag:
