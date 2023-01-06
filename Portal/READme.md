# Portal!
## @Author : M3tr1c_r00t
![Screenshot_2023-01-05_22_20_46 (2)](https://user-images.githubusercontent.com/99975622/211106353-ff5542a2-5290-4e50-930b-15844d4ee0e3.png)

Portal is a linux easy machine which exploited the vsftpd 2.3.4 Backdoor Command Execution...

### Enumeration...
```
# Nmap 7.93 scan initiated Thu Jan  5 22:16:33 2023 as: nmap -sC -sV -A -p 21,22 -oN nmapports.txt 10.150.150.12
Nmap scan report for 10.150.150.12
Host is up (0.23s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 2.0.8 or later
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 10.66.67.70
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 2.3.4 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 1fbce3e35bebffb230a74c3311bf67a3 (RSA)
|   256 c8e4182959d04eeadc0550bcd56fe500 (ECDSA)
|_  256 58d5706d0d80710aba8e1c7ac7372fe2 (ED25519)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 4.15 - 5.6 (95%), Linux 5.3 - 5.4 (95%), Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), Linux 2.6.32 (94%), Linux 5.0 - 5.3 (94%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Adtran 424RG FTTH gateway (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 21/tcp)
HOP RTT       ADDRESS
1   303.97 ms 10.66.66.1
2   304.15 ms 10.150.150.12

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu Jan  5 22:17:05 2023 -- 1 IP address (1 host up) scanned in 32.52 seconds
```

After the nmap scan, i did a searchsploit to find any known exploits and we find one for vsftpd 2.3.4 (Backdoor Code Exectution)...
![Screenshot_2023-01-05_22_18_11](https://user-images.githubusercontent.com/99975622/211106865-a4265431-bd01-4814-a5aa-1b5229efe287.png)

#### Methodology...
So how the exploit works, is that , while logging into ftp using any username that ends with a smily face, ":)", and the password also ending with a smily face, a backdoor to the application is opened on port 6200 

<br> So, for our instance, we are going to use the msfconsole exploit...
![Screenshot_2023-01-05_22_19_41](https://user-images.githubusercontent.com/99975622/211107657-57ab91ae-d890-4042-b013-c3ddd44e2383.png)
open metasploit, search for vsftpd 2.3.4 and select the exploit, set the required options and then run the exploit...
<br>And we've gotten our shell!
![Screenshot_2023-01-05_22_20_03](https://user-images.githubusercontent.com/99975622/211107808-6d39e8b3-bd84-44aa-9e21-f84726a3de5c.png)
Look in the current directory and you'll find the flag...
![Screenshot_2023-01-05_22_20_16](https://user-images.githubusercontent.com/99975622/211107916-75813a9f-9793-4a05-8bae-54eb0d3926f6.png)


And Done!
### Socials
@Instagram : https://instagram.com/M3tr1c_r00t
<br>@Twitter : https://twitter.com/M3tr1c_root
