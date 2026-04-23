# week 6 : Lian Yu TryHackMe

### 1. Introduction

⚠️ Note: The target IP address is dynamically assigned by TryHackMe. It may change each time the lab is started or reset. All commands below were executed using the active session IP during testing.

-----

### 2. Target Information 
- Target IP : 10.49.xxx.xxx 

### 3. Port Scanning

```
nmap -sC -sV -p- <target-ip>
```

#### Discovered services : 
- Port 80 -> website
- Port 21 -> FTP
- Port 22 -> SSH

<img width="1002" height="380" alt="Screenshot 2026-04-21 110130" src="https://github.com/user-attachments/assets/82f9a869-f50e-4490-add5-63d68a464bc2" />

<br>

### 4. Web Enumeration

```
  http://<target-ip>
```
<img width="1129" height="799" alt="Screenshot 2026-04-21 110227" src="https://github.com/user-attachments/assets/290da14c-8fda-4c02-bbee-009bd9af8ca2" />

<br>

###  5. Directory Brute Force

Command used : 
```
gobuster dir -u http://10.49.146.104 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
#### Result :
- /island directory found
<img width="1010" height="658" alt="Screenshot 2026-04-21 110424" src="https://github.com/user-attachments/assets/c643206e-41e7-4f48-918e-84156312a4ac" />

<br>

### 6. Hidden Directory Exploration


```
  http://<target-ip>/island/
```

<img width="945" height="406" alt="Screenshot 2026-04-21 110717" src="https://github.com/user-attachments/assets/110eb3db-64c6-48a3-93e4-c9240bda81be" />
<br>

Command used : 
```
gobuster dir -u http://10.49.153.26/island/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

#### Result :
- Additional hidden structure discovered under /island
  
<img width="1002" height="625" alt="Screenshot 2026-04-21 111240" src="https://github.com/user-attachments/assets/6be0159b-61b5-488a-88ed-62f284e73a1e" />

<br>

### 7. Deeper Hidden Path Discovery

#### Found Directory :
```
/island/2100
```
#### Checking the website

```
 http://10.49.153.26/island/2100/
```

<img width="1141" height="766" alt="Screenshot 2026-04-21 111444" src="https://github.com/user-attachments/assets/083fd5bc-7ccc-4789-bb4c-b9e3a7a4e3dd" />
<br>

  #### Found :
  - clues in source code :
<img width="685" height="367" alt="Screenshot 2026-04-20 215016" src="https://github.com/user-attachments/assets/0ba89440-a3c9-43f1-bfd6-65b57b19b7f3" />

<br>

### 8. Hidden File Discovery

Command used : 
```
gobuster dir -u http://10.49.153.26/island/2100 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x ticket
```
<img width="1004" height="663" alt="Screenshot 2026-04-21 111900" src="https://github.com/user-attachments/assets/78f5c977-a483-4372-9bfa-445800ff167a" />
<br>

#### Result :
```
green_arrow.ticket
```
### 9. Hidden File Analysis
#### Checking the website
```
 http://10.49.153.26/island/2100/green_arrow.ticket
```

#### Found :

<img width="876" height="234" alt="Screenshot 2026-04-20 220328" src="https://github.com/user-attachments/assets/f5b3019d-e6a5-4186-82ed-51383335a5ed" />

<br>

#### Action taken :
- decode using Base 58
- retrieve password

<img width="968" height="590" alt="Screenshot 2026-04-20 220554" src="https://github.com/user-attachments/assets/04e21b90-488a-4e96-a1d5-6ebb378db36e" />

  <br>

#### Result :
- FTP password :

 ```
 !#th3h00d
 ```

### 10. FTP Access

Command used :

```
ftp <target-ip>
```

#### Outcome :
- Successfully logged into FTP server
- Retrieved files:
  - .jpg
  - .png
    
<img width="995" height="661" alt="Screenshot 2026-04-21 112453" src="https://github.com/user-attachments/assets/a317ec0d-e472-44a6-b69e-3280d0320285" />

<br>  

#### Download files:
```
get aa.jpg
get .other_user
```

### 11. Steganography Analysis : 

#### Extract hidden data from image :
```
steghide extract -sf aa.jpg
```
#### Output:
- Extracted file: ss.zip

#### Unzip contents
```
unzip ss.zip
```
#### Files obtained :
- passwd.txt
- shado

#### Retrieve SSH password
```
cat shado
```
#### Result :
- SSH Password : M3tahuman

<img width="697" height="247" alt="Screenshot 2026-04-23 121546" src="https://github.com/user-attachments/assets/0ecff6fc-c675-489b-91b7-21855983bfbb" />

<br>

### 12. User Enumeration : 

### 17. Answers : 

| Question | Answer |
|----------|--------|
| Web directory found | `/2100` |
| File name found | `green_arrow.ticket` |
| FTP password | `!#th3h00d` |
| SSH password | `shado` |
| user.txt | *(to be completed)* |
| root.txt | *(to be completed)* |

