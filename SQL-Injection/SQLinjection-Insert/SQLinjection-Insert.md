# WRITE UP

**Challenge:** [SQL injection - Insert](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-Insert)

<img src="./media/image1.png" style="width:6.5in;height:2.09028in" alt="Graphical user interface, text, application Description automatically generated" />

Website cho ta 2 tab gồm authentication và register. Ở Register, ta có thể tùy ý tạo được account và không hề có filter input.

<img src="./media/image2.png" style="width:5.95544in;height:1.93615in" alt="Graphical user interface, text, application Description automatically generated" />

<img src="./media/image3.png" style="width:5.98037in;height:2.43987in" alt="Graphical user interface, text, application Description automatically generated" />

<img src="./media/image4.png" style="width:6.5in;height:1.90208in" alt="Graphical user interface, text, application, website Description automatically generated" />

Từ đó, ta xác định chỗ để tiêm vào database. Ở tab register, ta có thể thấy website yêu câu 3 field gồm username, password và email. Do đó, database sẽ thực hiện tạo user theo kiểu:

***INSERT INTO users VALUES (username, password, email)***

Trong khi đó, website không hề filter email field và ta có thể lợi dụng bug này để có thể INSERT thêm các giá trị ta muốn với multiple insertions và tấn công vào email field.

**Payload:** *INSERT INTO users VALUES (username, password, email), (sth, sth, attack\_payload)-- -*

<img src="./media/image5.png" style="width:6.5in;height:3.27292in" alt="Graphical user interface, text, application Description automatically generated" />

Login vào account, ***ss, ss, (select version()):***

<img src="./media/image6.png" style="width:6.5in;height:3.23264in" alt="Graphical user interface, text, application, email Description automatically generated" />

-   Database version(): **10.3.34-MariaDB-0ubuntu0.20.04.1**

Tiếp tục, ta cần fuzz để tìm ra được table và column, nhưng khi thử thì bị message “Request failed” cho đến khi sử dụng LIMIT thì mới biết là nó bị giới hạn:

<img src="./media/image7.png" style="width:6.5in;height:3.16458in" alt="Graphical user interface, text, application, email Description automatically generated" />

Thử sử dụng trick với OFFSET thì được response **“Attack detected”.**

<img src="./media/image8.png" style="width:6.5in;height:3.20139in" alt="Graphical user interface, text, application, email Description automatically generated" />

Login vào account vừa INSERT, ta biết được 1 table:

<img src="./media/image9.png" style="width:6.5in;height:2.57778in" alt="Graphical user interface, text Description automatically generated" />

Sử dụng GROUP\_CONCAT để show các table nhưng có vẻ không có tables nào có thông tin user hoặc flag mà toàn là các table khác.:

<img src="./media/image10.png" style="width:6.5in;height:2.48125in" alt="Graphical user interface, text, application Description automatically generated" />

<img src="./media/image11.png" style="width:6.5in;height:3.03889in" alt="Graphical user interface, text, application, email Description automatically generated" />

Thử xem lại version, ta thấy server sử dụng MariaDB. Sau một hồi stuck và check cheatsheet, ta có thể sử dụng **information\_schema.processlist** để check các thread đang thực thi của server database (vì user có thể reg bất cứ lúc nào). Lúc này, ta có thể kiểm tra table **INFO** để có thể xem server sẽ thực thi cái gì khi reg account ([Information Schema PROCESSLIST Table - MariaDB Knowledge Base](https://mariadb.com/kb/en/information-schema-processlist-table/)):

<img src="./media/image12.png" style="width:5.99323in;height:2.98848in" alt="Graphical user interface, text, application, email Description automatically generated" />

Reg acc để show table **INFO** của **information\_schema.processlist**:

<img src="./media/image13.png" style="width:6.32601in;height:2.75749in" alt="Graphical user interface, text Description automatically generated" />

<img src="./media/image14.png" style="width:6.37083in;height:2.61121in" alt="Graphical user interface, text, application, email Description automatically generated" />

Payload thực thi của server:

***INSERT INTO \`membres\` ( \`username\`, \`password\`, \`email\`)***

-   Table cần tìm: **membres**

Show các column của membres table:

<img src="./media/image15.png" style="width:6.5in;height:2.81597in" alt="Graphical user interface, text, email Description automatically generated" />

Tuy vậy, ta chẳng kiếm được bất kỳ thông tin nào từ bảng membres này cả

Sau 2 tiếng stuck, vì quá bất lực, em quyết định sử dụng burpsuite để bruteforce tất cả các table của **information\_schema.tables:**

-   Auto register account:

<img src="./media/image16.png" style="width:6.5in;height:3.27083in" alt="Graphical user interface, application Description automatically generated" />

-   Auto login:

<img src="./media/image17.png" style="width:6.5in;height:3.64375in" alt="Graphical user interface, application Description automatically generated" />

-   Sau khi xem qua các table mà bruteforce giúp ta leak, ta đã tìm được đúng table cần tìm :

<img src="./media/image18.png" style="width:6.5in;height:3.50972in" alt="Graphical user interface, application Description automatically generated" />

Đến đây, ta thực hiện tìm column trong flag table:

-   Payload: *username=uuysyy&password=123&email=gg'),('cgc','123',(select column\_name from information\_schema.columns where table\_name='flag' limit 0,1))-- -*

<img src="./media/image19.png" style="width:6.5in;height:3.40139in" alt="Graphical user interface, text Description automatically generated" />

Giờ thì tìm flag:

*username=sadadas&password=123&email=gg'),('cvb','123',(select flag from flag limit 0,1))-- -*

<img src="./media/image20.png" style="width:6.5in;height:3.20903in" alt="Graphical user interface, text, application, email Description automatically generated" />

-   Flag: moaZ63rVXUhlQ8tVS7Hw

<img src="./media/image21.png" style="width:6.5in;height:3.29722in" alt="Graphical user interface, text, application Description automatically generated" />

**Flag:** moaZ63rVXUhlQ8tVS7Hw

\- Flag:
