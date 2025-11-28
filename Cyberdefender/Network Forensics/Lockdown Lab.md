# Scenario
TechNova Systems’ SOC has detected suspicious outbound traffic from a public-facing IIS server in its cloud platform activity suggestive of a web-shell drop and covert connections to an unknown host.

As the forensic examiner, you have three critical artefacts in hand: a PCAP capturing the initial traffic, a full memory image of the server, and a malware sample recovered from disk. Reconstruct the intrusion and all of the attacker’s activities so TechNova can contain the breach and strengthen its defenses.

# Tactics
`Execution`  , `Persistence`  , `Privilege Escalation`  , `Defense Evasion` , `Discovery` , `Lateral Movement` , `Command and Control`  

# Tools
`Wireshark` , `MemProcFS` , `Volatility 3` , `FLOSS/Strings` , `Threat Intel Tools`

# PCAP Analysis
### 1. After flooding the IIS host with rapid-fire probes, the attacker reveals their origin. Which IP address generated this reconnaissance traffic?
Answer: `10.0.2.4`

### 2. Zeroing in on a single open service to gain a foothold, the attacker carries out targeted enumeration. Which MITRE ATT&CK technique ID covers this activity?
Answer: `T1046`

### 3. While reviewing the SMB traffic, you observe two consecutive Tree Connect requests that expose the first shares the intruder probes on the IIS host. Which two full UNC paths are accessed?
Answer: `\\10.0.2.15\IPC$,\\10.0.2.15\Documents`
Filter for wireshark: `tcp.port == 445`

### 4. Inside the share, the attacker plants a web-accessible payload that will grant remote code execution. What is the filename of the malicious file they uploaded, and what byte length is specified in the corresponding SMB2 Write Request?
Answer: `shell.aspx, 1015024`
Filter for wireshark: `ip.src == 10.0.2.4 & ip.dst == 10.0.2.15 || smb2`

### 5. The newly planted shell calls back to the attacker over an uncommon but firewall-friendly port. Which listening port did the attacker use for the reverse shell?
Answer: `4443`
Filter for wireshark: `ip.src == 10.0.2.15 && ip.dst == 10.0.2.4 && tcp`

# Memory Dump Analysis
### 1. Your memory snapshot captures the system’s kernel in situ, providing vital context for the breach. What is the kernel base address in the dump?
Answer: `0xf80079213000` 
### 2. A trusted service launches an unfamiliar executable residing outside the usual IIS stack, signalling a persistence implant. What is the final full on-disk path of that executable, and which MITRE ATT&CK persistence technique ID corresponds to this behaviour?
Answer: `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\updatenow.exe,T1547`

### 3. The reverse shell’s outbound traffic is handled by a built-in Windows process that also spawns the implanted executable. What is the name of this process, and what PID does it run under?
Answer: `w3wp.exe`
Using: `pstree`

### 4. The reverse shell’s outbound traffic is handled by a built-in Windows process that also spawns the implanted executable. What is the name of this process, and what PID does it run under?
Answer: `w3wp.exe,4332`

# Malware Sample Analysis
### 1. Static inspection reveals the binary has been packed to hinder analysis. Which packer was used to obfuscate it?
Answer: `UPX`
Platform: `Virustotal`

### 2. Threat-intel analysis shows the malware beaconing to its command-and-control host. Which fully qualified domain name (FQDN) does it contact?
Answer: `cp8nl.hyperhost.ua`

### 3. Open-source intel associates that hash with a well-known commodity RAT. To which malware family does the sample belong?
Answer: `agenttesla`
