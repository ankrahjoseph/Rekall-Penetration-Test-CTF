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

# Linux Servers CTF
Tools used : Nessus, Kali, Mestasploit, John the ripper, PHP

I also tested Rekall's Linux servers for vulnerabilities

## Preparation
After logging into the Kali machine, I navigated to the directory hosting the docker container and started it.
I accessed Nessus at https://kali:8834/

## Flags

**Flag 1** </br>  
I did a WHOIS search on totalrekall.xyz and found sensitive data about the domain servers and
domain registration and found flag 1



# Windows Servers CTF
Tools used : Nessus, Kali, Mestasploit, John the ripper, PHP

**Preparation** :
Used the attached Kali VM to conduct this test
