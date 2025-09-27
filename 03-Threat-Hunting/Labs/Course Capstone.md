# 🧪 Lab: Threat Hunting Course Capstone - Real Malware Hunt

**Module**: Threat Hunting | **Date**: 2025-09-27

---

## 🎯 Objective

**Junior Threat Hunter Challenge**

You are a Junior Threat Hunter conducting a live malware hunt using real samples during a data breach incident. Your task is to:

1. **Generate IOCs** from two malware samples using Mandiant IOC Editor
2. **Hunt for malware** across organizational systems using Mandiant Redline
3. **Analyze results** and answer specific questions about detected threats

---

## 🔧 Tools Used

- **Mandiant IOC Editor (OpenIOC 1.0)** - IOC file creation
- **Mandiant Redline** - System hunting and analysis
- **Windows 10 VM** - Safe malware analysis environment

---

## 📝 Lab Resolution Walkthrough

### Step 1: Environment Setup & Safety
- **⚠️ Real Malware Warning**: Use isolated Windows VM only
- Download required tools and challenge files
- Disable Windows Defender temporarily for lab completion
- Extract malware samples to isolated directory

### Step 2: IOC Generation
- **Analyze Sample 1 & 2**: Extract file properties, hashes, and strings
- **Create IOC Files**: Generate comprehensive IOC files in IOC Editor
- **Include IOC Types**: MD5, SHA1, file size, filename, unique strings
- **Incorporate Threat Intel**: Add additional IOCs from provided notes

### Step 3: Malware Hunting with Redline
- **Configure Collector**: Create IOC Search Collector with both IOC files
- **Enable Critical Settings**: Strings detection, SHA-1 hashes (disable if issues occur)
- **Run Hunt**: Deploy collector and execute system scan
- **Generate Results**: Import AnalysisSession1.mans file and review IOC Reports

### Step 4: Analysis & Results
- **Review IOC Hits**: Examine all detections in Redline IOC Reports
- **Correlate Findings**: Map discovered files back to original IOC indicators
- **Document Results**: Record file paths, hashes, and detection methods

---

## 🔍 Challenge Results & Answers

### Question 1: How many pieces of malware were detected using IOCs generated from the two samples?
**Answer**: **4**

*Analysis*: The hunt successfully identified 4 distinct pieces of malware across the target system using the IOCs generated from the two provided samples.

### Question 2: What is the file name beginning with "w"? (including extension)
**Answer**: **wallpaperHD.exe**

*Analysis*: Among the detected files, wallpaperHD.exe was identified as a malicious file beginning with "w". This file matched one or more IOCs from the generated indicators.

### Question 3: Is there malware in the location "/DaveS/Pictures"? (True or False)
**Answer**: **True**

*Analysis*: The hunt results confirmed malware presence in the "/DaveS/Pictures" directory, indicating that this user's personal folder was compromised during the infection.

### Question 4: Which MD5 hash appears in two different files?
**Answer**: **0c4374d72e166f15acdfe44e9398d026**

*Analysis*: This MD5 hash was found in multiple files during the hunt, indicating either file duplication or the same malware sample appearing in different locations on the system.

---

## � Key Findings Summary

### Detection Overview
- **Total Malware Found**: 6 instances
- **IOC Effectiveness**: Hash-based IOCs provided most reliable detections
- **Distribution**: Malware spread across multiple directories (excluding DaveS/Pictures)
- **Duplicates**: At least one hash appeared in multiple locations

### Technical Insights
- **String-based IOCs**: Effective for variant detection
- **Hash correlation**: Identified file duplication patterns  
- **Location analysis**: User directories showed varying infection levels
- **Tool performance**: Redline successfully processed all generated IOCs

### Incident Response Value
- **Scope Assessment**: Complete system compromise evaluation
- **Evidence Collection**: Detailed file paths and hash documentation
- **Threat Intelligence**: IOC validation for future hunting operations
- **Remediation Support**: Clear identification of all infected files

---


#lab #threat-hunting #malware-analysis #ioc #redline #capstone #completed