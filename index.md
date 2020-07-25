## Welcome to the Homelab Documentation Page



### Homelab

In this Lab I created a network of virtual machines (VMs) using the virtualisation software Oracle VM Virtualware. The purpose of the Lab was to develop practical knowledge of the Windows Server operating system and the Active Directory service.

### Initial Setup

    * Created 2 VMs for Windows 10 Enterprise and 1 VM for Windows Server 2016.
      
    * Created NAT network to allow connectivity between VMs.
      
    * Configured each VM; mounted the ISOs, connected to the NAT network and increased number of processors to 2.
      
    * Ran through installations of Windows on each VM.
      
    * Renamed WS2016 computer to DC01 within Server Manager.
      
    * Installed AD DS onto DC01 and promoted to Domain Controller (DC) - new forest called Springfield.com. 

    * Forest and domain functional level of WS2016.
      
    * Assigned Domain Controller with static IP of 10.10.10.10.
      
    * Temporarily assigned static addresses to Windows 10 VMs to verify connectivity through the NAT network.
      Check whether you need to add the echo rule to firewall here or later when DHCP is installed.
     
    * Changed Win10 VM names, and added each to the Springfield.com domain, using admin permissions - restart to apply.
      Joining to DC did not work, had to assign static IPs to DC and Computer, then use DC as primary DNS.
      
    * NetBIOS domain name of STARLITETECH.
      
    * Commands used to confirm DC “netdom query dc” & “dsquery server”.
      
    * Found the new computer object in AD, put it in an OU, make that the default OU for computers
      Find the distinguished name of the OU, then use that after the redircmp powershell command. I deleted the computer that I’d already added, then when I tried to log into         this machine with a domain account it didn’t let me. I did a fresh join to the domain and this fixed it, the computer went into the correct new OU too.


# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/r-kirman/homelab/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
