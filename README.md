# week 6 : Lian Yu TryHackMe

### Target Information 
- Target IP : 10.49.146.104

1. Finding open Ports

```
nmap -sC -sV -p- 10.49.146.104
```

#### Result : 
- Port 80 -> website
- Port 21 -> FTP
- Port 22 -> SSH

2. Checking the website

```
  http://10.49.146.104
```
<img width="991" height="127" alt="Screenshot 2026-04-20 213248" src="https://github.com/user-attachments/assets/d635bcb1-3263-4979-90c1-44dc24e4dc41" />

<br>

  3. Finding Hidden Directories


used Gobuster : 
```
gobuster dir -u http://10.49.146.104 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
#### Result :
- found /island

4. Exploring /island
  
<img width="1152" height="421" alt="Screenshot 2026-04-20 214211" src="https://github.com/user-attachments/assets/6b584206-d515-40ff-bfef-1bbaa8ddcda4" />

<br>

#### Questions: 
1. Web Directory found : 2100
2. File Name found :
3. FTP Password :
4. File name with SSH password :
5. user.txt:
6. root.txt :

