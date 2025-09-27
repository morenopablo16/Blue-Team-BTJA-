
# 📝 02_Generating-Indicators

**Module**: Threat Hunting | **Date**: 2025-09-27

---

## 🎯 Key Concepts

### What are IOCs (Indicators of Compromise)
- **Definition**: Method of information sharing to help organizations identify similar attacks
- **Purpose**: Enable threat detection and sharing between organizations
- **Application**: Used in threat hunting to search for malicious activity

### Core IOC Categories
- **Network-based**: IP addresses, domains, URLs
- **Host-based**: File hashes, file names, file sizes, registry keys
- **Email-based**: Sender addresses, subject lines, attachment hashes
- **Behavioral**: Process names, command-line arguments, network connections

---

## 📝 Essential IOC Types & Collection Methods

### 1. File-Based Indicators

**File Size (Bytes)**
- **Linux**: `ls -lh filename` (shows human-readable) or `ls -l filename` (exact bytes)
- **Windows**: Right-click → Properties → Size
- **Usage**: Unlikely that many files have identical byte counts
- **Example**: Malware sample = 1,057,889 bytes

**File Names**
- **Collection**: Visible in file explorer or `ls` command
- **Best Practice**: Include full filename with extension
- **Example**: `malicious_file.exe`

**File Hashes (Critical for Malware Detection)**

**MD5 Checksums**:
```bash
# Linux
md5sum filename.txt
# Result: 5d363d305385b3a71ca7eed28eb2c209

# Windows PowerShell
Get-FileHash filename.txt -Algorithm MD5
```

**SHA-1 Checksums**:
```bash
# Linux
sha1sum filename.txt
# Windows PowerShell
Get-FileHash filename.txt -Algorithm SHA1
```

**SHA-256 (Industry Standard)**:
```bash
# Linux
sha256sum filename.txt
# Windows PowerShell (default)
Get-FileHash filename.txt
```

**Hash Properties**:
- **Uniqueness**: Identical files = identical hash
- **Sensitivity**: One character change = completely different hash
- **Collision Risk**: MD5 has higher collision risk than SHA-256

### 2. Network-Based Indicators

**IP Addresses**
- **Use Case**: Identify malicious command & control servers
- **Example**: Organization A detects DDoS from 5 IPs → shares with Org B for blocking
- **Application**: Set up alerts and firewall rules

**Email Addresses**
- **Use Case**: Phishing campaign detection
- **Example**: `purelyanexample@googlemail.com` sending malicious emails
- **Sharing**: Warn other organizations about sender

### 3. String-Based Indicators

**Extracting Strings**:
```bash
# Linux - extract human-readable strings from binary
strings malware.exe
```

**Selection Criteria**:
- **Unique strings**: Avoid common words (reduces false positives)
- **Example**: Malware contains "0wNeD BY #Lun4rSqUAD" → use "Lun4rSqUAD" as IOC
- **Application**: Search across file systems for matching strings

---

## 🛠️ Mandiant IOC Editor (IOCe)

### Tool Overview
- **Developer**: FireEye (Mandiant)
- **Purpose**: Create and manage IOC files in XML format
- **Platform**: Windows only

### IOC File Structure

**Logical Operators**:
- **OR Logic**: Any matching IOC triggers detection
- **AND Logic**: All IOCs must match for detection

**File Creation Process**:
1. **Installation**: Download from FireEye, create IOCs folder
2. **New IOC**: File → New → Indicator
3. **Populate Fields**: Name, Author, Description
4. **Add Indicators**: Right-click → Add Item → FileItem → [Type]

**Common IOC Categories in IOCe**:
- **FileItem**: MD5, SHA1, File Name, File Size
- **Network**: IP addresses, domains, ports
- **Email**: Sender, subject, attachments
- **Registry**: Keys, values, modifications

### Best Practices
- **Combine Multiple IOCs**: Use both file hashes and behavioral indicators
- **Test IOCs**: Verify accuracy before deployment
- **Regular Updates**: Refresh IOC databases as threats evolve
- **False Positive Management**: Choose specific, unique indicators

---

## � Practical Applications

### Threat Intelligence Sharing
- **Cross-Organization**: Share IOCs between security teams
- **Industry Groups**: Participate in threat intelligence feeds
- **Automated Detection**: Import IOCs into SIEM systems

### Malware Analysis Workflow
1. **Collection**: Gather file properties (size, name, hashes)
2. **String Extraction**: Identify unique text patterns
3. **IOC Creation**: Build comprehensive IOC files
4. **Deployment**: Integrate into hunting tools
5. **Validation**: Test detection accuracy


---


#theory #threat-hunting #ioc #malware-analysis #forensics