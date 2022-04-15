# WRITE UP

**Challenge:** [SQL injection - Insert](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-Insert)

![Graphical user interface, text, application Description automatically generated](./media/image1.png){width="6.5in" height="2.0902777777777777in"}

Website cho ta 2 tab gồm authentication và register. Ở Register, ta có thể tùy ý tạo được account và không hề có filter input.

![Graphical user interface, text, application Description automatically generated](./media/image2.png){width="5.9554363517060365in" height="1.9361526684164478in"}

![Graphical user interface, text, application Description automatically generated](./media/image3.png){width="5.980374015748032in" height="2.439869860017498in"}

![Graphical user interface, text, application, website Description automatically generated](./media/image4.png){width="6.5in" height="1.9020833333333333in"}

Từ đó, ta xác định chỗ để tiêm vào database. Ở tab register, ta có thể thấy website yêu câu 3 field gồm username, password và email. Do đó, database sẽ thực hiện tạo user theo kiểu:

***INSERT INTO users VALUES (username, password, email)***

Trong khi đó, website không hề filter email field và ta có thể lợi dụng bug này để có thể INSERT thêm các giá trị ta muốn với multiple insertions và tấn công vào email field.

**Payload:** *INSERT INTO users VALUES (username, password, email), (sth, sth, attack_payload)\-- -*

![Graphical user interface, text, application Description automatically generated](./media/image5.png){width="6.5in" height="3.2729166666666667in"}

Login vào account, ***ss, ss, (select version()):***

![Graphical user interface, text, application, email Description automatically generated](./media/image6.png){width="6.5in" height="3.232638888888889in"}

-   Database version(): **10.3.34-MariaDB-0ubuntu0.20.04.1**

Tiếp tục, ta cần fuzz để tìm ra được table và column, nhưng khi thử thì bị message "Request failed" cho đến khi sử dụng LIMIT thì mới biết là nó bị giới hạn:

![Graphical user interface, text, application, email Description automatically generated](./media/image7.png){width="6.5in" height="3.1645833333333333in"}

Thử sử dụng trick với OFFSET thì được response **"Attack detected".**

![Graphical user interface, text, application, email Description automatically generated](./media/image8.png){width="6.5in" height="3.201388888888889in"}

Login vào account vừa INSERT, ta biết được 1 table:

![Graphical user interface, text Description automatically generated](./media/image9.png){width="6.5in" height="2.577777777777778in"}

Sử dụng GROUP_CONCAT để show các table nhưng có vẻ không có tables nào có thông tin user hoặc flag mà toàn là các table khác.:

![Graphical user interface, text, application Description automatically generated](./media/image10.png){width="6.5in" height="2.48125in"}

![Graphical user interface, text, application, email Description automatically generated](./media/image11.png){width="6.5in" height="3.0388888888888888in"}

Thử xem lại version, ta thấy server sử dụng MariaDB. Sau một hồi stuck và check cheatsheet, ta có thể sử dụng **information_schema.processlist** để check các thread đang thực thi của server database (vì user có thể reg bất cứ lúc nào). Lúc này, ta có thể kiểm tra table **INFO** để có thể xem server sẽ thực thi cái gì khi reg account ([Information Schema PROCESSLIST Table - MariaDB Knowledge Base](https://mariadb.com/kb/en/information-schema-processlist-table/)):

![Graphical user interface, text, application, email Description automatically generated](./media/image12.png){width="5.993233814523185in" height="2.9884831583552054in"}

Reg acc để show table **INFO** của **information_schema.processlist**:

![Graphical user interface, text Description automatically generated](./media/image13.png){width="6.326011592300962in" height="2.7574923447069115in"}

![Graphical user interface, text, application, email Description automatically generated](./media/image14.png){width="6.370831146106736in" height="2.6112095363079617in"}

Payload thực thi của server:

***INSERT INTO \`membres\` ( \`username\`, \`password\`, \`email\`)***

-   Table cần tìm: **membres**

Show các column của membres table:

![Graphical user interface, text, email Description automatically generated](./media/image15.png){width="6.5in" height="2.8159722222222223in"}

Tuy vậy, ta chẳng kiếm được bất kỳ thông tin nào từ bảng membres này cả

Sau 2 tiếng stuck, vì quá bất lực, em quyết định sử dụng burpsuite để bruteforce tất cả các table của **information_schema.tables:**

-   Auto register account:

![Graphical user interface, application Description automatically generated](./media/image16.png){width="6.5in" height="3.2708333333333335in"}

-   Auto login:

![Graphical user interface, application Description automatically generated](./media/image17.png){width="6.5in" height="3.64375in"}

-   Sau khi xem qua các table mà bruteforce giúp ta leak, ta đã tìm được đúng table cần tìm :

![Graphical user interface, application Description automatically generated](./media/image18.png){width="6.5in" height="3.5097222222222224in"}

Đến đây, ta thực hiện tìm column trong flag table:

-   Payload: *username=uuysyy&password=123&email=gg\'),(\'cgc\',\'123\',(select column_name from information_schema.columns where table_name=\'flag\' limit 0,1))\-- -*

![Graphical user interface, text Description automatically generated](./media/image19.png){width="6.5in" height="3.401388888888889in"}

Giờ thì tìm flag:

*username=sadadas&password=123&email=gg\'),(\'cvb\',\'123\',(select flag from flag limit 0,1))\-- -*

![Graphical user interface, text, application, email Description automatically generated](./media/image20.png){width="6.5in" height="3.2090277777777776in"}

-   Flag: moaZ63rVXUhlQ8tVS7Hw

![Graphical user interface, text, application Description automatically generated](./media/image21.png){width="6.5in" height="3.297222222222222in"}

**Flag:** moaZ63rVXUhlQ8tVS7Hw
