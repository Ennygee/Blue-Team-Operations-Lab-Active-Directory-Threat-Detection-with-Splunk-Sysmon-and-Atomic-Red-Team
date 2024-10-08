# Blue Team Operations Lab: Active Directory Threat Detection with Splunk, Sysmon, and Atomic Red Team

## Objective
This project simulates a real-world Active Directory (AD) environment, focusing on blue team operations. It integrates Splunk for log collection, Sysmon for detailed telemetry, and Atomic Red Team for attack simulations. The lab provides hands-on experience in configuring network security, detecting and responding to attacks, and analyzing telemetry data for comprehensive security operations training.

### Skills Learned
- Configuration and management of Active Directory and Domain Controllers.
- Integration and management of Splunk for log collection and analysis.
- Hands-on experience with Sysmon for telemetry collection.
- Conducting and detecting brute force attacks using Kali Linux.
- Simulating MITRE ATT&CK techniques with Atomic Red Team.
- Practical experience with SIEM systems for monitoring and analyzing cybersecurity events.

### Tools Used
- **VirtualBox**: Virtual machine manager for running the lab environment.
- **Windows Server 2022**: Domain controller for Active Directory.
- **Windows 10**: Target machine for simulated attacks.
- **Kali Linux**: Attack machine for penetration testing.
- **Ubuntu Server**: Running Splunk for log collection and telemetry analysis.
- **Sysmon**: Installed on Windows machines for detailed telemetry.
- **Splunk Universal Forwarder**: For forwarding logs from Windows machines to Splunk.
- **Atomic Red Team**: Simulates real-world cyberattacks to generate telemetry.

## Lab Diagram

