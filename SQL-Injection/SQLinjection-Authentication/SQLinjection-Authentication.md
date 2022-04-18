# WRITE UP

**Challenge:** [SQL injection - Authentication](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-authentication)

<img src="./media/image1.png" style="width:4.53264in;height:2.20094in" alt="Graphical user interface, text, application, website Description automatically generated" />

Thử với payload:

-   Username: 1’--

-   Password: 1

<img src="./media/image2.png" style="width:4.10869in;height:0.8084in" alt="A picture containing logo Description automatically generated" />

Như vậy, ta không thể inject được vào input. Thử inject vào password:

-   Username: 1

-   Password: 1’ or 1=1--

<img src="./media/image3.png" style="width:4.68253in;height:2.04271in" alt="Graphical user interface, application Description automatically generated" />

Ta có thể đoán được, có vẻ như cần phải có username chính xác mới có thể inject được ở username, thử kiểm chứng bằng cách inject ở username với payload “user1—".

<img src="./media/image3.png" style="width:4.68253in;height:1.27739in" alt="Graphical user interface, application Description automatically generated" />

Như vậy, để trộm được password của admin, ta cần phải biết username của admin để thực hiện inject. Và nhờ informations hiển thị của user1, ta có thể đoán username của admin có thể là **admin** hoặc **administrator.**

**Thử với payload:**

-   Username: admin’--

-   Password: 1

<img src="./media/image4.png" style="width:4.59206in;height:2.25853in" alt="Graphical user interface, text, application, email Description automatically generated" />

Inspect và tìm được password của admin:

<img src="./media/image5.png" style="width:4.6254in;height:1.36678in" alt="Text Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
