# WRITE UP

**Challenge: [SQL Truncation](https://www.root-me.org/en/Challenges/Web-Server/SQL-Truncation)**

![Graphical user interface, application Description automatically generated](./media/image1.png){width="6.5in" height="1.9340277777777777in"}

**SQL Truncation** là lỗ hổng xảy ra khi user input vượt qua các điều kiện của database khiến database xung đột và gây ra hiện tượng thiếu xác thực.

Ở challenge này, ta phải mạo danh admin và login vào tab của admin. Đầu tiên, ta kiếm tra sources code và thấy được comment về các query khi register:

![Graphical user interface, text, application Description automatically generated](./media/image2.png){width="6.5in" height="3.0840277777777776in"}

Ở username và password, ta có thể thấy, database giới hạng length = 12 (login) và length = 32 (password). Như vậy, ta thử attack vào username với payload:

-   **Username:** admin+++++++hehehehe

-   **Password:** somethinghere

![Graphical user interface, text, application, email Description automatically generated](./media/image3.png){width="4.442051618547682in" height="1.7334831583552055in"}

Khi này, ta nhận được thông báo "User saved". Theo SQL Truncations, lúc này, thông tin login của ta sẽ bị truncate thành:

-   **Username**: admin

-   **Password (new)**: somethinghere

Ta chuyển qua tab Administrator, login vào bằng password vừa tạo:

![Graphical user interface, text, application, website Description automatically generated](./media/image4.png){width="6.0838604549431325in" height="2.441877734033246in"}

Ta nhận được flag sau khi login!

**Flag:** J41m3Qu4nD54Tr0nc