This section provides a detailed network diagram that visualizes the lab's structure. The diagram was created using **draw.io** and illustrates the relationships between key components such as the Domain Controller, Target Machine, Attack Machine, and Splunk Server. The network flows and connections are mapped out for easy understanding of the lab architecture.

   ![Screenshot 2024-09-09 204521](https://github.com/user-attachments/assets/c69e0f48-d9e9-4e39-91cd-a5984441850a)

*Explanation*: The diagram helps in visualizing the internal network and its configuration for Active Directory, attack simulation, and log analysis.


## Steps

1. **Virtual Network Setup**  
    - Created a NAT network in VirtualBox with IP range `192.168.10.0/24`.

    *Ref 1: NAT Network Configuration*

    ![Screenshot 2024-09-09 222021](https://github.com/user-attachments/assets/fd86a27e-48c0-406d-968d-91e711b6de5f)

2. **Static IP Configuration for Splunk Server**  
    - Configured a static IP `192.168.10.10` on the Ubuntu Splunk server.

    *Ref 2: Static IP Configuration*

    ![Screenshot 2024-09-09 223531](https://github.com/user-attachments/assets/c14b3fd3-78e2-42cf-a6d6-c2e711b02ec7)

3. **Installing Virtual Machines**  
    - Windows 10 (Target), Kali Linux (Attacker), Windows Server 2022 (AD Domain Controller), and Ubuntu Server (Splunk).

    *Ref 3: VM Setup Overview*

    ![Screenshot 2024-09-09 221101](https://github.com/user-attachments/assets/128c1420-c32f-4462-a668-570b7e71c2e1)

4. **Configuring Static IP on Domain Controller**  
    - Set static IP `192.168.10.7` on Windows Server 2022.

    *Ref 4: Static IP for Domain Controller*

    ![Screenshot 2024-09-09 224631](https://github.com/user-attachments/assets/df20e0e9-1aef-4447-bb41-b22af9d00254)

5. **Installing Active Directory Domain Services (AD DS)**  
    - Installed and configured AD DS on Windows Server 2022.

    *Ref 5: AD DS Installed*

    ![Screenshot 2024-09-16 205514](https://github.com/user-attachments/assets/a30ca733-5a0a-4a7c-8f46-ad5bf3456cee)

6. **Creating Organizational Units (OUs) and Users**  
    - Created OUs in AD and added users like James Bond and Halland Goal.

    *Ref 6: AD OU and User Creation*

    ![Screenshot 2024-09-16 205257](https://github.com/user-attachments/assets/fb235843-fa3d-4496-b395-63e7297c46f7)
   
8. **Joining Windows 10 to the Domain**  
    - Joined Windows 10 to the domain `Ennyspc.local`.

    *Ref 7: Windows 10 in Domain*

    ![Screenshot 2024-09-16 210857](https://github.com/user-attachments/assets/cf49b6d4-dc60-427f-a880-59531494ff6b)

9. **Installing Splunk on Ubuntu Server**  
    - Installed Splunk and configured it to run at boot.

    *Ref 8: Splunk File in Ubuntu server*

    ![Screenshot 2024-09-16 212559](https://github.com/user-attachments/assets/ed1f63ad-dea6-4d9d-a52f-5acf2a786090)

10. **Installing Sysmon and Splunk Forwarder on Windows**  
    - Installed Sysmon and Splunk Universal Forwarder for Windows event logs.

    *Ref 9: Splunk server receiving data from endpoint*

 ![image](https://github.com/user-attachments/assets/0e6099f7-84d1-4920-a939-3007d3ef07d4)

11. **Conducting a Brute Force Attack from Kali Linux**  
    - Used Crowbar to brute force the Windows Target machine via RDP.

    *Ref 10: Brute Force Attack Execution*

![image](https://github.com/user-attachments/assets/8453676b-45c5-415e-bc82-605f38b46717)

12. **Analyzing the Attack in Splunk**  
    - Analyzed login attempts in Splunk (Event ID 4625 and 4624).

    *Ref 11: Log Analysis in Splunk*

    ![image](https://github.com/user-attachments/assets/5d855eb1-dd48-4514-8d17-fd51b9cce1d3)

13. **Installing Atomic Red Team on Windows 10**  
    - Installed Atomic Red Team for attack simulations.

    *Ref 12: Atomic Red Team file on Target PC*

    ![image](https://github.com/user-attachments/assets/48b2856f-ac42-48e6-86f1-58695c92ff6f)
14. **Running Atomic Red Team Tests**  
    - Simulated a user creation attack (`T1136.001`) using Atomic Red Team.

    *Ref 13: Atomic Red Team Test Execution*

  ![image](https://github.com/user-attachments/assets/2f8935b8-d696-4386-8b37-6ab91439a5ab)

### Challenges and Solutions
- **Performance Issues**: Reduced RAM usage on the Domain Controller and Target Machine to 2GB each to avoid system overload.
- **Kali Linux Static IP Configuration**: Encountered issues with static IP, resolved by verifying network connectivity.
- **System Performance**: Hosting 3 out of 4 VMs on my local machine caused performance strain, but adjusting system resources resolved the issue.

*Ref 14: System Performance*

![Screenshot 2024-09-04 051557](https://github.com/user-attachments/assets/11ee63dc-66ee-4aea-a22f-f71c17433890)

### Results
- Successfully detected and mitigated brute force attacks using Splunk for analysis.
- Sysmon captured detailed telemetry logs of failed and successful login attempts.
- Deployed Atomic Red Team to simulate attack scenarios and detected the attacks via Splunk.

*Ref 15: Brute Force Attack Detected in Splunk*

![image](https://github.com/user-attachments/assets/928e8ba9-c731-49e1-85db-90898a1bfcf1)

### Learning Outcomes
- Proficiency in setting up and managing an Active Directory domain.
- Practical skills using SIEM systems like Splunk for event monitoring and analysis.
- Understanding of attack simulations and detection using tools like Crowbar and Atomic Red Team.
- Improved system performance management when running multiple virtual machines.

### Next Steps
- Optimize Splunk dashboards for enhanced attack telemetry visualization.
- Simulate more complex attack scenarios using MITRE ATT&CK techniques.
- Expand the lab by integrating additional security tools such as EDR systems.
- Automate alerts for faster detection of specific attack patterns.
