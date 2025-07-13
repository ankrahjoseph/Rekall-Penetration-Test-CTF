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

! [Flag 1] (https://github.com/ankrahjoseph/Web-Application-CTF/blob/aa4c759d71aab19b6afe7f3a1f47407a13bd057b/Rekall%20Images/f%201.png?raw=true)

**I also tested Rekall's Linux and Windows servers for vulnerabilities**

# Linux Servers CTF
Tools used : Nessus, Kali, Mestasploit, John the ripper, PHP

I also tested Rekall's Linux servers for vulnerabilities

**Preparation** :
After logging into the Kali machine, I navigated to the directory hosting the docker container and started it.
I accessed Nessus at https://kali:8834/

# Windows Servers CTF
Tools used : Nessus, Kali, Mestasploit, John the ripper, PHP

**Preparation** :
Used the attached Kali VM to conduct this test
