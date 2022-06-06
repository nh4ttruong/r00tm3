# Steganography
Root-me link for this subject: [https://www.root-me.org/en/Challenges/Steganography/](https://www.root-me.org/en/Challenges/Steganography/)

Lưu ý: Đây chỉ là hướng giải của mình và có thể nó sẽ không đúng với thời điểm bạn giải. Bên cạnh đó, flag đã bị mình thay thế thành \*\*\*\*\*\*\* để tuân theo tiêu chuẩn của root-me.

## EXIF - Metadata

Link challenges: <https://www.root-me.org/en/Challenges/Steganography/EXIF-Metadata>

Sử dụng tool để xem exifdata: <https://www.metadata2go.com/>

Ta tìm được GPS location: **43 deg 17' 56.27" N, 5 deg 22' 49.38" E**

<img src="./media/image1.png" style="width:6.6875in;height:4.125in" alt="Graphical user interface, application Description automatically generated" />

Sử dụng Google Maps để định vị location ta tìm được địa chỉ tại: **2 Pl. des Capucines, 13001 Marseille, France:**

<img src="./media/image2.png" style="width:5.91314in;height:2.79017in" alt="Map Description automatically generated" />

Flag là thành phố nơi chụp bức ảnh.

**Flag:** \*\*\*\*\*\*\*

<img src="./media/image3.png" style="width:6.6875in;height:3.69306in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

## Dot and next line

Hình ảnh được cho:

<img src="./media/image4.jpeg" style="width:5.58276in;height:4.35606in" alt="Text, letter Description automatically generated" />

Chú ý vào title của challenge, ta có ‘dot’ và ‘next line’ là hai keyword. Chú ý vào hình ảnh được cho, ta có thể thấy được sự sắp xếp ngẫu nhiên và không có quy tắc của các dấu chấm và cả xuống dòng.

Từ tên của challenge, ta đặt ra 2 giả thuyết:

\- Ghép các ký tự bên dưới dấu chấm lại với nhau (dot and next line)

\- Và ngược lại (line and next dot)

Từ đó, ta có 2 kết quả:

\- urpa de (không có nghĩa và dư thừa khoảng trắng)

\- chatelet15h

Submit và thành công

**Flag**: \*\*\*\*\*\*\*

<img src="./media/image5.png" style="width:6.6875in;height:3.74167in" alt="A screenshot of a computer screen Description automatically generated" />

## Steganomobile

Link: <https://www.root-me.org/en/Challenges/Steganography/Steganomobile>

<img src="./media/image6.png" style="width:6.6875in;height:1.11944in" alt="Graphical user interface, text Description automatically generated" />

Sử dụng công cụ <https://dcode.fr> để decode nó dưới dạng Multi-Tap Phone ta được kết quả là CELLPHONE.

<img src="./media/image7.png" style="width:6.6875in;height:2.45833in" alt="Graphical user interface, text, website Description automatically generated" />

Thử nhập kết quả nhưng sai. Chuyển sang lowercase thì submit thành công!

**Flag:** \*\*\*\*\*\*\*

<img src="./media/image8.png" style="width:6.6875in;height:3.225in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

## Twitter Secret Messages

Link: <https://www.root-me.org/en/Challenges/Steganography/Twitter-Secret-Messages>

Sử dụng công cụ Twtitter Secret Message: <https://holloway.nz/steg/>

<img src="./media/image9.png" style="width:6.6875in;height:2.53472in" alt="Graphical user interface, application Description automatically generated" />

Ta nhận được message: **rendezvous at grand central terminal on friday.**

**Flag:** \*\*\*\*\*\*\*

<img src="./media/image10.png" style="width:6.6875in;height:3.34792in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

## Poem from Space

Link: <https://www.root-me.org/en/Challenges/Steganography/Poem-from-Space>

<img src="./media/image11.png" style="width:6.6875in;height:3.93958in" alt="Text Description automatically generated" />

Bôi đen file, ta thấy được file có lồng thêm những khoảng trắng (whitespace):

<img src="./media/image12.png" style="width:6.6875in;height:3.34861in" alt="Chart, funnel chart Description automatically generated" />

Đây có thể là Whitespace Language. Ta remove các ký tự latin đằng trước đi và để lại các khoảng trắng dư thừa.

Sử dụng công cụ Whitespace Language decode để decode:

<img src="./media/image13.png" style="width:6.6875in;height:3.21319in" alt="Text Description automatically generated with medium confidence" />

**Flag:** RootMe{\*\*\*\*\*\*\*}

<img src="./media/image14.png" style="width:6.6875in;height:3.4625in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

## Yellow dots

Link: <https://www.root-me.org/en/Challenges/Steganography/Yellow-dots>

<img src="./media/image15.png" style="width:6.6875in;height:3.63264in" alt="Text Description automatically generated" />

Tên bài là Yellow dots, ta có thể liên tưởng đến printer. Sử dụng stegsolve để tìm ra điểm khác biệt trong file ảnh:

<img src="./media/image16.png" style="width:6.6875in;height:3.11319in" alt="Text Description automatically generated" />

Hình ảnh khác biệt hiện ra, ta có thể dò nó theo printer serial:

<img src="./media/image17.png" style="width:3.06456in;height:1.64391in" alt="A picture containing calendar Description automatically generated" />

Ta có bảng dò như sau:

<img src="./media/image18.png" style="width:6.6875in;height:3.21597in" alt="Table, Excel Description automatically generated" />

**Flag:** \*\*\*\*\*\*\*

<img src="./media/image19.png" style="width:6.6875in;height:3.70972in" alt="A screenshot of a computer screen Description automatically generated with medium confidence" />

## WAV - Noise analysis

Link:<https://www.root-me.org/en/Challenges/Steganography/WAV-Noise-analysis>

Đề bài là một file ch3.wav. Mở lên nghe thì rất khó chịu. Phân tích metadata thì không thu thập được bất cứ gì.

Sử dụng công cụ Audicity để modify âm thanh. Sau nhiều lần thử thì công thức cho ra được một đoạn voice tiếng anh là: Speed Low (giảm còn 30%) + Reverse (đảo ngược đoạn âm thanh):

<img src="./media/image20.png" style="width:6.6875in;height:2.74167in" alt="A screenshot of a computer Description automatically generated" />

Nghe lại ta có được flag: **3b27641fc5h0**

**Flag:** \*\*\*\*\*\*\*

<img src="./media/image21.png" style="width:6.6875in;height:3.75556in" alt="A screenshot of a computer Description automatically generated" />

## EXIF - Thumbnail

Link: <https://www.root-me.org/en/Challenges/Steganography/EXIF-Thumbnail>

Strings thử file thì thấy mấy không tìm được gì đặc biệt, kể cả exiftool:

<img src="./media/image22.png" style="width:6.6875in;height:2.80278in" alt="Graphical user interface, application, Teams Description automatically generated" />

Sử dụng công cụ bóc tách thumbnail, <https://29a.ch/photo-forensics/#thumbnail-analysis>, ta được flag:

<img src="./media/image23.png" style="width:5.39044in;height:2.66276in" alt="A screenshot of a computer Description automatically generated" />

**Flag:** \*\*\*\*\*\*\*

<img src="./media/image24.png" style="width:5.11364in;height:2.87967in" alt="A screenshot of a computer Description automatically generated" />

## WAV-Spectral-analysis

Link: <https://www.root-me.org/en/Challenges/Steganography/WAV-Spectral-analysis>

Sử dụng Audicity tool và chọn chế độ Spectogram để xem. Ta có thể xem được sóng và nó hình thành đoạn text:

<img src="./media/image25.png" style="width:6.6875in;height:4.23611in" alt="Graphical user interface, application Description automatically generated" />

**Flag:** \*\*\*\*\*\*\*

<img src="./media/image26.png" style="width:5.41196in;height:3.15051in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

## APNG – Just a PNG

Link: <https://www.root-me.org/en/Challenges/Steganography/APNG-Just-A-PNG>

Exiftool kiểm tra file:

<img src="./media/image27.png" style="width:6.6875in;height:3.15in" alt="Graphical user interface, text Description automatically generated" />

Sử dụng công cụ APNG Disassembler 2.9 để extract .apng ra nhiều frame:

<img src="./media/image28.png" style="width:6.6875in;height:2.97083in" alt="A screenshot of a computer Description automatically generated" />

Kiểm tra thư mục xuất ra thì có các file text là frame data. Mở các file đầu lên thì thấy các thông số frame có vẻ như đã bị ASCII hóa. Thử dịch ngược lại 4 file đầu thì ra chữ FLAG (70 76 65 71):

<img src="./media/image29.png" style="width:5.90567in;height:2.80811in" alt="Graphical user interface Description automatically generated" />

Sử dụng python để decode và ta được flag:

<img src="./media/image30.png" style="width:5.92433in;height:2.70132in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

**Flag:** \*\*\*\*\*\*\*

<img src="./media/image31.png" style="width:5.34073in;height:3.05303in" alt="A screenshot of a computer Description automatically generated" />

## TXT - George and Alfred

Link: <https://www.root-me.org/en/Challenges/Steganography/TXT-George-and-Alfred>

Mở challenge, ta tìm được đoạn text là bài thơ:

<img src="./media/image32.png" style="width:6.6875in;height:3.26042in" alt="Text Description automatically generated" />

Ở cuối bài, người ta có để một cái hint:

<img src="./media/image33.png" style="width:6.23387in;height:1.81682in" alt="A screenshot of a computer Description automatically generated" />

Mở bài gốc, ta biết được, những từ đầu hàng ở đoạn cuối là lời mà Musset gửi đến Georges. Bản của challenge đã thay dòng **“La réponse de Georges Sand :”** à **“De la même manière George Sand a répondu ceci :”.** Dựa vào hint, ở trên, ta có thể đoán được “phrase cachée” là **Cette Nuit**. Thử flag thì thấy passed!

**Flag:** \*\*\*\*\*\*\*

<img src="./media/image34.png" style="width:6.6875in;height:3.76875in" alt="A screenshot of a computer Description automatically generated" />

## Embedded PDF

Sử dụng **pdf-parser** để xem cấu trúc của file pdf:

**pdf-parser -w epreuve\_BAC\_2004.pdf**

<img src="./media/image35.png" style="width:6.6875in;height:3.86806in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

Ta thấy, file **Hidden\_b33rs.txt** được embedded trong pdf. Do vậy, sử dụng **peepdf** để xem cấu trúc của stream thì thấy Filespec nằm ở object 78, từ đó, ta sẽ extract object 78 ra file:

<img src="./media/image36.png" style="width:6.6875in;height:3.89375in" alt="Text Description automatically generated" />

Extract obect 78 ra hiddenpdf.txt:

<img src="./media/image37.png" style="width:6.6875in;height:3.12083in" alt="Text Description automatically generated" />

File hiddenpdf.txt:

<img src="./media/image38.png" style="width:6.6875in;height:3.18403in" alt="Graphical user interface, text Description automatically generated" />

Data đã bị encode base64, decode nó và xem header thì phát hiện đây là file JFIF:

<img src="./media/image39.png" style="width:5.74216in;height:1.33345in" alt="Text Description automatically generated" />

Xuất ra file hidden.jpg, ta có flag:

<img src="./media/image40.png" style="width:6.6875in;height:3.29375in" alt="Graphical user interface, application, Teams Description automatically generated" />

**Flag:** \*\*\*\*\*\*\*

<img src="./media/image41.png" style="width:6.6875in;height:3.72569in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

## Kitty spy

Link: <https://www.root-me.org/en/Challenges/Steganography/Kitty-spy>

Binwalk file ch16.jpg ta thấy được các file zip lồng trong file img:

<img src="./media/image42.png" style="width:6.6875in;height:1.67431in" alt="Text Description automatically generated" />

Extract các file zip ra:

<img src="./media/image43.png" style="width:6.6875in;height:2.43611in" alt="A picture containing text Description automatically generated" />

<img src="./media/image44.png" style="width:6.56724in;height:0.70839in" />

Trong step 1, ta có:

<img src="./media/image45.png" style="width:6.6875in;height:3.25625in" alt="Graphical user interface, map Description automatically generated" />

Sử dụng stegsolve để xem ảnh dưới nhiều dạng:

<img src="./media/image46.png" style="width:6.6875in;height:4.40556in" alt="Map Description automatically generated" />

Ta được flag ở step1: **\*\*\*\*\*\*\*** (hihi encrypted flag)

Đến step2, ta unzip với pass là flag ở step1:

<img src="./media/image47.png" style="width:6.1922in;height:1.15843in" alt="Text Description automatically generated" />

Đọc file README\\#2.txt, ta nhận được một đoạn chữ số khả nghi là MD5: **18574115dbcd47d71e7eb9da74e45bf2**

<img src="./media/image48.png" style="width:6.6875in;height:1.10208in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

Sử dụng tool thử tìm đoạn plaintext của nó:

<img src="./media/image49.png" style="width:6.6875in;height:2.53542in" alt="Graphical user interface, application, website Description automatically generated" />

Ta có key: **\*\*\*\*\*\*\*** (hihi encrypted key). Sử dụng steghide để extract file từ monster.wav:

<img src="./media/image50.png" style="width:6.6875in;height:1.12292in" alt="Text Description automatically generated" />

Ta tìm được password ở step 2: **s3c0nDSt3pIsAls0D0n3**

Đến step3, ta có một source web nghi ngờ. Mở file README trong source code, ta nhận được dòng có nội dung như kiểu QR Code sẽ là key ở web này liên quan đến flag:

<img src="./media/image51.png" style="width:6.6875in;height:3.23958in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

Mở file LICENSE.md, ta nhận được một đoạn BrainFuck:

<img src="./media/image52.png" style="width:6.6875in;height:1.35347in" alt="A screenshot of a computer Description automatically generated with low confidence" />

Decode và y như dự đoán rằng, có thể QR Code sẽ hỗ trợ ta ở step này:

<img src="./media/image53.png" style="width:6.6875in;height:1.32153in" alt="Graphical user interface, application Description automatically generated" />

Ở file index.html, ta có được message sau:

<img src="./media/image54.png" style="width:6.6875in;height:1.88403in" alt="A picture containing graphical user interface Description automatically generated" />

Tui bị dừng lại ở đây là chưa nghĩ ra hướng tiếp theo.

## Crypto Art

<img src="./media/image55.png" style="width:4.56801in;height:0.88587in" alt="Text Description automatically generated with medium confidence" />

Đây là file Netpbm với đuôi là .ppm.

String file và ta được thông điệp:

<img src="./media/image56.png" style="width:5.74244in;height:1.60759in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

Sử dụng dcode.fr để tiên đoán cipher và ta thấy nó hợp nhất Vigenere:

<img src="./media/image57.png" style="width:4.24261in;height:2.58151in" alt="Graphical user interface, text, application Description automatically generated" />

Sau một hồi không thể auto bruteforce được Vigenere thì bài này có lẽ cần phải có key mới có thể decode. Tìm hiểu về ppm thì em phát hiện nó có thể chèn thêm text vào trong đó (hide). Sử dụng npiet language để phiên dịch nó thử:

<img src="./media/image58.png" style="width:5.8474in;height:2.14668in" alt="Graphical user interface, text, application, email Description automatically generated" />

Cuối cùng ta có key: EYJF**** (hihi encrypted key)

Decode và nhận kết quả:

<img src="./media/image59.png" style="width:4.54406in;height:2.08173in" alt="Graphical user interface, application Description automatically generated" />

**Flag:** \*\*\*\*\*\*\*

<img src="./media/image60.png" style="width:6.1561in;height:3.31905in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

## PNG - Pixel Indicator Technique

Pixel Indicator Technique là kỹ thuật ẩn giấu thông tin vào pixel của ảnh. Sử dụng công cụ stegopit (chuyên cho PIT) để phân tích ảnh của challenge:

<img src="./media/image61.png" style="width:5.55887in;height:1.97651in" alt="Graphical user interface Description automatically generated with medium confidence" />

Và ta tìm được hidden data:

**Flag:** **\*\*\*\*\*\*\***

<img src="./media/image62.png" style="width:4.4429in;height:2.48304in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

## PNG - Pixel Value Differencing

Đây là challenge dựa trên kỹ thuật PVD (Pixel Value Differencing) để ẩn dấu message trong png. Tương tự challenge, ta sử dụng công cụ **stegopvd (**[Tinyscript steganography tool implementing the Pixel Value Differencing algorithm · GitHub](https://gist.github.com/dhondta/feaf4f5fb3ed8d1eb7515abe8cde4880)) để extract message:

<img src="./media/image63.png" style="width:6.6875in;height:1.65139in" alt="Graphical user interface Description automatically generated" />

**Flag:** **\*\*\*\*\*\*\***

<img src="./media/image64.png" style="width:5.93409in;height:3.41503in" alt="A screenshot of a computer Description automatically generated" />
