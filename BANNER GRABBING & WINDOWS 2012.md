# Defending Windows r2 2012


1. WHITELIST ON WINDOWS

2. SETUP FIREWALL RULES

3. CHANGE THE IP ADDRESSES FOR SPECIFIC PORTS

4. CHANGE DEFAULT NAMES


--------------------------------------------------------------------

# HOW TO PREVENT BANNER GRABBING

1. Disable Information Leaks in IIS if running a web server ✅ 
	a. Open IIS Manager
	
	b. Select the server in the left panel, then double click on "`HTTP Response Headers`"
	
	c. In the right hand side, click `Remove` for the `X-Powered-By` and `Server` Headers
	
2. Edit web.config file to suppress details ✅ 

	a. Add the code below into your web.config file to prevent error details
	
		```
			<system.webServer>
			  <httpErrors errorMode="Custom" />
			  <security>
			    <requestFiltering removeServerHeader="true" />
			  </security>
			</system.webServer>
		```
		
3. Registry Edit to remove Server Header ✅ 
	
	a. Open Registry Editor and navigate to: Press Win + R -> regedit then follow the path below
	`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HTTP\Parameters`
	
	b. Add a new `DWORD` value named `DisableServerHeader` and set it to one

4. Disable Unnecessary Services : Disable services on the server that aren't being used, they should be disabled. 
	e.g. Open Services.msc and disable services that are not needed (e.g. Telnet, FTP, etc)
	
	a. Get-Service | Select-Object Name, DisplayName, Status : Disable services that are not being used
	
	b. Press Win + R -> services.msc , This will show you all the services and their status
	
	c. In the manager : Right Click a service you dont want to run, click stop if running then right click and choose properties and select disabled
	d. There are several services to consider disabling over the network such as :
		1. Lanman Server : Supports file and printer sharing over the network.
			-> Can be exploited to access shared resources. Disable if the server is not sharing files or printers.
		
		2. NetBIOS over TCP/IP (TCP/IP Protocol Driver) : Allows NetBIOS services to be used over TCP/IP
			-> Can expose the server to NetBIOS-related attacks. Disable if not required for legacy apps
		
		3. TCP/IP NetBIOS Helper (LmHosts) : Allow NetBIOS name resolution over TCP/IP
			-> Can be exploited for network reconnaissance. Disable if your network does not rely on NetBIOS
			
		4. Workstation : Maintains network connections and access to shared resources.
			-> Can be used to connect unauthorized shares. Disable if the server does not need to print
			
		5. Remote Registry(RemoteRegistry) : Allows remote access to the Windows Registry.
			-> Can be exploited to modify the registry remotely. Disable unless remote registry access is specifically needed for administration
		
		6. Print Spooler (Spooler) : Manages print jobs sent to printers.
			-> Vulnerable to exploitation e.g PrintNightmare Vulnerability. Disable if server does not need to print
			
		7. IP Helper (iphlpsvc) : Provides support for IPv6 transition technologies. 
			-> May expose vulnerabilities if not needed. Disable if your environment does not require IPv6.
			
		8. Distributed Link Tracking Client (TrkWks) : Maintains links to files in distributed environments.
			-> Can expose the server to potential vulnerabilities. Disable if not using distributed file systems
			
		9. SSDP Discovery Service (SSDPSRV) : Enables discovery of UPnP devices.
			-> Can be used for network reconnaissance. Disable if UPnP devices is not needed
			
		10. UPnP Device Host (UPnPHost) : Allows the hosting of Universal Plug and Play devices.
			-> Can introduce vulnerabilities and unauthorized access. Disable if PnP is not in use
			
		11. Routing and Remote Access (RemoteAccess) : Provides routing services and VPN access. 
			-> Provides routing service and VPN access. Disable if not being used as a router or VPN service
			
		12. Windows Error Reporting Service (WerSvc) : Provides error reporting to Microsoft. 
			-> Can be exploited to gather information about system vulnerabilities. Disable if you do not need error reporting
			
Assess Your Needs: Before disabling any service, assess your server's role and requirements. Some services may be necessary for specific applications or functionalities.
Consult Documentation: Check the documentation for your applications and server role to identify essential services.
Test After Disabling: After disabling any service, monitor the server for functionality and stability to ensure there are no unintended consequences.
Keep the Server Updated: Regularly update the server and apply security patches to minimize vulnerabilities.
Limit Access: Ensure that only necessary accounts have administrative privileges and access to critical services.

5. Harden SSH (If using OpenSSH) : 
	
	a. Edit the `sshd_config` file to disable the ssh banner
	
	b. Set the `Banner None` to disable the display of SSH banners
	
	c. Set `Protocol 2` to ensure you are using the most secure version of the SSH Protocol
	
6. Use a firewall :
	
	a. Open Windows Firewall with Advanced Security
	
	b. Set up Inbound Rules and Outbound Rules to limit access to services that aren't needed or to restrict banner grabbing attempts
	
	c. Block access to known ports commonly used for banner grabbing (e.g. TCP 21, 22, 80, 443, 8080)
	
7. Use Network Devices (IPS/IDS or Load Balancers) : Deploy network security devices like IPS or IDS that can detect and block banner grabbing attempts


8. Update and Patch Your Software : Ensure that your Windows Server and any application on it are fully updated and patched. Running the latest versions of software and applying security patches reduces the risk of exploits through banner grabbing.

9. Disable SMB and NetBIOS : Unnecessary protocols like SMB and NetBIOS may expose server details

	a. Disable SMBv1 : `Set-SmbServerConfiguration -EnableSMB1Protocol $false`
	
	b. Disable NetBIOS over TCP/IP
	
		1. Open Network and Sharing Center > Change Adapter Settings
		
		2. Right-Click on your network adapter and go to properties
		
		3. Select Internet Protocol Version 4 (TCP/IPv4) and Click Properties
		
**THE ABOVE INCREDIBLY AND EFFECTIVELY REDUCE THE RISK OF EXPOSING SENSITIVE INFORMATION THROUGH BANNER GRABBING**

## TEST THE BANNER GRABBING

1. `nc -v -z target_ip targert_port` : e.g. nc -v 10.1.10.2 80 - Attempt to grab a banner from a web server
	
2. `nmap --script banner target_ip`

3. echo -e "HEAD / HTTP/1.0\r\n\r\n" | nc 10.1.10.2 80
	
	
	
	
	
	
	
	
	
	
	





