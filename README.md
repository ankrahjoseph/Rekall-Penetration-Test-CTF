# CTF Challenge: Rekall Web Application CTF
**Tools used** : Burpsuite, Kali, Javascript, HTML, PHP

## Scenario 
Rekall Corporation is a fictional company that specializes in offering virtual reality experiences based on images that customers upload.
- These experiences could include dream vacations, adventures, or even secret missions.
- Rekall guarantees that these virtual reality experiences will feel real.
  
Rekall is about to go live with its business, and it needs penetration testers to find any vulnerabilities within its technical systems.
- Rekall has a brand new web application and several Windows and Linux servers that manage its businesses.

I am tasked with using the offensive security skills that I’ve learned over the last couple of weeks to find any vulnerabilities in Rekall’s technical infrastructure and summarize the appropriate mitigations.

## Preparation
After logging into the Kali machine, I navigated to the directory hosting the docker container and started it.
I accessed the application at http://192.168.14.35.

## Flags

**Flag 1** </br>  
I began the process by testing the web application and the first vulnerability I exploited was
cross-site scripting ( XSS ) on the welcome page by inserting <script>alert('XSS');</script> in
the 'Put Your Name Here' field.
  
![Flag 1](https://github.com/ankrahjoseph/Web-Application-CTF/blob/aa4c759d71aab19b6afe7f3a1f47407a13bd057b/Rekall%20Images/f%201.png?raw=true)
  
**Flag 2** </br>  
I injected another script <SCRscriptIPT>alert(“Hello”);</SCRscriptIPT> into the search bar of the browser on the “Memory-Planner” page to generate another pop up on the screen from the VR planner page.

![Flag 2](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%202.png?raw=true)  

**Flag 3** </br>     
I then used the script <dummy<dummy<script>alert('Hello');</dummy</script></dummy> to generate a pop-up on the comments page.

![Flag 3](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%203.png?raw=true)

**Flag 4** </br>  
I then checked the http response header and found sensitive data which contained the fourth flag.

![Flag 4](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%204.png?raw=true)

**Flag 5** </br>  
After that, I went back to the VR Planner page and uploaded a .php payload into the first image upload field which had no validation to the kind of file extension to be uploaded on the website.

![Flag 5](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%205.png?raw=true)

**Flag 6** </br>  
I edited my payload’s extension from .php to .php.jpg to be able to exploit the vulnerability of the second upload field on that page.

![Flag 6](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%206.png?raw=true)

**Flag 7** </br>  
On the login page, I discovered that it was vulnerable to SQL injection so I used the payload “ok’ or 1=1--”

![Flag](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%207.png?raw=true)

**Flag 8** </br>  
The eighth flag was discovered within the HTML source code of the 'Login' page, where the login credentials were exposed.

![Flag 8](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%208.png)

**Flag 9** </br>  
I used directory traversal techniques on the disclaimer page to view the robots.txt file. With this, I determined that the goodbot agent is allowed to access all parts of the web app and found flag 9.

![Flag 9](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%209.png)

**Flag 10** </br>  
When I logged in as administrator, I accessed the networking panel and used command injection in the first field to view the vendors.txt file with ; character www.example.com; cat vendors.txt

![Flag10](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%2010.png)

**Flag 11** </br>
Since the second field was validated to strip ; from working, I used | to inject another command to view the vendors.txt file in that field. www.example.com | cat vendors.txt

![Flag 11](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%2011.png)

**Flag 12** </br>  
I used Burpsuite to brute force the login page of the website with the user “melina” that I found in passwd with command injection. The password was the same as the username and I was able to login into the user login field as melina

![Flag 12 a](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%2012%20a.png)  
![Flag 12](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%2012.png)

**Flag 13** </br>  
I did a php injection by changing the url of the souvenirs page to 192.168.14.35/souvenirs.php?message=CALLUSNOW;system('ls') to view the content of the directory.

![Flag 13](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/f%2013.png)

**Flag 14** </br>  
When I got into the admin legal documents area, access was restricted so I used burpsuite to change the session ID and tested out session IDs from 1-100 until I had access. The session ID that gave me access was admin=87

![Flag 14](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/F14.png)

**Flag 15** </br>  
I used the command injection vulnerability to find the old_disclaimer directory and used the directory traversal exploit to view the disclaimer_1.txt file.

![Flag 15](https://github.com/ankrahjoseph/Web-Application-CTF/blob/main/Rekall%20Images/flag%2015.png)

> **I also tested Rekall's Linux and Windows servers for vulnerabilities**

# CTF Challenge: Rekall Linux Servers CTF
Tools used : Nessus, Kali, Mestasploit, John the ripper, PHP

## Preparation
After logging into the Kali machine, I navigated to the directory hosting the docker container and started it. I accessed Nessus at https://kali:8834/

## Flags

**Flag 1** </br>  
I did a WHOIS search on totalrekall.xyz and found sensitive data about the domain servers and
domain registration and found flag 1

![Flag 1](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Linux%20images/flag%201.png)

**Flag 2** </br>  
I did a ping and NSlookup on totalrekall.xyz and got the ip address of the server which was flag 2.  

**Flag 3** </br>  
I used crt.sh to check their web certificate registration. and found out that, the domain had no valid certificates and found flag 3

![Flag 3](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Linux%20images/flag%203.png)

**Flag 4** </br>  
I did an nmap scan on the IP address and discovered that there were 5 hosts connected to the network for flag 4.

![Flag 4](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Linux%20images/flag%204.png)

**Flag 5 and 6** </br>  
I used a nessus to run an aggressive scan on each of the hosts and found out that 192.168.13.13 was running Drupal and 192.168.13.12 was vulnerable to Apache struts, which were flag 5 and 6.

![Flag 5](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Linux%20images/flag%205.png)  
![Flag 6](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Linux%20images/flag%206.png)

**Flag 7** </br>  
I used Metasploit’s msfconsole to run the (multi/http/tomcat_jsp_upload_bypass) on 192.168.13.10 and opened a shell session. Then I searched the system to find sensitive data and found flag 7.

![Flag 7](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Linux%20images/flag%207.png)

**Flag 8** </br>  
I went back to msfconsole and the exploit exploit/multi/http/apache_mod_cgi_bash_env_exec on 192.168.13.11 and opened a meterpreter session which I used to check the /etc/sudoers file to find sensitive data about the host and found flag 8.

![Flag 8](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Linux%20images/flag%208.png)

**Flag 9** </br>  
I checked the /etc/passwd file to find all the users active on the system and found flag 9.

![Flag 9](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Linux%20images/flag%209.png)

**Flag 10** </br>  
I went back to msfconsole and used the exploit multi/http/struts2_content_type_ognl on 192.168.13.12 which opened a meterpreter session to the host. I searched on the system for sensitive data and found flag 10.

![Flag](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Linux%20images/flag%2010.png)

**Flag 11** </br>  
I tried several drupal exploits on meterpreter and got a session to 192.168.13.13 with the unix/webapp/drupal_restws_unserialize module. I checked the user ID of the session and that was flag 11.

![Flag 11](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Linux%20images/flag%2011.png)

**Flag 12** </br>  
From the WHOIS search, I realized the user alice was the sshuser for the domain; I connected to 192.168.13.14 using SSH with username and password alice:alice. Then I used a CVE-2019-14287 vulnerability to escalate my privileges to root user and found flag 12.

![Flag 12](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Linux%20images/flag%2012.png)

# CTF Challenge: Rekall Windows Servers CTF
Tools used : Nessus, Kali, Mestasploit, John the ripper, PHP

## Preparation
Used the attached Kali VM to conduct this test

## Flags
**Flag 1** </br>  
I also found a github repository of rekall which contained the hash of the password of user trivera and I used John to crack the hash.

![Flag 1a](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%201%20a.png)
![Flag 1b](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%201%20b.png)

**Flag 2** </br>  
I did an nmap scan on the network 172.22.117.0/24 and found that there were two windows hosts connected. The host 172.22.117.20 had the http port open so I went to the browser and went to the page using the IP, it asked for a username and password then I logged in with trivera credential and found flag 2.

![Flag 2a](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%202%20a.png)
![Flag 2b](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%202.PNG)

**Flag 3** </br>  
The port scan also showed that the ftp port was open so I logged into ftp as anonymous and found flag 3, transferred it to my local host and viewed it.

![Flag 3a](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%203%20a.png)
![Flag 3](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%203.png)

**Flag 4** </br>  
From the nmap scan results, SLmail was running on port 25 and on POP3 port 110. I loaded msfconsole and used the windows/pop3/seattlelab_pass to open a meterpreter session,
listed the files in the directory and discovered flag 4.

![Flag 4](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%204.png)

**Flag 5** </br>  
The hint for flag 5 was to check scheduled tasks so I ran schtasks and found a task named flag5. I used the command (schtasks /query /TN flag5 /FO list /v) to view info about the task and found the flag as a comment.

![Flag 5](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%205.png)

**Flag 6** </br>  
Using the same meterpreter session, I loaded kiwi and dumped the user hashes on the system and found flag 6, and ADMBob. I copied their hashes and used John to crack their passwords. Flag 6 was **Computer!**.

![Flag 6-1](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%206%20-1.png)
![Flag 6](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%206.png)

**Flag 7** </br>  
I listed the objects in the directory and moved into the Documents directory. Found flag 7 as a text file.

![Flag 7](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%207.png)

**Flag 8** </br>  
Using the ADMBob credentials I cracked, I used the windows/smb/psexec to move laterally into the Server2019 machine. I connected into a shell and used the net user command to view the users on the system and found flag 8.

![Flag 8](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%208.png)

**Flag 9** </br>  
I went to the root directory and listed the content and found flag 9.

![Flag 9](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%209.png)

**Flag 10** </br>  
I went back to meterpreter and used the command dcsync_ntlm Administrator to view the hash for the Administrator account which was flag 10.

![Flag 10](https://github.com/ankrahjoseph/Rekall-Penetration-Test-CTF/blob/main/Rekall%20Images/Rekall%20Windows%20Images/flag%2010.png)
