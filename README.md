# Active-Directory-configuration-and-creating-bulk-users

creating a mini corporate network.


<h2>Description</h2>

creating two virtual machines with VMware.The first one is the windows 2019 domain controller server(DC). Second one is a client VM+ running windows 10 pro. Set up two NIC one internal and one connected to home router. create  Domain, RAS/NAT, DHCP. using a powershell script to auto-create 1k+ user accounts. Making sure the client computer and all authenticated users are properly set up.

Visual description:
![visual](https://github.com/Rpau1/Active-Directory-configuration-and-users/assets/147562929/b67919b3-33a1-4817-a3a9-333e546b3757)



<br />


<h2>Languages Used</h2>

- <b>PowerShell: Used to automate the creation of 1k+ user accounts based on randomly generated names.</b> 

<h2>Project walk-through:</h2>

1) Downloaded VMware;got the extension pack too including the windows
![vmware download](https://github.com/Rpau1/Active-Directory-configuration-and-users/assets/147562929/fc0a2fb9-8767-4a87-bb24-3c011a60594b)

2) Downloaded windows 19 server iso 64bit.[LINK](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)
3) Downloaded windows 10 iso 64bit.[LINK](https://www.microsoft.com/en-us/software-download/windows10)

4) open up vmware click "new" on top, name this vm DC> select the 2019 server iso > select 2-4 cpu at least 2 reccomended> click create
5) right click on the DC vm created>click settings > go to general tab> on clip board settings set both to bidirectional> go network tab> adapter 1 we are gonna select NAT(this is gonna be the external internet)>Adapter 2 select internal Network(this is for the client vm and users). Now we have both of the NIC set up.
6) Turn on your VM(this might take a while)
7) While its turning on select standard OS, custom install and, default hard drive if any of these questions appear.
8) Give the built in administrator account password of "Password1" we are going to use this password for every password in this lab just for the ease of use.
9) Click on devices on top of the DC vm click on "insert guest addition cd image" go to folder within the vm click this pc than next to the C drive you will see the virtua; box gues edition click that run the amd64> keep clicking next till the last tab. on the last tab click reboot now. let the vm restart. Log in to the new vm as administrator. [this step makes the vm run more smoothly]
10) setting up IP: Click the network diagram bottom right in the vm>click network> click network adapter options>change ethernet name to _INTERNET_(this is the extarnal adapter conncted to the internet with home router> rename Ethernet2 to INTERNAL if you click on it and chose status it will show you the vm ip and empty gateway adress> right click on it again> go to properties> select ipv4 click next and type in this ips shown in this picture below for internal>click ok.
    ![assigning ip to internal](https://github.com/Rpau1/Rpau1/assets/147562929/572f6179-caf7-4e88-bd1f-2b648a757c28)
(see how the DNS server adress is a loop back adress that's so this server uses itself for DNS) 

12) rename pc: right click on windows chose rename and name it DC>click next>it will reboot> log in. 
   


<h2> Resources Used </h2>
<b>[YouTube: Active directory Lab Tutorial] (https://youtu.be/MHsI8hJmggI?si=9e6oHqkikdU-4uT0)</b>

<b></b> 
