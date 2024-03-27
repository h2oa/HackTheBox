# HackTheBox

# nmap

nmap 1.2.3.4 -sV

# set hosts

window: C:\Windows\System32\drivers\etc
linux: /etc/hosts

# hash

`hashid hash.txt` để detect loại hash, xong dùng `hashcat`

brute force hash có dạng số theo sau:
`hashcat -a 3 -m 1400 hash.txt susan_nasus_?d?d?d?d?d?d?d?d?d`

# Kinh nghiệm

- login page: brute force, default account (tùy công nghệ)
- input: SSTI, command injection
- check `/var/mail` lấy thông tin mail nếu có
