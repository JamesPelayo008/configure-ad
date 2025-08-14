<p align="center">
<img width="472" alt="image" src="https://github.com/user-attachments/assets/7228963c-9c73-4709-8c52-1e0e0bff44c1" />
</p>

<h1>DNS Setup in Azure: Connecting a Client PC to a Server</h1>
This tutorial outlines the set up and connection between a DNS server and a client PC  within Azure Virtual Machines.<br />






<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create a resource group and a virtual network
- Set up DNS server VM in Azure 
- Set up Client VM in Azure
- Configure the Client VM to use DNS's Servers private IP
- Test DNS connectivity via Powershell in the Client VM

Note: The resource group and Vnet are labled as "Active Directory" but this project only focuses in DNS and client-pc set up and connectivity.


<h2>Setup Virtual Machines</h2>
 
The first step is to create a resource group in Azure, the names are customizable, in this case it was labeled as "Active Directory", make sure to choose your correct region in the region box below.
<p>
<p>
<img width="1470" alt="image" src="https://github.com/user-attachments/assets/5bfed63e-936d-4fff-864b-5e844429eb04" />

</p>
<p>

</p>
<br />
After you create the resource group you'll create a Virtual network, this Virtual Network will allow our DNS server and client-pc to communicate securely within the same private network. Again make sure to choose your correct region.
</p>
<p>
<img width="1470" alt="image" src="https://github.com/user-attachments/assets/47980140-3262-40d3-af53-1f5e49fa2095" />
</p>
<p> 
 The next step will be to create the first virtual machine, which will serve as the DNS server. The name is customizable, but make sure to select the resource group that was made, and in the image section select Windows Server 2022.
</p>
<br />

<p>
  <img width="1464" alt="image" src="https://github.com/user-attachments/assets/be09457d-90b0-406d-ba72-5eec041fe661" />
</p>
<p>
Next for the size section just select an option that has 2 cpus for better processing. After create a simple username and password, this will be used to log in to our virtual machines via remote desktop.
</p>
<img width="1119" alt="image" src="https://github.com/user-attachments/assets/ea8661a8-bdd5-4f50-a762-7ddb3e10c886" />
</p>
</p>
 Once the username and password are created, make sure to check both boxes in the licesing section at the very bottom, if the option is availabe.
</p>
</p>
<img width="942" alt="image" src="https://github.com/user-attachments/assets/301abb4a-2255-4f9a-b961-3e2d30f91c5f" />
</p>
</p>
Then, make your way to the network tab and ensure that the virtual network box is set to the one that was created earlier. Once you've verified that its the correct virtual network  click review and create.
</p>
</p>
<img width="1118" alt="image" src="https://github.com/user-attachments/assets/0befd5a4-fa44-4451-8e2e-4382ffd76f8b" />
</p>
</p>
Now you'll create the second virtual machine, this virtual machine will serve as our client pc. Follow the same steps listed up above, but this time, make sure to select Windows 10 pro in the image section. 
</p>
<img width="1108" alt="image" src="https://github.com/user-attachments/assets/6d1f6fd5-0946-4b3c-9f43-2420afe87d94" />
</p>
</p>
<img width="1132" alt="image" src="https://github.com/user-attachments/assets/638149cb-3f8f-4de5-9ffe-3756719778ac" />
</p>
</p>
Once your done and have verfied that everything is correct, click review and create.
</p>
</p>
<img width="1127" alt="image" src="https://github.com/user-attachments/assets/214548ab-d830-4a0a-9a77-ab2851b02e5d" />
</p>
</p>

<h2> DNS IP Setup & Client Configuration</h2>
The Virtual Machines are now setup, but before launching them, you need to change the DNS ip address to static. To do that, go to network settings of the DNS VM and click on where it says network Interface / IP configuration.
</p>
</p>
<img width="1458" alt="image" src="https://github.com/user-attachments/assets/01461519-e24c-4ca2-be39-77869fda281c" />
</p>
</p>
Next click "ipconfig1", on the right youll see "Edit IP Configuration" then under "Private IP Address Settings" change the allocation from dynamic to static. Once you've done that click save at the bottom.
</p>
</p>
<img width="1458" alt="image" src="https://github.com/user-attachments/assets/07092549-32f9-44ed-884f-bf5ed83f2f2b" />
</p>
</p>
 You can now launch the DNS server VM. Make your way back to Virtual machines on Azure and Copy the public IP address, make sure its the correct one you labeled for the DNS server.
