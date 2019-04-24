# ADS-Config
Config for ADS

## Task
Your task is to design and implement technical security defenses, to achieve the required functionality as specified below in this requirements specification, and you will describe your approach in a technical report (which is described in the module handbook).
You need to make your actual system configuration changes to the VMs provided.
The systems you are provided includes insecure settings and/or software.
Your report's contents should follow the structure of the below headings (plus Executive Summary, Limitations, Conclusion, and References sections) to describe the changes you make, including describing any insecure settings or software you find and fix in the systems you have been provided. Describe every change that was necessary, with screenshots showing the changes and demonstrating with a testing plan whether the security functions as intended.

## Users

````
username: user1
password: 9AYY8981
Metadata: room number 1
Phone extension: 2342
group: admin
username: user2
password: RTCFE3Z0
Metadata: room number 2
Phone extension: 2343
group: staff
username: user3
password: 5Y9HD8GD
Metadata: room number 3
Phone extension: 2344 
group: staff
username: user4
password: XTPPSQUN
Metadata: room number 3
Phone extension: 2345
group: staff,developer
username: user5
password: OGJL1CX7
Metadata: room number 4
Phone extension: 2346
group: staff,developer
````

## Auth
You need to use authentication schemes of your choice to enable these Users to log into systems and services. Justify your approach and describe how well it achieves the security requirements documented below.
In your report describe what it would take for a new user to be added, or for a user to change their password. Describe the effect of network eavesdropping on the authentication.
SSH settings: Disable SSH access for user1, user2, user3, user4, and user5, on the server and desktop VMs. This change is important to make as soon as you add these users to your VMs. Leave the SSH access settings otherwise unchanged; for example, your main user should be able to SSH to these VMs. (When marking your work we may SSH to your VMs).

## Systems
You are provided with VMs, which you are required to configure, and leave in a state for review, with persistent settings that survive reboot.
To install software: For temporary access to the Internet, run sudo dhclient ens3 so you can install additional software via apt-get as required (if you want to access the Internet for anything other than apt-get you may need to configure the proxy to 172.22.0.51:3128). Then run sudo service networking restart to reset your IP address, which will restore network connectivity between your other VMs.

## Servers

**Web server**

The server VM needs to be running an Apache web server, hosting a website.

**FTP server**

An FTP server needs to be running, accepting connections from any of the Users, with their credentials. Users should have their own directory for saving backups, which should not be available to other users. A shared directory should be available (read and write) to all authenticated users. A "code" directory should only be available to users in the "developers" group.

**SMB server**
A centralised Windows file share (Samba) should be hosted on this VM and available to all Users with their credentials.

## Security controls
The server system should be locked down, in a way that limits the potential damage caused by a vulnerability in the file sharing services or the web server (Hint: consider sandboxing, containerisation, and/or MAC restrictions). In your report make it clear how much protection there is against malicious users, or software vulnerabilities.
All network services should be configured to provide secure communication. In your report describe the information an eavesdropper could capture from the network.
Use network-based authentication to enable Users to access the services using their credentials. Only the Admin user (user1 above, a member of the admin group) should be able to log directly into the server via SSH or login. In your report describe what it would take for a new user to be granted access, or for a user to change their password.

## developer_desktop
### Authentication
The developer_desktop system should be available for anyone in the developer or admin group to login. They should have superuser/sudo access. Use network-based authentication.
### Functionality
The developers need to be able to compile C code, and access the network shares.
I###dentified security problems
In your report describe any insecure settings and/or software you found and document how you made the system secure.

## staff_desktop
### Authentication
This staff_desktop system should be available for any valid User to login. They should not have superuser access. Only users in the admin group should have superuser access. Use network-based authentication.
### Access controls
New files created by users should not be automatically shared with other users on the system. There should be a shared directory "/srv/shared" for users to share files locally (read, write).
### Directory service
Users should have some way to query phone numbers and room numbers of any Users. Users should also be able to use Firefox to access the website on the server; and have access to the FTP and Samba server via Dolphin.
### Security controls
Lock down the system to limit damage that could be caused by vulnerabilities. In your report make it clear how much protection there is against malicious users, or software vulnerabilities.
### Identified security problems
In your report describe any insecure settings and/or software you found and document how you made the system secure.


## auth_server
This server is intended to be used to host network-authentication, such as LDAP, Kerberos, and/or Active Directory (such as via Samba DC). 

