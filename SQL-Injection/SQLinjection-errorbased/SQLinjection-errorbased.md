# WRITE UP

**Challenge:** [SQL injection - Error](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-Error)

<img src="./media/image1.png" style="width:6.5in;height:2.97917in" alt="A screenshot of a computer Description automatically generated" />

Website cung cấp cho ta 2 tab (Authentication và Contents), tuy vậy, khi fuzz SQLi vào Authentication thì không có kết quả khả thi. Chuyển qua tab Contents, ta phát hiện ra website sẽ res về lỗi cho ta:

<img src="./media/image2.png" style="width:6.5in;height:2.53125in" alt="Graphical user interface, text, application Description automatically generated" />

Thử fuzz các payload dựa vào “ORDER BY”:

<img src="./media/image3.png" style="width:6.5in;height:1.67014in" alt="Graphical user interface, text, application, website Description automatically generated" />

<img src="./media/image4.png" style="width:6.5in;height:1.86042in" alt="Graphical user interface, text, application Description automatically generated" />

<img src="./media/image5.png" style="width:6.32555in;height:2.41688in" alt="Graphical user interface, text, application Description automatically generated" />

Có thể thấy, với position==3 hoặc VARCHAR/CHAR type thì database res về lỗi. Như vậy, ta cần phải hiết 3 position của database này cũng như dựa vào type varibles để attack. Dựa vào cheatsheet của MySQL, ta có thể sử dụng ***CAST … AS \[type\]*** để khiến database res về error khi <u>postion không thể là VARCHAR/CHAR</u>. Mở burpsuite và thử payload:

<img src="./media/image6.png" style="width:6.5in;height:3.34583in" alt="Graphical user interface, text, application, email Description automatically generated" />

Lỗi res về cho ta biết, website sẽ chỉ hiển thị 1 row. Đến đây, ta có thể sử dụng LIMIT để filter res về 1 row:

<img src="./media/image7.png" style="width:6.5in;height:3.15972in" alt="Graphical user interface, text, application, email Description automatically generated" />

-   Table name: **m3mbr35t4bl3**

<img src="./media/image8.png" style="width:6.5in;height:3.31736in" alt="Graphical user interface, text, application, email Description automatically generated" />

-   Column name (first column): **id**

Đến đây, ta cần sử dụng OFFSET để có thể filter vào đúng postion ta cần LIMIT để hiển thị các column còn lại:

<img src="./media/image9.png" style="width:6.5in;height:3.27014in" alt="Graphical user interface, text, application, email Description automatically generated" />

<img src="./media/image10.png" style="width:6.5in;height:3.32014in" alt="Graphical user interface, text, email Description automatically generated" />

-   Username column: us3rn4m3\_c0l

-   Password column: p455w0rd\_c0l

<img src="./media/image11.png" style="width:6.5in;height:3.24375in" alt="Graphical user interface, text, application, email Description automatically generated" />

<img src="./media/image12.png" style="width:6.5in;height:3.27292in" alt="Graphical user interface, text, email Description automatically generated" />

-   Username của admin: **admin**

-   Password của admin: **1a2BdKT5DIx3qxQN3UaC**

<img src="./media/image13.png" style="width:6.5in;height:3.82083in" alt="A screenshot of a computer Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
