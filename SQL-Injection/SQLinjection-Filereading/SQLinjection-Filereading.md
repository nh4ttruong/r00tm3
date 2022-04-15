# WRITE UP

**Challenge:** [SQL injection -- File reading](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-file-reading)

![Graphical user interface, text, application Description automatically generated](./media/image1.png){width="6.5in" height="2.1645833333333333in"}

Ở tab Members, ta tìm được thông tin cơ bản của admin. Từ đây, thử fuzz với URL bằng burpsuite để tìm kiếm điều khác biệt:

![Graphical user interface, text, application, email Description automatically generated](./media/image2.png){width="6.5in" height="3.1375in"}

Bắt đầu tìm kiếm số cột:

![Graphical user interface, text, application, email Description automatically generated](./media/image3.png){width="6.5in" height="2.173611111111111in"}

-   Có 4 cột

Sau một hồi fuzz, ta đã tìm được các bảng của dtb:

![Graphical user interface, text Description automatically generated](./media/image4.png){width="6.5in" height="2.8694444444444445in"}

*id=1+and+0=1+union+select+group_concat(table_name),1,1,1+from+information_schema.tables\--+-*

Ta thấy, có table 'member', tiến hành tìm column của nó. Tuy nhiên, dtb đã filter mất tiêu:

![Graphical user interface, text, email Description automatically generated](./media/image5.png){width="6.5in" height="2.8381944444444445in"}

Thử convert 'member' hex value: **0x6D656D626572**

![Graphical user interface, text, email Description automatically generated](./media/image6.png){width="6.5in" height="2.879166666666667in"}

-   member_id,member_login,member_password,member_email

Tìm password thôi. Tuy nhiên, đến lúc này database k constaint table_name nữa, ta có payload:

*id=1+and+0=1+union+select+member_login,member_password,1,1+from+member*

![Graphical user interface, text, application, email Description automatically generated](./media/image7.png){width="6.5in" height="2.7041666666666666in"}

Đến đây, ta nhận được một chuỗi base64 nhưng decode ra không phải password. Sau khi mò mẫm vô ích, nhìn lại tên bài là file reading, ta có thể đoán rằng, tất cả sẽ nằm trong source code tại index.php. Ta sẽ sử dụng sqlmap để tìm ra source web:

![A screenshot of a computer Description automatically generated](./media/image8.png){width="6.5in" height="2.4451388888888888in"}

![Text Description automatically generated](./media/image9.png){width="6.5in" height="2.363888888888889in"}

Source code cho ta thấy, password đã bị hash bằng **SHA1**, sau đó bị **stringxor** với base64 của chính nó.

![Text Description automatically generated](./media/image10.png){width="6.5in" height="3.327777777777778in"}

Giờ thì hiểu nó rồi, ta sử dụng python để stringxor ngược lại thành SHA1:

![A screenshot of a computer Description automatically generated with medium confidence](./media/image11.png){width="6.5in" height="3.3361111111111112in"}

-   SHA1 password: **77be4fc97f77f5f48308942bb6e32aacabed9cef**

![Graphical user interface, text, website Description automatically generated](./media/image12.png){width="6.146720253718285in" height="2.720055774278215in"}

-   Password: **superpassword**

![Graphical user interface, text, application Description automatically generated](./media/image13.png){width="6.5in" height="2.147222222222222in"}

![A screenshot of a computer Description automatically generated](./media/image14.png){width="5.80648075240595in" height="3.093687664041995in"}

**Flag:** superpassword
