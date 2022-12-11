# Docker layers

Challenge: [https://www.root-me.org/fr/Challenges/Forensic/Docker-layers](https://www.root-me.org/fr/Challenges/Forensic/Docker-layers)

Sử dụng `container-diff` để analyze history của file `.tar`

```
container-diff analyze -t history ch29.tar

-----History-----

Analysis for ch29.tar:
-/bin/sh -c #(nop) ADD file:d2abf27fe2e8b0b5f4da68c018560c73e11c53098329246e3e6fe176698ef941 in /
-/bin/sh -c #(nop)  CMD ["bash"]
-/bin/sh -c apt update -y
-/bin/sh -c apt install -y curl openssl
-/bin/sh -c #(nop) COPY file:2ca89eb39686ffcc3d2d87bbc9293559252cff471f80c2ed5d024b214f9a6fa3 in /
-/bin/sh -c echo -n $(curl -s https://pastebin.com/raw/P9Nkw866) | openssl enc -aes-256-cbc -iter 10 -pass pass:$(cat /pass.txt) -out flag.enc
-/bin/sh -c rm /pass.tx
```

Ta thấy, tác giả sử dụng encrypt file flag lấy từ https://pastebin.com/raw/P9Nkw866 (not found) và encrypt với password được mount tại /pass.txt từ một file local.

Giờ thì untar file `ch29.tar` ra và tìm kiếm flag:

```
 1bbd61a572ad5f5e2ac0f073465d10dc1c94a71359b0adfd2c105be4c1cb2507
 316bbb8c58be42c73eefeb8fc0fdc6abb99bf3d5686dd5145fc7bb2f32790229.tar
 3309d6da2bd696689a815f55f18db3f173bc9b9a180e5616faf4927436cf199d.tar
 4942a1abcbfa1c325b1d7ed93d3cf6020f555be706672308a4a4a6b6d631d2e7.tar
 5bcc45940862d5b93517a60629b05c844df751c9187a293d982047f01615cb30
 743c70a5f809c27d5c396f7ece611bc2d7c85186f9fdeb68f70986ec6e4d165f.tar
 82ba49da0bd5d767f35d4ae9507d6c4552f74e10f29777a2a27c97778962476d
 8d364403e7bf70d7f57e807803892edf7304760352a397983ecccb3e76ca39fa.tar
 8f0d75885373613641edc42db2a0007684a0e5de14c6f854e365c61f292f3b4d
 b324f85f8104bfebd1ed873e90437c0235d7a43f025a047d5695fe461da717c6.json
 b58c5e8ccaba8886661ddd3b315989f5cf7839ea06bbe36547c6f49993b0d0aa.tar
 ca7f60c6e2a66972abcc3147da47397d1c2edb80bddf0db8ef94770ed28c5e16
 db04fe239ab708e4ab56ea0e5c1047449b7ea9e04df9db5b1b95d00c6980ff3f
 flag.enc
 manifest.json
 openssl
 repositories
```

Unzip tiếp các file `.tar` còn lại sẽ xuất hiện file `flag.enc` và `pass.txt`:

```
cat pass.txt
d4428185a6202a1c5806d7cf4a0bb738a05c03573316fe18ba4eb5a21a1bc8ea
```

```
cat flag.enc
Salted__s`;?�d�q���/�!����$@�����8�=NK:�E�n%���.N��02)�d
```

Sử dụng `openssl` để descrypt `flag.enc`:

```
openssl enc -aes-256-cbc -iter 10 -d -in flag.enc -out flag.txt
```

Và nhận flag: `cat flag.txt *******************`
