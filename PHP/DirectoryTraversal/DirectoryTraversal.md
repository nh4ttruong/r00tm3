# WRITE UP

**Challenge:** [Directory Traversal](https://www.root-me.org/en/Challenges/Web-Server/Directory-traversal)

<img src="./media/image1.png" style="width:6.13757in;height:2.60322in" alt="Graphical user interface, text, application Description automatically generated" />

Thử tìm các hình ảnh ở các tab, không phát hiện điều gì khác biệt. Chú ý đến **URL** <http://challenge01.root-me.org/web-serveur/ch15/ch15.php?galerie=emotes> có *galerie=\[value\].* Ta thử xóa đi value để website trả về dạng ‘index’:

<img src="./media/image2.png" style="width:6.19367in;height:3.29998in" alt="Graphical user interface, text, application Description automatically generated" />

Lúc này, website trả về một **alt=“86hwnX2r”.** Chọn “Open image in new window” thì nhận được 403 Forbidden:

<img src="./media/image3.png" style="width:6.21377in;height:1.32108in" alt="Graphical user interface, text, application Description automatically generated" />

Có lẽ galerie lúc này phải là null hoặc bằng value nào đó. Ta back về ch15.php source web và add vào source link của ảnh đó <http://challenge01.root-me.org/web-serveur/ch15/ch15.php?galerie=86hwnX2r> ta chuyển đến trang khác:

<img src="./media/image4.png" style="width:6.26122in;height:2.52723in" alt="Graphical user interface, text, application Description automatically generated" />

Ảnh password đã xuất hiện, truy cập source password và nhận password <https://challenge01.root-me.org/web-serveur/ch15/galerie/86hwnX2r/password.txt>

<img src="./media/image5.png" style="width:6.27696in;height:2.49469in" alt="Graphical user interface, text Description automatically generated" />

<img src="./media/image6.png" style="width:6.5in;height:3.63333in" alt="A screenshot of a computer Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