</p>
<img width="1470" alt="image" src="https://github.com/user-attachments/assets/0dcc59d2-fc88-4ee5-a269-23c0562a7892" />
</p>
</p>
Then paste the IP address when adding a new PC on remote desktop.
</p>
</p>
<img width="1455" alt="image" src="https://github.com/user-attachments/assets/927d18e1-e8b4-4792-88b9-975604ef3914" />
</p>
</p>
Once you open the VM, the first thing that should pop up on the screen is server manager.
</p>
<img width="1459" alt="image" src="https://github.com/user-attachments/assets/2df99c61-23f1-46d0-9fd4-871c7af9c118" />
</p>
</p>
Next right click the windows icon on the bottom left and select "Run" once its open type in "wf.msc".
</p>
</p>
<img width="721" alt="image" src="https://github.com/user-attachments/assets/8763fdf4-06ce-4a0c-82ca-dc4c7b685994" />
</p>
</p>
This will open up "Windows Defender FireWall with Advanced Security", now under where it says "Public Profile is Active" click on "Windows Firewall Properties" and change the fire wall state from on to off on all three profiles Domain, Private, and Public.
</p>
</p>
<img width="1435" alt="image" src="https://github.com/user-attachments/assets/b992db5f-c1f9-4bd2-acbb-5b1715f654d0" />
<img width="1455" alt="image" src="https://github.com/user-attachments/assets/4f4eb947-d8dd-4bbf-9d76-cdf27b1fcb02" />
<img width="1463" alt="image" src="https://github.com/user-attachments/assets/e64ae773-5a8d-40b4-aaa6-1c3dc94614c7" />
</p>
</p>
Once you get to ipsec settings click Apply and Ok to close.
</p>
<img width="1458" alt="image" src="https://github.com/user-attachments/assets/5fac0d39-c363-4c12-bc17-b02c5c69447f" />
</p>
</p>
 Back in Azure copy the private ip address of the DNS server, you'll use this for the DNS settings in the client-pc VM.
</p>
<img width="1461" alt="image" src="https://github.com/user-attachments/assets/22580133-0ae8-443e-81a1-d4f18cf10106" />
</p>
</p>
After the IP address is copied, go to client pc's network settings, and click on the network interface card.
</p>
</p>
<img width="1463" alt="image" src="https://github.com/user-attachments/assets/7fd90a41-4df4-47fa-89ad-4a91b6556bf0" />
</p>
</p>
Then under settings select "DNS servers" and change it to custom. After you've slected custom, paste the DNS server's private ip address in the box below and click save.
</p>
</p>
<img width="1444" alt="image" src="https://github.com/user-attachments/assets/8b3df1e0-6260-4b16-8bb2-6b882ef148e9" />
</p>
</p>
Restart the client VM to ensure all changes fully apply.
</p>
</p>
<img width="1463" alt="image" src="https://github.com/user-attachments/assets/f5dab384-cdaf-4640-aaf1-5797b720e5f6" />
</p>
</p>
Once the VM restarts launch the client VM via remote desktop.
</p>
</p>
<img width="1458" alt="image" src="https://github.com/user-attachments/assets/c9483c2c-f98a-421f-8a96-26f6b6cc7917" />
</p>
</p>

<h2>Client & DNS Server Connectivity Test</h2>
Now you're going to check connectivity of the client pc and the DNS server via powershell. Once you log on into the client VM, in the search bar type powershell to launch it.
</p>
</p>
<img width="1456" alt="image" src="https://github.com/user-attachments/assets/856b71dc-f44a-4c75-810a-e8cd1354dbb2" />
</p>
</p>
Next  type in "ping 10.0.0.4" to test connectivity with the DNS server.
</p>
</p>
<img width="1467" alt="image" src="https://github.com/user-attachments/assets/9b69a4fb-b9b9-4076-8e5e-bc800fce679c" />
</p>
</p>
If the ping is succsesful you'll see replies from the ip address, if not double check in Azure and confirm that the correct private ip address set or check the fire wall properties in the DNS server VM.
</p>
</p>
<img width="1460" alt="image" src="https://github.com/user-attachments/assets/931110c6-0ad8-44eb-8140-aacbfa8d2cfa" />
</p>
</p>
After testing connectivity type "ip config /all" and check that the DNS server output matches the private ip address.
</p>
</p>
<img width="1426" alt="image" src="https://github.com/user-attachments/assets/e6645bfe-02d7-435a-9c8a-8678db32994b" />
</p>
</p>
Once you've confirm that the output is correct, you've sucssessfully connected the client pc to the DNS server. This completes the final step of the tutorial.
</p>
</p>
<img width="1446" alt="image" src="https://github.com/user-attachments/assets/1aee37db-32ac-4664-97c9-3d4193a0c9d2" />
</p>
</p>
Make sure to stop or delete the virtual machines and resource groups once your done to avoid unesessary charges.

This concludes the tutorial, you should now have a clearer understanding of how a client PC connects to a DNS server, which you can confidently apply in the future.
</p>
</p>
<img width="1467" alt="image" src="https://github.com/user-attachments/assets/1a5aad89-7865-4b8e-b776-14e1df991fda" />


