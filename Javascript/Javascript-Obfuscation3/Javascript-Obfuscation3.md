# WRITE UP

## Challenge: [Javascript - Obfuscation 3](https://www.root-me.org/en/Challenges/Web-Client/Javascript-Obfuscation-3)

Kiểm tra Sources website, ta thấy có file ch13.html:

![Text Description automatically generated](./media/image1.png){width="6.5in" height="2.8208333333333333in"}

Decode chuỗi ở biến pass, ta nhận được kết quả FAUX PASSWORD HAHA. Đọc lại code, ta thấy, ở dòng 21, script có sử dụng hàm dechiffre() để decode một đoạn chuỗi giá trị loại hex. Ta sử dụng công cụ ASCII Code để decrypt nó và được:

![Graphical user interface, text Description automatically generated](./media/image2.png){width="6.5in" height="2.7041666666666666in"}

Ta nhận được chuỗi "55,56,54,79,115,69,114,116,107,49,50". Chuỗi này có format giống chuỗi ở biến pass, ta decode nó một lần nữa với công cụ ASCII Code và được:

![Graphical user interface, application Description automatically generated](./media/image3.png){width="6.5in" height="2.401388888888889in"}

Từ đó, ta suy đoán được, password = '786OsErtk12'

**Password:** **786OsErtk12**
