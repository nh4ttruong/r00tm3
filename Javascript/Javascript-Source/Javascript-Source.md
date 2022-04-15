# WRITE UP

## Challenge: [Javascript - Source](https://www.root-me.org/en/Challenges/Web-Client/Javascript-Source)

Vào website, ta thấy có một ô alert hiện ra bắt ta nhập mật khẩu:

![A screenshot of a computer Description automatically generated with medium confidence](./media/image1.png){width="5.958772965879265in" height="1.0325995188101487in"}

Kiểm tra Sources của website, ta thấy một file (index):

![Text Description automatically generated](./media/image2.png){width="5.908790463692038in" height="2.101534339457568in"}

Đến đây, ta có thể thấy, body sẽ sử dụng event onload để chạy hàm login(), hàm login() sẽ so sánh password với chuỗi \"123456azerty\", do đó, ta sẽ sử dụng chuỗi này để nhập vào ô alert ban đầu cũng như vào password của challenge.

![A screenshot of a computer Description automatically generated](./media/image3.png){width="4.184514435695538in" height="2.0515726159230097in"}

**Password:** **123456azerty**
