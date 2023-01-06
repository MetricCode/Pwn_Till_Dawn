# PwnDriveAcademy!
## @Author : M3tr1c_r00t
![Screenshot_2023-01-05_22_34_49 (2)](https://user-images.githubusercontent.com/99975622/211108890-990fc090-0748-40ac-9cea-fc4e063c1301.png)
PwnDrive is a Easy Windows Machine that is vulnerable to the Eternal Blue Exploit.

### Enumeration...
```
# Nmap 7.93 scan initiated Thu Jan  5 22:28:08 2023 as: nmap -sC -sV -A -p 21,80,135,139,445,443,1433,3306,3389,47001,49152,49153,49155,49154,49156,49157,49192 -oN nmapports.txt 10.150.150.11
Nmap scan report for 10.150.150.11
Host is up (0.21s latency).

PORT      STATE SERVICE        VERSION
21/tcp    open  ftp            Xlight ftpd 3.9
80/tcp    open  http           Apache httpd 2.4.46 ((Win64) OpenSSL/1.1.1g PHP/7.4.9)
|_http-title: PwnDrive - Your Personal Online Storage
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1g PHP/7.4.9
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
135/tcp   open  msrpc          Microsoft Windows RPC
139/tcp   open  netbios-ssn    Microsoft Windows netbios-ssn
443/tcp   open  ssl/http       Apache httpd 2.4.46 ((Win64) OpenSSL/1.1.1g PHP/7.4.9)
| tls-alpn: 
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
|_http-title: PwnDrive - Your Personal Online Storage
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2009-11-10T23:48:47
|_Not valid after:  2019-11-08T23:48:47
|_http-server-header: Apache/2.4.46 (Win64) OpenSSL/1.1.1g PHP/7.4.9
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
445/tcp   open  microsoft-ds   Windows Server 2008 R2 Enterprise 7601 Service Pack 1 microsoft-ds
1433/tcp  open  ms-sql-s       Microsoft SQL Server 2012 11.00.2100.00; RTM
|_ms-sql-ntlm-info: ERROR: Script execution failed (use -d to debug)
|_ms-sql-info: ERROR: Script execution failed (use -d to debug)
|_ssl-date: 2023-01-05T23:10:09+00:00; +40m08s from scanner time.
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2020-08-24T13:11:13
|_Not valid after:  2050-08-24T13:11:13
3306/tcp  open  mysql          MySQL 5.5.5-10.4.14-MariaDB
| mysql-info: 
|   Protocol: 10
|   Version: 5.5.5-10.4.14-MariaDB
|   Thread ID: 1071
|   Capabilities flags: 63486
|   Some Capabilities: FoundRows, InteractiveClient, Speaks41ProtocolOld, Speaks41ProtocolNew, Support41Auth, SupportsTransactions, DontAllowDatabaseTableColumn, SupportsCompression, ConnectWithDatabase, LongColumnFlag, SupportsLoadDataLocal, ODBCClient, IgnoreSigpipes, IgnoreSpaceBeforeParenthesis, SupportsMultipleResults, SupportsMultipleStatments, SupportsAuthPlugins
|   Status: Autocommit
|   Salt: L9xqNpjDU^X":>iv7M\e
|_  Auth Plugin Name: mysql_native_password
3389/tcp  open  ms-wbt-server?
| rdp-ntlm-info: 
|   Target_Name: PWNDRIVE
|   NetBIOS_Domain_Name: PWNDRIVE
|   NetBIOS_Computer_Name: PWNDRIVE
|   DNS_Domain_Name: PwnDrive
|   DNS_Computer_Name: PwnDrive
|   Product_Version: 6.1.7601
|_  System_Time: 2023-01-05T23:09:55+00:00
| ssl-cert: Subject: commonName=PwnDrive
| Not valid before: 2023-01-04T22:40:26
|_Not valid after:  2023-07-06T22:40:26
|_ssl-date: 2023-01-05T23:10:07+00:00; +40m08s from scanner time.
47001/tcp open  http           Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49152/tcp open  msrpc          Microsoft Windows RPC
49153/tcp open  msrpc          Microsoft Windows RPC
49154/tcp open  msrpc          Microsoft Windows RPC
49155/tcp open  msrpc          Microsoft Windows RPC
49156/tcp open  msrpc          Microsoft Windows RPC
49157/tcp open  msrpc          Microsoft Windows RPC
49192/tcp open  ms-sql-s       Microsoft SQL Server 2012 11.00.2100.00; RTM
|_ms-sql-ntlm-info: ERROR: Script execution failed (use -d to debug)
|_ms-sql-info: ERROR: Script execution failed (use -d to debug)
|_ssl-date: 2023-01-05T23:10:09+00:00; +40m08s from scanner time.
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2020-08-24T13:11:13
|_Not valid after:  2050-08-24T13:11:13
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Microsoft Windows 7 or Windows Server 2008 R2 (97%), Microsoft Windows Server 2008 R2 SP1 (96%), Microsoft Windows Server 2008 SP1 (96%), Microsoft Windows Server 2008 SP2 (96%), Microsoft Windows 7 (96%), Microsoft Windows 7 SP0 - SP1, Windows Server 2008 SP1, Windows Server 2008 R2, Windows 8, or Windows 8.1 Update 1 (96%), Microsoft Windows 7 SP1 (96%), Microsoft Windows Vista or Windows 7 SP1 (96%), Microsoft Windows Vista SP1 - SP2, Windows Server 2008 SP2, or Windows 7 (96%), Microsoft Windows Vista SP2, Windows 7, or Windows 7 SP1 (96%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows Server 2008 R2 Enterprise 7601 Service Pack 1 (Windows Server 2008 R2 Enterprise 6.1)
|   OS CPE: cpe:/o:microsoft:windows_server_2008::sp1
|   Computer name: PwnDrive
|   NetBIOS computer name: PWNDRIVE\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2023-01-05T15:09:57-08:00
| smb2-time: 
|   date: 2023-01-05T23:09:55
|_  start_date: 2020-08-24T13:11:20
|_nbstat: NetBIOS name: PWNDRIVE, NetBIOS user: <unknown>, NetBIOS MAC: 000c298987cb (VMware)
| smb2-security-mode: 
|   210: 
|_    Message signing enabled but not required
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: mean: 1h48m42s, deviation: 3h01m26s, median: 40m07s

TRACEROUTE (using port 21/tcp)
HOP RTT       ADDRESS
1   237.81 ms 10.66.66.1
2   237.92 ms 10.150.150.11

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu Jan  5 22:30:05 2023 -- 1 IP address (1 host up) scanned in 117.34 seconds
```

### Methodology ...
Eternalblue itself concerns CVE-2017-0144, a flaw that allows remote attackers to execute arbitrary code on a target system by sending specially crafted messages to the SMBv1 server.

I immediately went for the eternal blue exploit after realizing that the smb server was version 1 from the nmap scan...
<br> So fire up msfconsole, search for ms17 and select the eternal blue exploit ...
![Screenshot_2023-01-05_22_32_02](https://user-images.githubusercontent.com/99975622/211111383-33188d0f-71c8-44ff-b808-a3ecbde240e0.png)

Next up, set up the options then run the exploit...
![Screenshot_2023-01-05_22_32_51](https://user-images.githubusercontent.com/99975622/211111425-e8eaa53f-052d-4e1e-9671-5da6dea6c650.png)
And we can see it is vulnerable...
We get a meterpreter shell, get the windows shell by typing shell...

![Screenshot_2023-01-05_22_33_31](https://user-images.githubusercontent.com/99975622/211111508-b98433a2-4f54-42ef-8514-b60acb9c11f6.png)
Then navigate to the administrator's desktop directory to get your flag...
![Screenshot_2023-01-05_22_34_15](https://user-images.githubusercontent.com/99975622/211111564-ff4d9270-c043-4b23-8226-1e81e7cba444.png)

And Done!
### Socials
@Instagram : https://instagram.com/M3tr1c_r00t
<br>@Twitter : https://twitter.com/M3tr1c_root
