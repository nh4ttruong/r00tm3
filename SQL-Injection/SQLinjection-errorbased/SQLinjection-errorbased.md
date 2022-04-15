# WRITE UP

**Challenge:** [SQL injection - Error](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-Error)

![A screenshot of a computer Description automatically generated](./media/image1.png){width="6.5in" height="2.9791666666666665in"}

Website cung cấp cho ta 2 tab (Authentication và Contents), tuy vậy, khi fuzz SQLi vào Authentication thì không có kết quả khả thi. Chuyển qua tab Contents, ta phát hiện ra website sẽ res về lỗi cho ta:

![Graphical user interface, text, application Description automatically generated](./media/image2.png){width="6.5in" height="2.53125in"}

Thử fuzz các payload dựa vào "ORDER BY":

![Graphical user interface, text, application, website Description automatically generated](./media/image3.png){width="6.5in" height="1.6701388888888888in"}

![Graphical user interface, text, application Description automatically generated](./media/image4.png){width="6.5in" height="1.8604166666666666in"}

![Graphical user interface, text, application Description automatically generated](./media/image5.png){width="6.3255479002624675in" height="2.4168766404199475in"}

Có thể thấy, với position==3 hoặc VARCHAR/CHAR type thì database res về lỗi. Như vậy, ta cần phải hiết 3 position của database này cũng như dựa vào type varibles để attack. Dựa vào cheatsheet của MySQL, ta có thể sử dụng ***CAST ... AS \[type\]*** để khiến database res về error khi [postion không thể là VARCHAR/CHAR]{.underline}. Mở burpsuite và thử payload:

![Graphical user interface, text, application, email Description automatically generated](./media/image6.png){width="6.5in" height="3.345833333333333in"}

Lỗi res về cho ta biết, website sẽ chỉ hiển thị 1 row. Đến đây, ta có thể sử dụng LIMIT để filter res về 1 row:

![Graphical user interface, text, application, email Description automatically generated](./media/image7.png){width="6.5in" height="3.1597222222222223in"}

-   Table name: **m3mbr35t4bl3**

![Graphical user interface, text, application, email Description automatically generated](./media/image8.png){width="6.5in" height="3.317361111111111in"}

-   Column name (first column): **id**

Đến đây, ta cần sử dụng OFFSET để có thể filter vào đúng postion ta cần LIMIT để hiển thị các column còn lại:

![Graphical user interface, text, application, email Description automatically generated](./media/image9.png){width="6.5in" height="3.270138888888889in"}

![Graphical user interface, text, email Description automatically generated](./media/image10.png){width="6.5in" height="3.3201388888888888in"}

-   Username column: us3rn4m3_c0l

-   Password column: p455w0rd_c0l

![Graphical user interface, text, application, email Description automatically generated](./media/image11.png){width="6.5in" height="3.24375in"}

![Graphical user interface, text, email Description automatically generated](./media/image12.png){width="6.5in" height="3.2729166666666667in"}

-   Username của admin: **admin**

-   Password của admin: **1a2BdKT5DIx3qxQN3UaC**

![A screenshot of a computer Description automatically generated](./media/image13.png){width="6.5in" height="3.8208333333333333in"}

**Flag:** 1a2BdKT5DIx3qxQN3UaC
