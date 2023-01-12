# Library!
## @Author : M3tr1c_r00t
Library is an easy box which uses the openmediavault rce exploit using metasploit which gets us a meterpreter shell as root.

### Enumeration...
**__Nmap...__**
```
# Nmap 7.93 scan initiated Tue Jan 10 22:34:05 2023 as: nmap -sC -sV -A -p 80,22 -oN nmapports.txt 10.150.150.111
Nmap scan report for 10.150.150.111
Host is up (0.21s latency).

PORT   STATE    SERVICE VERSION
22/tcp filtered ssh
80/tcp open     http    nginx
|_http-title: openmediavault control panel - library.pwntilldawn.local
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 4.15 - 5.6 (93%), Linux 5.0 (93%), Linux 5.0 - 5.4 (93%), Linux 5.3 - 5.4 (93%), Linux 2.6.32 (93%), Linux 5.0 - 5.3 (92%), Linux 5.4 (91%), ASUS RT-N56U WAP (Linux 3.4) (91%), Linux 3.1 (91%), Linux 3.16 (91%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   204.12 ms 10.66.66.1
2   204.04 ms 10.150.150.111

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Jan 10 22:34:25 2023 -- 1 IP address (1 host up) scanned in 20.24 seconds

```
### Gobuster...
```
/css                 [36m (Status: 301)[0m [Size: 178][34m [--> http://10.150.150.111/css/][0m
/favicon.ico         [32m (Status: 200)[0m [Size: 1406]
/fonts               [36m (Status: 301)[0m [Size: 178][34m [--> http://10.150.150.111/fonts/][0m
/images              [36m (Status: 301)[0m [Size: 178][34m [--> http://10.150.150.111/images/][0m
/index.php           [32m (Status: 200)[0m [Size: 3419]
/js                  [36m (Status: 301)[0m [Size: 178][34m [--> http://10.150.150.111/js/][0m
/licenses            [36m (Status: 301)[0m [Size: 178][34m [--> http://10.150.150.111/licenses/][0m
/rpc                 [36m (Status: 301)[0m [Size: 178][34m [--> http://10.150.150.111/rpc/][0m

```
After visiting the webserver, we find a login page for an openmediavault cms.
We can google the default creds and see if they work.
![Screenshot_2023-01-10_22_31_18](https://user-images.githubusercontent.com/99975622/212146645-f28b40d7-1093-415c-9444-60d339cd9699.png)

After trying the default creds,we are able to log in.
![Screenshot_2023-01-10_22_31_36](https://user-images.githubusercontent.com/99975622/212146687-81413ce2-7ce3-4d6e-84f5-c94e757a74b1.png)

Next up, searching for an exploit, i went to look up the cms version on searchsploit.

We find the exploit and fire up msfconsole.
![Screenshot_2023-01-10_22_39_08](https://user-images.githubusercontent.com/99975622/212146901-0777fc82-def9-44bd-8691-3082911b73ac.png)
Set up the options then run the exploit...
![Screenshot_2023-01-10_22_40_51](https://user-images.githubusercontent.com/99975622/212147064-0c092c46-ac35-4d79-96b9-82f01307df7a.png)
And we've gotten an connection. We are root user so we can go and get our flags....
#### FLAG1.TXT
![Screenshot_2023-01-10_22_43_03](https://user-images.githubusercontent.com/99975622/212147426-e30388c8-dae5-4ea8-ae19-58628562bcdb.png)

### Socials

<br>@ twitter: https://twitter.com/M3tr1c_root
<br>@ instagram: https://instagram.com/m3tr1c_r00t/
