# Active-Directory-configuration-and-creating-bulk-users

creating a mini corporate network.


<h2>Description</h2>

-creating two virtual machines with VMware.
-The first one is the windows 2019 domain controller server(DC). Second one is a Client VM running windows 10 pro/enterprise.
-Set up two NIC one internal and one connected to home router(internet).
- In domain controller(Win 2019 server) create and configure Domain, RAS/NAT, DHCP.
- using a powershell script to auto-create 1k+ user accounts. 
-Making sure the client computer is configured and connected properly and  also, making sure authenticated users are properly set up to use it.

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
13) installing Active directory domain services:go to server manager in the vm> click on add roles and features>click next till server roles> there click the box on "Active directory domain services"> keep clicking next than click install>click on the flag top right of server manager app>click on promote domain properties>than name the domain mydomain.com> and for deployment option select domain forest>click next> use Password1 for password>kepp preesing next till you go to install>click install. the computer will automaticaly restart let it restart than log in again as same admin user.
     ![AD domain config](https://github.com/Rpau1/Rpau1/assets/147562929/026e8a47-0097-4830-8c98-8e1f8afa4be8)


14) creating dedicated admin account instead of built in admin:click on windows>click "windows administritive tools"> click "active directory users and computers">right click on mydomain.com> click new> orgonizational unit> name it ADMINS> right click that folder and select new user> name it your full name > for user name get the first initial of your first name than your last name>click next>click finish>right click on the new user created> go to properties>than to member of>click add> type "domain admins">click check name> click ok>apply>ok.
15) sign out of the vm and log in as the new administrator account(it will show mydomain under password whili logging in)
16) installing RAS/NAT: go to server manager> add roles and features>click nest till you get to server roles>check Remote access>click next> check routing>keep clicking next till you get to install> click install. now go on tools top right hand of server manager>go to routing and remote access> right click on DC control>click on configure and enable> click next> click NAT> click next> it will give a option to chose between internet and internal> chose internet> click next>click finish> now its configured and DCcontrol will have a green dot next to it.
17) setting up DHCP servers: go too add roles and features>go to server roles>check on DHCP servers>keep clickin on next and than instal
18) set up DHCP scope: go to tools>click DHCP>right click on ipv4> click new sope> name the scope after ip range so "172.16.0.100-200">fill up the information according to the picture below>click next> set lease IP to 8 days> click next>click "yes" for client configuration> enter the domain controlers ip adress172.16.0.1>click add> click next>next again> click finish> right click on the DHCP server and refresh.
    ![setting scope for dhcp](https://github.com/Rpau1/Rpau1/assets/147562929/06b6a6fd-e1cc-4546-93ab-348b4cbe52bc)

19) using powershell script to create bulk users: go to explorer in vm> come to this repisotory in github>Download AD_PS-master.zip. within that folder you will see the "create_users.ps1" powershell script and names.text has random names from name generator. the script will use those name while creating user accounts.>in names.txt add your own full name and save it> go to windows>right click on powershell and run as administrator>open the powershell script from the folder>click run,you will most likely see an execution policy error> so type in this command "Set-ExecutinPolicy unrestricted"> click yes to all in the pop up> go to the directory where you stored the script for me it's c:\users\r-paul\desktop\AD_PS-master.zip> now click run> click run on the pop up too> it will start creating users.
    ![running script to create users](https://github.com/Rpau1/Rpau1/assets/147562929/9502da61-0b5b-493a-97e4-417edb28994e)


20) now go to active directory users and computers> expand the domain> click on users> you will see all the users created if not right click on domain and refres you can also right click on the users and click "find" to find your own user account with your name.
    ![new users created in the AD](https://github.com/Rpau1/Rpau1/assets/147562929/ab761835-7cc8-4265-a168-726fb07c1cd8)


21) crreating windows10 client vm: set up just like the DC vm with same configuration but chose the windows 10 pro/enterprise 64bit get a trial KEY from microsoft if needed. On network setting we only need one network adaptor and make sure it's set to inernal. name the vm client1 or client2. start and open the vm.

22) on comman prompt in the client vm run "ipconfig" you will see the gateway ip is empty.
    ![checking network connection on clientvm](https://github.com/Rpau1/Rpau1/assets/147562929/41b325f1-2cf5-471c-8f13-f14d4da540f9)

23) go back to DCvm go on DHCP on server manager>go to ipv4> righ click and chose server option> chose router> add the domain controlers(DC) ip adress "172.16.0.1">click add >apply>ok>right click the server and restart it.
24) go back to client vm command prompt and run "ipconfig /renew" and we will see it is connected to host server. if you run"ipconfig" again you will see the deafult gateway.
    ![now we have gatewayip on client](https://github.com/Rpau1/Rpau1/assets/147562929/4e1eefca-01fe-400f-b98b-dcb2c2639446)

25) if you ping mydomain.com you will see it connects.
26) now we are going to rename the pc and join the domain: right click on start>systems>rename this pc(advanced)>click change> name client1 or client 2>click on domain and type in mydomain.com>click ok> type your user account name and password made on your name for me it's "rpaul" "Password1">ok>ok>restart

27) if we go back to DGCP on domain controler server(DC) vm we can see the client connection running on DHCP server.
    ![see the client connection running on server DHCP](https://github.com/Rpau1/Rpau1/assets/147562929/d099c0c4-7cac-42f0-acf3-63ac2acdaa34)


28) if we go to active directory client and computers and go to computers folder we see the newly created client computer as member of the domain.
    ![Computer created for client2 showing in DC AD](https://github.com/Rpau1/Rpau1/assets/147562929/29267a5a-3eba-4329-a2d5-d16e291b8e9d)
29) using one of the user account creted to log into domain and connect.
       ![loggin into that computer as one of the users created by the ps script](https://github.com/Rpau1/Rpau1/assets/147562929/19f4575c-a203-4c40-9ce9-614bd872ba08)



DONE. 




    
   

    
   

   


<h2> Resources Used </h2>
<b>[YouTube: Active directory Lab Tutorial] (https://youtu.be/MHsI8hJmggI?si=9e6oHqkikdU-4uT0)</b>

<b></b> 
