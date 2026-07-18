DNS & WINS Configuration Audit Tool
-----------------------------------
PowerShell automation tool for collecting DNS and WINS configuration settings from multiple Windows servers and generating a consolidated network configuration report.

Overview
---------
The DNS & WINS Configuration Audit Tool helps Windows administrators quickly collect and review DNS and WINS settings across multiple servers from a single location.
The script reads a server list from a text file, prompts for administrative credentials, remotely queries all IP-enabled network adapters, and gathers DNS and WINS configuration information for each server.
This tool is particularly useful during:

DNS migration projects
WINS decommissioning initiatives
Server onboarding activities
Infrastructure documentation reviews
Network troubleshooting
Compliance audits
Data center migrations
Network standardization projects

Features
---------
Graphical server list file picker
Secure credential prompt
Remote WMI-based data collection
DNS server discovery
WINS server discovery
Primary DNS identification
Secondary DNS identification
Primary WINS identification
Secondary WINS identification
Multi-server auditing
Consolidated reporting
Real-time error handling

How It Works
------------
The script performs the following actions:

Prompts the administrator to select a server list file
Reads server names from the selected text file
Prompts for administrative credentials
Connects to each server using WMI
Identifies all IP-enabled network adapters
Retrieves DNS server settings
Retrieves WINS server settings
Stores the results in memory
Displays a consolidated report in table format

Information Collected
----------------------
For every IP-enabled network adapter, the script collects:

Server Name
Primary DNS Server
Secondary DNS Server
Primary WINS Server
Secondary WINS Server

DNS Information
---------------
The script retrieves configured DNS servers from each network adapter.
Example:
Primary DNS: 10.10.10.10
Secondary DNS: 10.10.10.11
If only one DNS server is configured:
Secondary DNS: Not Configured

WINS Information
-----------------
The script retrieves configured WINS servers from each network adapter.
Example:
Primary WINS: 10.20.20.10
Secondary WINS: 10.20.20.11

Server List Format
-------------------
Create a text file containing one server name per line.
Example:
SERVER01
SERVER02
SERVER03
SERVER04
SERVER05
Save the file as:
Servers.txt
When the script starts, a file browser window appears allowing you to select the server list file.

Authentication
--------------
The script prompts for credentials that will be used across all target servers.
Examples:
DOMAIN\Administrator
SERVER01\Administrator
The supplied credentials are passed to all remote WMI queries.

Network Adapter Discovery
--------------------------
The script queries:
Win32_NetworkAdapterConfiguration
Only adapters with IP enabled are processed.
This ensures that disconnected, disabled, or inactive adapters are automatically ignored.

Output Format
-------------
Results are displayed in a formatted PowerShell table.
Example:
ServerName      PrimaryDNS      SecondaryDNS      PrimaryWINS      SecondaryWINS
SERVER01        10.1.1.10       10.1.1.11         10.1.2.10        10.1.2.11
SERVER02        10.1.1.10       Not Configured    10.1.2.10        Not Configured
SERVER03        10.2.1.10       10.2.1.11         Not Configured   Not Configured

Error Handling
--------------
If the script cannot retrieve configuration information from a server, an error is displayed.
Example:
Failed to get network adapter settings for SERVER01: Access is denied.
Common failure scenarios include:

Invalid credentials
RPC failures
WMI service issues
Firewall restrictions
Network connectivity problems
Offline servers
DNS resolution failures

Prerequisites
--------------
PowerShell

PowerShell 5.1 or later

Administrative Access
The account running the script should have:

Administrative rights on target servers
Remote WMI access permissions
Network access to target servers

WMI Requirements
The following service should be operational on target servers:

Windows Management Instrumentation (WMI)

RPC Requirements
The following services should be operational:

Remote Procedure Call (RPC)
RPC Endpoint Mapper

Firewall Requirements
The environment should permit:

WMI traffic
RPC communication
Administrative remote access

Usage
-----
Run the script:
.\DNS-WINS-Configuration-Audit.ps1
Select the server list file.
Enter administrative credentials when prompted.
Allow the script to complete.
Review the results displayed in the PowerShell console.

Example Workflow
-----------------
Network Configuration Audit

Export server inventory to a text file
Launch the script
Select the server list file
Enter administrative credentials
Allow collection to complete
Review DNS settings
Review WINS settings
Identify inconsistencies or non-standard configurations

Benefits
--------
Eliminates manual server-by-server checks
Provides centralized visibility into DNS settings
Helps identify outdated WINS configurations
Supports migration planning
Improves network documentation
Simplifies compliance auditing
Accelerates troubleshooting efforts
Reduces operational overhead

Use Cases
---------
DNS standardization projects
WINS migration assessments
Infrastructure documentation reviews
Disaster recovery planning
Compliance reporting
Network troubleshooting
Server onboarding validation
Data center migration planning

Limitations
-----------
Requires administrative credentials
Depends on WMI availability
Requires network connectivity
Results are displayed in the console only
No automatic CSV export
Queries only IP-enabled adapters
Processes servers sequentially

Future Enhancements
--------------------
CSV export capability
Excel reporting
HTML reporting
Email summary generation
Parallel processing
Gateway information collection
IP address inventory reporting
DHCP configuration reporting
DNS consistency validation
Automatic compliance checks


Author
-------
Sundaram Gaur
Senior Systems Engineer | Windows Server | PowerShell Automation | Infrastructure Operations

Disclaimer
-----------
This script is intended for authorized administrative use only. It retrieves network configuration information from remote Windows servers and requires appropriate permissions and connectivity. Always ensure organizational policies and security requirements are followed when performing infrastructure auditing activities.
