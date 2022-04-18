# WRITE UP

## Challenge: [Javascript - Authentication 2](https://www.root-me.org/en/Challenges/Web-Client/Javascript-Authentication-2)

Vào website, ta thấy có một nút login và một thẻ &lt;a&gt; để đóng của sổ:

<img src="./media/image1.png" style="width:5.94562in;height:1.11353in" alt="Rectangle Description automatically generated with medium confidence" />

Click vào login button, website sẽ hiện 2 ô alert lần lượt là username và password. Kiểm tra Sources website, ta thấy có file login.js:

<img src="./media/image2.png" style="width:5.77934in;height:2.13885in" alt="Text Description automatically generated" />

Ta thấy, script so sánh username == TheUsername && password == ThePassword. Trong khi đó TheUsername và ThePassword lần lượt là TheSplit\[0\] và TheSplit\[1\]. Từ đó với **var TheLists = \["GOD:HIDDEN"\]**, ta có thể suy ra:

-   Username: GOD

-   <img src="./media/image3.png" style="width:3.6875in;height:1.72431in" />Password: HIDDEN

\- Flag: \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
