# 📋 General Blue Team Cheatsheet

> Comandos y técnicas esenciales para el análisis de Blue Team

---

## 🔍 **Threat Hunting**

### Comandos Básicos Windows
```cmd
# Procesos activos
tasklist /v
wmic process list full

# Servicios
sc query
net start

# Conexiones de red
netstat -ano
netstat -ab
```

### PowerShell para Hunting
```powershell
# Eventos de logon
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4624}

# Procesos con conexiones de red
Get-NetTCPConnection | Select LocalAddress,LocalPort,RemoteAddress,RemotePort,State,@{Name="Process";Expression={(Get-Process -Id $_.OwningProcess).ProcessName}}
```

---

## 🎭 **Threat Emulation**

### MITRE ATT&CK Tactics
- **Initial Access**: T1566 (Phishing)
- **Execution**: T1059 (Command Line Interface)
- **Persistence**: T1547 (Boot/Logon Autostart)
- **Defense Evasion**: T1055 (Process Injection)

### Atomic Red Team
```bash
# Instalar Atomic Red Team
IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing)

# Ejecutar test específico
Invoke-AtomicTest T1566.001
```

---

## 🦠 **Malware Analysis**

### Análisis Estático
```bash
# Información básica del archivo
file sample.exe
strings sample.exe
hexdump -C sample.exe | head -20

# Hashes
md5sum sample.exe
sha256sum sample.exe
```

### Herramientas Esenciales
- **PEStudio**: Análisis PE headers
- **Wireshark**: Captura de tráfico
- **Process Monitor**: Monitoreo en tiempo real
- **Volatility**: Análisis de memoria

---

## 📊 **SIEM Operations**

### Splunk SPL Básico
```spl
# Búsqueda básica
index=windows source="WinEventLog:Security"

# Estadísticas de eventos de logon
index=windows EventCode=4624 | stats count by user | sort -count

# Timeline de eventos
index=* | timechart span=1h count by sourcetype
```

### Elastic Stack (KQL)
```kql
# Eventos de autenticación fallida
event.code: 4625

# Procesos sospechosos
process.name: (cmd.exe OR powershell.exe) AND process.parent.name: winword.exe
```

---

## 🔬 **Digital Forensics**

### Volatility Commands
```bash
# Profile identification
volatility -f memory.dmp imageinfo

# Process listing
volatility -f memory.dmp --profile=Win7SP1x64 pslist

# Network connections
volatility -f memory.dmp --profile=Win7SP1x64 netscan
```

### Autopsy/Sleuth Kit
```bash
# Create timeline
fls -r -m / image.dd > bodyfile
mactime -b bodyfile > timeline.csv

# File system analysis
fsstat image.dd
istat image.dd inode_number
```

### Registry Analysis
```bash
# Extract registry hives
volatility -f memory.dmp --profile=Win7SP1x64 hivelist
volatility -f memory.dmp --profile=Win7SP1x64 printkey -K "Software\Microsoft\Windows\CurrentVersion\Run"
```

---

## 🌐 **Network Analysis**

### Wireshark Filters
```
# HTTP traffic
http

# DNS queries
dns

# Suspicious traffic
tcp.flags.syn==1 and tcp.flags.ack==0

# Large data transfers
frame.len > 1000
```

### Netstat Commands
```bash
# Active connections
netstat -ano | findstr ESTABLISHED

# Listening ports
netstat -an | findstr LISTENING

# Process associated with ports
netstat -b
```

---

## 🔒 **Security Tools**

### Nmap Scans
```bash
# Basic scan
nmap -sV -sC target_ip

# Vulnerability scan
nmap --script vuln target_ip

# Stealth scan
nmap -sS -T4 target_ip
```

### PowerShell Security
```powershell
# Check execution policy
Get-ExecutionPolicy

# Security event logs
Get-WinEvent -LogName Security | Where-Object {$_.Id -eq 4625}

# Installed software
Get-WmiObject -Class Win32_Product | Select Name, Version
```

---

## 📝 **Logging & Monitoring**

### Windows Event IDs
- **4624**: Successful logon
- **4625**: Failed logon
- **4648**: Logon with explicit credentials
- **4672**: Admin rights assigned
- **4697**: Service installed

### Sysmon Configuration
```xml
<Sysmon schemaversion="4.30">
  <EventFiltering>
    <ProcessCreate onmatch="exclude">
      <Image condition="end with">chrome.exe</Image>
    </ProcessCreate>
  </EventFiltering>
</Sysmon>
```

---

## 🚨 **Incident Response**

### Initial Triage
1. **Preserve Evidence**
2. **Identify Scope**
3. **Contain Threat**
4. **Collect Artifacts**
5. **Analyze & Report**

### Memory Acquisition
```bash
# Using FTK Imager
# File → Create Disk Image → Memory

# Using DumpIt
DumpIt.exe /OUTPUT C:\memory.dmp

# Linux memory
dd if=/dev/mem of=memory.dd
```

---

> 💡 **Tip**: Mantén este cheatsheet actualizado con nuevos comandos y técnicas que encuentres útiles durante tu journey de Blue Team!