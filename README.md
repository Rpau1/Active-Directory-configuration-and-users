# Active-Directory-configuration-and-users

creating a mini corporate network.


<h2>Description</h2>

creating two virtual machines with VMware.The first one is the windows 2019 domain controller server(DC). Second one is a client VM+ running windows 10 pro. Set up two NIC one internal and one connected to home router. create  Domain, RAS/NAT, DHCP. using a powershell script to auto-create 1k+ user accounts. Making sure the client computer and all authenticated users are properly set up. creating and assigning group policy objective to select user accounts in the domain

Visual description:
![sentinel final map](https://github.com/Rpau1/Azure-Sentinel-SIEM-/assets/147562929/69fcb4a5-9bd1-44b2-bd66-8e357b090860)


<br />


<h2>Languages Used</h2>

- <b>PowerShell: Extract RDP failed logon logs from Windows Event Viewer</b> 


<h2>Utilities Used </h2>

- <b>ipgeolocation.io: IP Address to Geolocation API</b>

<h2> Resources Used </h2>
<b>[YouTube: SIEM Tutorial] (https://youtu.be/RoZeVbbZ0o0?si=YNdqQ7tfGzRDojno)</b>

<b>*usig the sentinel map querry script you can bypass the manual extraction proccess.</b> 
