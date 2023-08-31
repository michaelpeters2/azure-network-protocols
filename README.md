<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Sample File Shares With Various Permissions
- Attempt to Access File Shares as a Normal User
- Create an “ACCOUNTANTS” Security Group, Assign Permissions, and Test Access
- Step 4

<h2>Actions and Observations</h2>

Create Sample File Shares With Various Permissions
-
1) Log into Domain Controller (DC-1) as your domain admin account ((mydomain.com\jane_admin)
2) Log into Client-1 as a normal user (mydomain\<someuser>) (Password1)
3) On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
<p>
  
![image](https://github.com/michaelpeters2/azure-network-protocols/assets/141062110/19169ee3-e138-4be2-b280-5f0e773bdb3f)

</p>
<p>
4) Set the following permissions (share the folder) for the “Domain Users” group:
  
5) Folder: “read-access”, Group: “Domain Users”, Permission: “Read”

7) Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”

8) Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”

(Skip accounting for now)

Attempt to Access File Shares as a Normal User
-
9) On Client-1, navigate to the shared folder (start, run, \\dc-1)
10) Try to access the folders you just created. Which folders can you access? Which folders can you create stuff in? Does it make sense?
<p>
  
![image](https://github.com/michaelpeters2/azure-network-protocols/assets/141062110/355c89e4-cb02-4d02-9731-178ee00ccd4e)

</p>
<p>
  
Create an “ACCOUNTANTS” Security Group, Assign Permissions, and Test Access
-
11) Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”
12) On the “accounting” folder you created earlier, set the following permissions:
13) Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”

![image](https://github.com/michaelpeters2/azure-network-protocols/assets/141062110/3aed3dbc-aeb1-4979-b00f-5c6757c08a53)

</p>
<p>
14) On Client-1, as  <someuser>, try to access the accountants folder. It should fail.

15) Log out of Client-1 as  <someuser>

16) On DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group

17) Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1\ - Does it work now?

It should! You now seem to have an idea of the basics of Network File Shares and Permissions!
