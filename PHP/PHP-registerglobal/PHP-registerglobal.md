# WRITE UP

**Challenge:** [PHP – register globals](https://www.root-me.org/en/Challenges/Web-Server/PHP-register-globals)

Theo document, ta có các global variable thường gặp là: '\_REQUEST', '\_SESSION', '\_SERVER', '\_ENV', '\_FILES'. Kiểm tra cookie của website, ta có thể thấy được PHP Session ID. Từ đó, ta có thể đoán được website có thể sử dụng \_SESSION để lưu trữ mảng các session ([PHP: $\_SESSION - Manual](https://www.php.net/manual/en/reserved.variables.session.php)).

<img src="./media/image1.png" style="width:6.5in;height:2.45764in" alt="Graphical user interface, application Description automatically generated" />

Thử bằng payload với **/index.php?\_SESSION\[*logged*\]=1**, ta tìm được password:

<img src="./media/image2.png" style="width:6.5in;height:1.88611in" alt="Graphical user interface, text, application Description automatically generated" />

-   Password: **NoTQYipcRKkgrqG**

<img src="./media/image3.png" style="width:6.5in;height:3.67431in" alt="A screenshot of a computer Description automatically generated" />

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
