# WRITE UP

**Challenge:** [SQL injection - Authentication](https://www.root-me.org/en/Challenges/Web-Server/SQL-injection-authentication)

![Graphical user interface, text, application, website Description automatically generated](./media/image1.png){width="4.532635608048994in" height="2.200942694663167in"}

Thử với payload:

-   Username: 1'\--

-   Password: 1

![A picture containing logo Description automatically generated](./media/image2.png){width="4.108689851268592in" height="0.808403324584427in"}

Như vậy, ta không thể inject được vào input. Thử inject vào password:

-   Username: 1

-   Password: 1' or 1=1\--

![Graphical user interface, application Description automatically generated](./media/image3.png){width="4.682525153105861in" height="2.0427121609798777in"}

Ta có thể đoán được, có vẻ như cần phải có username chính xác mới có thể inject được ở username, thử kiểm chứng bằng cách inject ở username với payload "user1---\".

![Graphical user interface, application Description automatically generated](./media/image3.png){width="4.682525153105861in" height="1.2773906386701663in"}

Như vậy, để trộm được password của admin, ta cần phải biết username của admin để thực hiện inject. Và nhờ informations hiển thị của user1, ta có thể đoán username của admin có thể là **admin** hoặc **administrator.**

**Thử với payload:**

-   Username: admin'\--

-   Password: 1

![Graphical user interface, text, application, email Description automatically generated](./media/image4.png){width="4.5920647419072615in" height="2.258529090113736in"}

Inspect và tìm được password của admin:

![Text Description automatically generated](./media/image5.png){width="4.62540135608049in" height="1.3667847769028871in"}

**Flag:** t0_W34k!\$
