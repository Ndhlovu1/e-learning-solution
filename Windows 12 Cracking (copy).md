netdiscover -i eth0

Question : 

# WINDOWS SERVER CRACKING

1. Setup File Server

2. Setup DNS, Active Directory, DHCP

______________________________________________________________________________________________

## STEP 1 : Adding Packages

1. In the WR12 : Go to Local Server

2. Select Manage : Choose Role Based Features

3. Select : 
	1. Active Directory Domain Services
	
	2. DHCP Server
	
	3. DNS Server
	
3. Click Next, Until you get to Install

____________________________________________________________________________________________________

## STEP 2 : Configuring Packages : ndhlovu.local

1. Select The Promote Icon in the Warning Information 

2. Select the Controller and choose add a new forest, then type the new domain name

3. Select the functional level that is 2years behind, hence the 2008 r2 server

123@DomainNdhlovu1!

10.1.10.2 : Server

------------------------------------------

## STEP 3

SET THE VMWARE TO BRIDGED AND PROMISCUOUS MODE TO ALLOW ALL

OPEN KALI

1. nmap -v -A 10.1.10.2 which will show the ports and search specifically for port 445

2. The script summary is (smb-vul-ms17-010 , EternaBlu) : Verify if the Server Message Block (SMB) can execute remote code.

nmap -p445 --script smb-vuln-ms17-010 10.1.10.2(target-machine) : Verify if it is vulnerable and then we can get the vulnerability status

nmap -p445 --script vuln 10.1.10.2(target-machine)


RUN MSFCONSOLE

search ms17-010(module name in brackets)

use exploit/exploit_path
_________________________________________
Basics : 

1. Familiarisation with Metasploit

2. Familiarisation with Nmap


_____________________________________
Links


https://infosecwriteups.com/cybertalent-exploiting-ms17-010-eternal-blue-on-a-remote-server-mature-blue-lab-18dee68da431

https://docs.rapid7.com/metasploit/working-with-payloads/

# NMAP SCANS

1. nmap -sV -sC target_ip

-sV: Version detection.
-sC: Runs default scripts.

2. nmap --script-help all

To list all available scripts, you can use the above
Nmap comes with a powerful scripting engine (NSE) that includes a wide variety of scripts for vulnerability detection.

3. nmap --script ssl-heartbleed target_ip

run specific scripts that check for known vulnerabilities. For example, to check for the Heartbleed vulnerability:

4. nmap --script vuln target_ip

The vuln category includes various scripts to check for common vulnerabilities, such as:

    http-vuln-cve2014-3704
    smb-vuln-ms17-010
    ftp-vsftpd-backdoor
    
 5. nmap --script=vuln target_ip
 
perform a comprehensive vulnerability scan, you can run all the scripts in the vuln category:


6. nmap -sV --script=vuln -oN output.txt target_ip

To save the scan results to a file, you can use the -oN (Normal output) or -oX (XML output) options

7. nmap --script smb-brute --script-args userdb=users.txt,passdb=passwords.txt target_ip

Some scripts require or can be fine-tuned with arguments using --script-args. For example, if you want to set a specific username and password for a script:

8. nmap --script-updatedb

It is essential to keep your Nmap scripts updated to detect the latest vulnerabilities. You can update the scripts with the following command:

9. nmap -sV --script=vuln --script-args=unsafe=1 target_ip

unsafe=1: This argument allows some scripts to run that might be more aggressive

















