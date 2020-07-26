## Objective

In this Lab I created a network of virtual machines (VMs) using the virtualisation software Oracle VM Virtualware. The purpose of the Lab was to develop practical knowledge of the Windows Server operating system and the Active Directory service.

### Contents

[Initial Setup](#initial-setup)

[DHCP](#dhcp)

[Users and Groups](#users-and-groups)

[Group Policy Objects (GPOs)](#gpos)

### Initial Setup

* Created 2 VMs for Windows 10 Enterprise and 1 VM for Windows Server 2016.

* Created NAT network to allow connectivity between VMs.

* Configured each VM; mounted the ISOs, connected each to the NAT network and increased number of processors to 2.

* Ran through installations of Windows on each VM.

* Renamed WS2016 computer to DC01 within Server Manager.

* Installed AD DS onto DC01 and promoted to Domain Controller (DC) - new forest called Springfield.com

* Forest and domain functional level of WS2016

* Assigned DC with static IP of 10.10.10.10

* Temporarily assigned static addresses to Windows 10 VMs to verify connectivity through the NAT network.
  Check whether you need to add the echo rule to firewall here or later when DHCP is installed

* Changed Windows 10 VM names and added each to the Springfield.com domain, using admin permissions - restart to apply.
  Joining to DC did not work, had to assign static IPs to DC and Computer, then use DC as primary DNS.
  
* NetBIOS domain name of SPRINGFIELD.

* Commands used to confirm DC "netdom query dc" & "dsquery server".

* Found the new computer object in AD, put it in an OU and made that the default OU for computers.
  Find the distinguished name of the OU, then use that after the redircmp powershell command. I deleted the computer that I'd already added, then when I tried to log into this m   machine with a domain account it didn't let me. I did a fresh join to the domain and this fixed it, the computer went into the correct new OU too.     

### DHCP

* Configured DHCP on DC, using user SPRINGFIELD/administrator.

* Created scope range 10.10.10.1 - 10.10.10.254/24.

* Excluded 10.10.10.1 - 99, default lease time of 8d.

* Added DC's static IP (10.10.10.10) as the DNS, Default Gateway (DG) and DHCP server.

* Added inbound rule to firewalls to allow echo requests.

* Enabled VMs to obtain IP automatically, and confirmed connectivity to server. Confirmed the VMs were getting IP addresses from DHCP scope correctly.

### USERS AND GROUPS

* Filled out the AD forest with characters from the Simpsons.

* Made groups for the users: "Powerplant", "Moe's Bar", "Simpson's Immediate Family", "Simpson's Extended Family", and "School".
Note that many of the characters overlap. For instance, Bart would be part of "Simpson's Immediate Family" and "School", and the "Simpson's Immediate Family" would be a group inside of "Simpson's Extended Family".

* Created a shared folder called SpringfieldFolder and within that made folders for each group - limited access to each folder to appropriate groups.
This is all about permissions management. What's the difference between NTFS and Share permissions..

* Made policy for password resets and password complexity requirements.

* Limited domain joins to domain admins only.
Any domain user can add a computer to the network domain usually, this is a security issue. Go to Server Manager > Tools > ADSI Edit (at this point I had to manually connect to the network before moving on) > Expand "Default Naming Context" > Select the correct domain and go to properties > Find the attribute called "ms-DS-MachineAccountQuota" > Change the value to 0. The default is 10, which allows any authenticated user from the domain to add workstations to the domain up to 10 times.

### GPOs

* For each user, mapped the share folder as a network drive to (K:).

* Created a GPO to prevent any user from using removable storage.
Computer Configuration > Policies > Administrative Templates > System > Removable Storage Access > Deny All Access.

*
