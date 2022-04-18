# WRITE UP

## Challenge: [Javascript - Obfuscation 3](https://www.root-me.org/en/Challenges/Web-Client/Javascript-Obfuscation-3)

Kiểm tra Sources website, ta thấy có file ch13.html:

<img src="./media/image1.png" style="width:6.5in;height:2.82083in" alt="Text Description automatically generated" />

Decode chuỗi ở biến pass, ta nhận được kết quả FAUX PASSWORD HAHA. Đọc lại code, ta thấy, ở dòng 21, script có sử dụng hàm dechiffre() để decode một đoạn chuỗi giá trị loại hex. Ta sử dụng công cụ ASCII Code để decrypt nó và được:

<img src="./media/image2.png" style="width:6.5in;height:2.70417in" alt="Graphical user interface, text Description automatically generated" />

Ta nhận được chuỗi “55,56,54,79,115,69,114,116,107,49,50”. Chuỗi này có format giống chuỗi ở biến pass, ta decode nó một lần nữa với công cụ ASCII Code và được:

<img src="./media/image3.png" style="width:6.5in;height:2.40139in" alt="Graphical user interface, application Description automatically generated" />

Từ đó, ta suy đoán được, password = ‘786OsErtk12’

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
