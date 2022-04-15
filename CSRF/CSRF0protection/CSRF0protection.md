# WRITE UP

**Challenge:** [CSRF - 0 protection](https://www.root-me.org/en/Challenges/Web-Client/CSRF-0-protection)

Tạo tài khoản và login vào website:

![Graphical user interface, application Description automatically generated](./media/image1.png){width="6.5in" height="2.2875in"}

Ở tab Profile, khi ta thực hiện submit thử thì nhận được message:

![Graphical user interface Description automatically generated with low confidence](./media/image2.png){width="3.733657042869641in" height="0.9250798337707786in"}

Ở tab Contact, ta có thể thấy form với method="post", submit thử thì ta nhận được message:

![Graphical user interface, text, application, email Description automatically generated](./media/image3.png){width="4.531679790026247in" height="2.2594564741907264in"}

Qua tab Private, ta thấy message:

![Graphical user interface, text, application Description automatically generated](./media/image4.png){width="5.342129265091864in" height="1.3167804024496939in"}

Từ đó, ta có thể đoán ra rằng, nội dung ở tab Contact sẽ được post lên và được admin kiểm duyệt Admin có thể click vào message của ta Có thể tấn công CSRF.

Để xem được tab Private, ta cần phải xác thực được Profile và từ đó ta có thể đoán được ý đồ của việc disable của nút Status là có lý do của nó. Tuy vậy, chỉ có admin mới có thể xác thực account. Kết hợp với suy luận ở trên, ta có thể thực hiện CSRF giả mạo gửi content đến cho admin và khiến script chạy để admin submit form cho ta.

Qua tab Profile, inspect element và thực hiện giả mạo một form tương tự form ở tab Profile. Sau đó, chèn thêm script để admin có thể submit form:

\<form id=\"clickme\" action=\"http://challenge01.root-me.org/web-client/ch22/?action=profile\" method=\"post\" enctype=\"multipart/form-data\"\>

\<input type=\"text\" name=\"username\" value=\"19522445\"\>

\<input type=\"checkbox\" name=\"status\" checked\>

\</form\>

\<script\>document.getElementById(\"clickme\").submit();\</script\>

![Graphical user interface, text, application, email Description automatically generated](./media/image5.png){width="5.983851706036745in" height="3.141938976377953in"}

Submit để gửi contact đến admin và qua tab Private để kiểm tra kết quả. Sau hơn 1 phút, ta nhận được flag:

![Graphical user interface, application Description automatically generated with medium confidence](./media/image6.png){width="5.9588495188101485in" height="1.841826334208224in"}

**Flag:** Csrf_Fr33style-L3v3l1!
