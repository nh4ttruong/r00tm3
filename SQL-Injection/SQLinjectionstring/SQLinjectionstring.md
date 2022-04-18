# WRITE UP

**Challenge:** [SQL injection - String](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-String)

<img src="./media/image1.png" style="width:6.5in;height:1.10208in" alt="Graphical user interface Description automatically generated with low confidence" />

Thử SQLi ở thẻ Login thì không bypass được, ta qua thẻ Search để thử. Ở thẻ này có vẻ khả thi hơn vì nó có thực hiện query theo input của ta. Ví dụ:

<img src="./media/image2.png" style="width:6.5in;height:1.20278in" alt="Graphical user interface, text Description automatically generated with medium confidence" />

Đầu tiên, thử với payload đơn giản **1’ or 1=1--** , thì phát hiện nó đã bị SQLi thành công:

<img src="./media/image3.png" style="width:6.5in;height:1.59375in" alt="A picture containing text Description automatically generated" />

Ta thực hiện blind SQL để tìm kiếm thông tin infor của admin để có thể login. Ta thử với payload **1’ union select 1** , thì nhận về lỗi sau:

<img src="./media/image4.png" style="width:6.5in;height:0.78125in" />

Có thể biết được server sử dụng SQLite3, từ đó, công việc của ta cần sử dụng cú pháp của SQLite3 để mò ra các table trong database với hi vọng tìm được admin. Nhưng trước tiên, ta cần phải thực hiện dò số cột. Thay payload thành **1’ union select 1,1--** thì có vẻ đã tìm được số cột là 2:

<img src="./media/image5.png" style="width:3.87534in;height:1.46679in" alt="Graphical user interface, text, application Description automatically generated" />

Vì server dùng SQLite3, do vậy, ta cần truy vẫn các table bằng cách tìm trong **sqlite\_master** hoặc **sqlite\_schema.** Thử truy vấn với payload **1’ union select 1,name from sqlite\_master--** ta có:

<img src="./media/image6.png" style="width:5.75883in;height:2.3502in" alt="Graphical user interface, text, application, email Description automatically generated" />

Tiếp tục, ta blind vào table users *1' union select 1,1 from users--*

<img src="./media/image7.png" style="width:4.9671in;height:1.9585in" alt="Graphical user interface, text, application, email Description automatically generated" />

Tiếp tục, ta thử query tìm username và password với payload **1' union select username,password from users-- :**

<img src="./media/image8.png" style="width:5.93385in;height:2.45855in" alt="Graphical user interface, text, application, email Description automatically generated" />

Thử login thì thành công:

<img src="./media/image9.png" style="width:6.5in;height:1.92431in" alt="Graphical user interface, application Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
