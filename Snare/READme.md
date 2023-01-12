# Snare!
## @Author : M3tr1c_r00t
![Screenshot_2023-01-10_22_17_38](https://user-images.githubusercontent.com/99975622/212154708-2487e596-85df-4d71-8ee3-0fe3da86de17.png)
### Enumeration...
_**Nmap...**_
```
# Nmap 7.93 scan initiated Tue Jan 10 21:14:51 2023 as: nmap -sC -sV -A -p 22,80 -oN nmapports.txt 10.150.150.18
Nmap scan report for 10.150.150.18
Host is up (0.20s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 2f0e73d4ae73147ec51c1584ef45a4d1 (RSA)
|   256 390b0bc986c98eb52b0c39c763ece210 (ECDSA)
|_  256 f6bfc5035bdfe5e1f4daac1eb207882f (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
| http-title: Welcome to my homepage!
|_Requested resource was /index.php?page=home
|_http-server-header: Apache/2.4.41 (Ubuntu)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 4.15 - 5.6 (95%), Linux 5.3 - 5.4 (95%), Linux 3.1 (94%), Linux 3.2 (94%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), Linux 2.6.32 (94%), Linux 5.0 - 5.3 (93%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Adtran 424RG FTTH gateway (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 443/tcp)
HOP RTT       ADDRESS
1   203.04 ms 10.66.66.1
2   203.01 ms 10.150.150.18

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Jan 10 21:15:10 2023 -- 1 IP address (1 host up) scanned in 19.84 seconds

```

_**Gobusterscan...**_
```
/.hta                [33m (Status: 403)[0m [Size: 278]
/.htaccess           [33m (Status: 403)[0m [Size: 278]
/.htpasswd           [33m (Status: 403)[0m [Size: 278]
/includes            [36m (Status: 301)[0m [Size: 317][34m [--> http://10.150.150.18/includes/][0m
/index.php           [36m (Status: 302)[0m [Size: 953][34m [--> /index.php?page=home][0m
/server-status       [33m (Status: 403)[0m [Size: 278]

```

On visiting the login page, i note there's an lfi exploitable parameter which we could try to exploit...
After a bit of testing, we can run a RFI on the server...
![Screenshot_2023-01-10_21_45_38](https://user-images.githubusercontent.com/99975622/212152233-65541abe-2bb9-4309-8309-bbf4342910e9.png)
After confirming this, we can make a php reverse script to send a connection to our system...
![Screenshot_2023-01-10_21_55_10](https://user-images.githubusercontent.com/99975622/212152423-90ad08e6-59ea-49bf-9a09-ad1433fc6051.png)
After saving the file, set up your python web server, set up a listerner then call on the file...

<br>While calling on the file, do not add a .php extension as there is an extension fixed on the file...
![Screenshot_2023-01-10_21_55_18](https://user-images.githubusercontent.com/99975622/212152824-a428794b-28f9-4e5b-921e-a034505b76c6.png)

### FLAG1
![Screenshot_2023-01-10_21_57_05](https://user-images.githubusercontent.com/99975622/212152955-5322d428-7f37-4d04-b99c-554f29fffd4f.png)

After running linpeas, we note that we can view and edit /etc/shadow file...
![Screenshot_2023-01-10_22_05_27](https://user-images.githubusercontent.com/99975622/212153095-71f1e9ac-33d7-4f84-8301-29a2d239b565.png)

Since i was using kali linux live boot, i viewed my own /etc/shadow file, copied the password hash to the kali user then pasted it to the machines snare user.

![Screenshot_2023-01-10_22_16_39](https://user-images.githubusercontent.com/99975622/212153438-1f9701bf-e197-493c-b3ce-0c649402540d.png)
Next, i moved to the snare user's account and since he could run any command as sudo, 
![Screenshot_2023-01-10_22_16_54](https://user-images.githubusercontent.com/99975622/212154009-76b901d8-0c17-4d2a-ab65-bb569747e419.png)
we can move into the root users command without a prompt for a password.
![Screenshot_2023-01-10_22_17_06](https://user-images.githubusercontent.com/99975622/212154060-4a9729a6-435b-4f9d-9f75-31b1355fd5ab.png)

###  FLAG2
![Screenshot_2023-01-10_22_17_14](https://user-images.githubusercontent.com/99975622/212154244-00a77139-50d8-4189-9a12-d9f785172d41.png)

And done!


## My socials:
<br>@ twitter: https://twitter.com/M3tr1c_root
<br>@ instagram: https://instagram.com/m3tr1c_r00t/
