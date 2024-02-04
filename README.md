<h1>JWipe - Disk Sanitization</h1>

 ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo)

<h2>Description</h2>
In Cybersecurity, it could be a daunting task to apply and implement security concepts if there is an unavailability of practical and safe infrastructure to carry out these activities.
I approached this project with that in mind. This homelab walks through the process of configuring, optimizing, and securing an I.T infrastructure. Although this will be at a relatively small scale, you will be able to apply the knowledge gained in a real-world large-scale/enterprise infrastructure.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Configuring pfSense firewall for Network Segmentation & Security
- Configuring Security Onion as an all-in-one IDS, Security Monitoring, and Log Management solution
- Configuring Kali Linux as an attack machine
- Configuring a Windows Server as a Domain Controller
- Configuring Windows desktops
- Configuring Splunk
- Ubuntu/CentOS/Metasploitable/DVWA/Vulnhub machines: All these are potential Linux machines that can be added to the network for exploitation, detection, or monitoring purposes.

<h2>Program walk-through:</h2>

<p align="center">
  HOMELAB NETWORK DESIGN & TOPOLOGY: <br/>
<img src="https://i.imgur.com/JyNqqh5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <p align="center">
Configuring pfsense
    <br />
  pfsense will be configured as a firewall to segment our private homelab network and will be only accessible from our Kali Linux machine.
    <br />
    <br/>
    Click “Create a New Virtual Machine” on VMware Workstation Homescreen.
    Make sure “Typical (recommended)” is selected and click Next:  <br/>
  <br />
  <br />
<img src="https://i.imgur.com/OZ0cnog.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
20GB disk size is sufficient for this VM.<br/>
Ensure that the “Split virtual disk into multiple files” option is selected.<br/>
Click Next. <br/>
Increase the memory to 2GB. <br/>
Add 5 network adapters and correspond them with a VMnet interface as shown below. Then click Finish: <br/>
<img src="https://i.imgur.com/Xg6FGau.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter assign interfaces  <br/>
Should VLANS be set up now [y:n]?: n  <br/>
Enter em0, em1, em2, em3, em4 & em5 respectively for each consecutive question  <br/>
Do you want to proceed [y:n]?: y:  <br/>
Enter option 2 <br/>
We’ll start with the LAN interface (2) <br/>
The ip address 192.168.1.1 is going to be used to access the pfsense WebGUI via the Kali Machine <br/>
Use the configuration below for the Lan interface <br/>
<img src="https://i.imgur.com/SbhKD7c.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Use the configuration below for the OPT2 interface <br />
Leave the OPT3 interface without an IP as it is going to have the span port with traffic that Security Onion will be monitoring. <br />
Use the configuration for the OPT4 interface <br/>
<img src="https://i.imgur.com/RCZTVhz.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<br />
<br />
pfsense Interfaces and Rules <br />
The pfsense VM configuration concludes, and from this point forward, the remaining setup will be handled through the Kali machine using the WebConfigurator.   
<p align="center">
<br />
<br />
You’ll be greeted with a “Wizard/pfSense Setup/” page.<br />
Click Next till you get to Step 2 of 9.<br />
Add 8.8.8.8 as your Primary DNS Server<br />
Add 4.4.4.4 as your Secondary DNS Server<br />

Click Next.  <br/>
<p align="center">

<img src="https://i.imgur.com/mqsG5ii.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 At Step 3 of 9, Choose your Timezone

Click Next.

At Step 4 of 9, untick the last two options

At Step 5 of 9, Click Next <br/>
<p align="center">
<img src="https://i.imgur.com/vIUq6fg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Click on Interfaces.

Select LAN

For “Description“, Change LAN to est of the Interfaces as shown below as this is the Kali interface

Scroll all the way down and Click Save  <br/>
<p align="center">
<img src="https://i.imgur.com/WbWzkk6.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<br />
<br />
For OPT3 Be sure to Enable Interface as shown below  <br/>
 <br /> 
<img src="https://i.imgur.com/0PuZYqW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

  Back at Interfaces Assignment select Bridges

Click Add

Select VictimNetwork as the Member Interface


Then select Display Advanced

Under Advanced Configuration for Span Port, select “SPANPORT”

Scroll all the way down and Click Save<br/>
<p align="center">
<img src="https://i.imgur.com/2myWpCX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Configuring Security Onion <br/>
 Transitioning to Security Onion, I download the ISO file and initiate the installation process by opting for the "Typical installation." Hardware customization involves adjusting memory and network adapter settings. As the installation proceeds, I configure various settings such as hostname, IP addressing, and other preferences.  <br/>
  <br />
<img src="https://i.imgur.com/iWOskc8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  After installing Security Onion, having access to the web interface will be done from an external Ubuntu Desktop simulating a SOC/Security Analyst accessing a SIEM or any other tool from their device.

In order to this, you’ll first have to configure an Ubuntu Desktop.<br/>
<p align="center">
<img src="https://i.imgur.com/aUouufM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Configuring Windows Server as a Domain Controller  
  After the installation

Rename the Domain Controller

~ Navigate to Settings in the search bar

~ Search for settings in the search bar

~ Search for “pc name” in the settings search

~ Select Rename PC and rename the PC your choice name

~ Select Restart Now  <br/>
After the reboot, on the Server Manager Dashboard, Click Manage >> Add Roles and Features. <br/>
<p align="center">
<img src="https://i.imgur.com/6Zs19xj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<img src="https://i.imgur.com/cA5FTgD.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/pjlpO0K.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
  Select the disk:  <br/>
<img src="https://i.imgur.com/2s9Dprj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/3w35jWI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/QUnVdlO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/lvdw09e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/0lP70BM.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/ZApXDoG.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
  Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/ptqdSq9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/1bCJB8o.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/RwwSrdE.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
  Select the disk:  <br/>
<img src="https://i.imgur.com/SpmEHgx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/acP0Ifj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/I6sG1Sg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/tEolB8u.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/IUWLKbx.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/WTQSSrr.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/RCQvIVW.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
  Select the disk:  <br/>
<img src="https://i.imgur.com/NeFGZVy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/3CWvqC2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>

</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
