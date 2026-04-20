# week 6 : Lian Yu TryHackMe

### Target Information 
- Target IP : 10.49.146.104

1. Finding open Ports

nmap -sC -sV -p- 10.49.146.104

#### Result : 
- Port 80 -> website
- Port 21 -> FTP
- Port 22 -> SSH

2. Checking the website

  http://10.49.146.104

  3. Finding Hidden Directories

used Gobuster : gobuster dir -u http://10.49.146.104 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

  ------------
1. Web Directory found :
2. File Name found :
3. FTP Password :
4. File name with SSH password :
5. user.txt:
6. root.txt :

