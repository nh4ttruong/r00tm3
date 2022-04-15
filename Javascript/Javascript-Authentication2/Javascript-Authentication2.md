# WRITE UP

## Challenge: [Javascript - Authentication 2](https://www.root-me.org/en/Challenges/Web-Client/Javascript-Authentication-2)

Vào website, ta thấy có một nút login và một thẻ \<a\> để đóng của sổ:

![Rectangle Description automatically generated with medium confidence](./media/image1.png){width="5.945615704286964in" height="1.113532370953631in"}

Click vào login button, website sẽ hiện 2 ô alert lần lượt là username và password. Kiểm tra Sources website, ta thấy có file login.js:

![Text Description automatically generated](./media/image2.png){width="5.779342738407699in" height="2.138850612423447in"}

Ta thấy, script so sánh username == TheUsername && password == ThePassword. Trong khi đó TheUsername và ThePassword lần lượt là TheSplit\[0\] và TheSplit\[1\]. Từ đó với **var TheLists = \[\"GOD:HIDDEN\"\]**, ta có thể suy ra:

-   Username: GOD

-   ![](./media/image3.png){width="3.6875in" height="1.7243055555555555in"}Password: HIDDEN

**Password:** **HIDDEN**
