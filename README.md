# week 6 : Lian Yu TryHackMe

### Target Information 
- Target IP : 10.49.146.104

### 1. Finding open Ports

```
nmap -sC -sV -p- 10.49.146.104
```

#### Result : 
- Port 80 -> website
- Port 21 -> FTP
- Port 22 -> SSH

### 2. Checking the website

```
  http://10.49.146.104
```
<img width="991" height="127" alt="Screenshot 2026-04-20 213248" src="https://github.com/user-attachments/assets/d635bcb1-3263-4979-90c1-44dc24e4dc41" />
<br>
<img width="1129" height="799" alt="Screenshot 2026-04-21 110227" src="https://github.com/user-attachments/assets/290da14c-8fda-4c02-bbee-009bd9af8ca2" />

<br>

###  3. Directory Brute Force


Command used : 
```
gobuster dir -u http://10.49.146.104 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
#### Result :
- /island
<img width="1010" height="658" alt="Screenshot 2026-04-21 110424" src="https://github.com/user-attachments/assets/c643206e-41e7-4f48-918e-84156312a4ac" />

<br>

### 4. Hidden Directory Analysis

  #### Found :
  - clues in source code :
<img width="685" height="367" alt="Screenshot 2026-04-20 215016" src="https://github.com/user-attachments/assets/0ba89440-a3c9-43f1-bfd6-65b57b19b7f3" />

<br>

<img width="1152" height="421" alt="Screenshot 2026-04-20 214211" src="https://github.com/user-attachments/assets/6b584206-d515-40ff-bfef-1bbaa8ddcda4" />

<br>

### 5. Clue Discovery

#### Found :
- File : .png / .jpg
- encoded data

<img width="876" height="234" alt="Screenshot 2026-04-20 220328" src="https://github.com/user-attachments/assets/f5b3019d-e6a5-4186-82ed-51383335a5ed" />

<br>

#### Action taken :
- decode using Base 58
- retrieve password

<img width="968" height="590" alt="Screenshot 2026-04-20 220554" src="https://github.com/user-attachments/assets/04e21b90-488a-4e96-a1d5-6ebb378db36e" />

  <br>
#### Questions: 
1. Web Directory found : 2100
2. File Name found :
3. FTP Password :
4. File name with SSH password :
5. user.txt:
6. root.txt :

