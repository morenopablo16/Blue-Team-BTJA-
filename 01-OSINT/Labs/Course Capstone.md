# 🧪 Lab: OSINT Challenge - MSP Breach Investigation

**Module**: OSINT | **Date**: 2025-09-26

---

## 🎯 Objective
**Law Enforcement OSINT Investigation**

Investigate person-of-interest (@sp1ritfyre) believed to be associated with hacking group that:
- Compromised a Managed Service Provider (MSP)
- Attempting to sell stolen credentials on clear net and dark web
- Build complete profile and find evidence linking to MSP breach

**Three Main Objectives:**
1. Identify social media accounts/websites used by person-of-interest
2. Build comprehensive profile of the individual
3. Find evidence of malicious behavior and MSP breach connection

---

## 🔧 Tools Used
- Twitter/X investigation techniques
- Google Dorks for website discovery
- DNS enumeration (TXT records)
- Base64/Hexadecimal decoding tools
- TheHarvester (if applicable)
- Social media correlation techniques
- Website analysis tools
- WHOIS lookup services

---

## 📝 Investigation Template

### 🆔 Known Starting Information
- **Twitter Handle**: @sp1ritfyre
- **Context**: Associated with hacking group, MSP breach, credential sales
- **Note**: Email used for Twitter registration is fake (exclude from report)

### 🔍 Investigation Targets

#### Personal Information Required:
```
[1] First Name: [TO INVESTIGATE]
[2] Last Name: [TO INVESTIGATE]  
[3] Age: [TO INVESTIGATE]
[4] Country: [TO INVESTIGATE]
[5] Interests (5 minimum): [TO INVESTIGATE]
[6] Hacker's employer (company name): [TO INVESTIGATE]
[7] Hacker's position within company: [TO INVESTIGATE]
```

#### Online Presence Discovery:
```
[8] Self-Owned Website (Hacker owns the domain): [TO INVESTIGATE]
[9] Other Websites (Person does not own domain, such as blogs): [TO INVESTIGATE]
```

#### Evidence Collection:
```
[10] URLs of webpages directly tying individual to MSP breach: [TO INVESTIGATE]
```

#### Email Address Intelligence:
```
[11] Email addresses used by hacker (2 expected): [TO INVESTIGATE]
```

---

---

## 📋 Investigation Write-up

### 🔍 Step 1: Initial Twitter Profile Analysis

**Objective**: Analyze @sp1ritfyre Twitter profile for initial intelligence

**Process**:
1. Navigate to Twitter and search for @sp1ritfyre

**Key Discovery**: 
- Found a link that seems to be Base64 encoded string in bio: 
- https://t.co/M3KiW4ZSbd

![[Assets/Pasted image 20250926191543.png]]

It seems to go nowhere

But if we use a base 64 decoder on that url we get this website `redhunt.net`

![[Assets/Pasted image 20250926194416.png]]


The we looked up on google the actual address @sp1ritfyre and we found out a blogger account

![[Assets/Pasted image 20250926191650.png]]

- Profile contains suspicious encoded data that needs decoding on the location field

**Key Discovery**:
- **Self-Owned Website:**:  redhunt.net

**Tools Used**: Twitter, Browser inspection tools

---

### 🔓 Step 2: Base64 Decoding Discovery

**Objective**: Decode any encoded information found in Step 1

**Process**:
1. Identify Base64 encoded strings (look for = or == padding)
2. Use CyberChef (https://gchq.github.io/CyberChef/) or base64decode.org
3. Decode the string found in Twitter bio
4. Analyze decoded content for domains, emails, or other intelligence



![[Assets/Pasted image 20250926191850.png]]

**Key Discovery**:
- Decoded Base64 reveals: `https://sammiewoodsec.blogspot.com/`
- This appears to be a domain owned by the target
- Need to investigate this domain further

**Tools Used**: CyberChef, base64decode.org

---

### 🌐 Step 3: Domain Analysis - sammiewoodsec.blogspot


**Objective**: Extract and verify personal details from discovered sources

**Process**:
1. Analyze blog posts for personal information leakage
2. Look for real name mentions in "About Me" sections
3. Search for age, location, interests mentioned
4. Cross-reference information across multiple sources
5. Build comprehensive personal profile


![[Assets/Pasted image 20250926192519.png]]


![[Assets/Pasted image 20250926192459.png]]

**Key Discoveries From Blogs**:
- **Real Name**: Sam Woods
- **Age**: 23 years old
- **Country**: United Kingdom
- **Professional Role**: Junior Penetration Tester
- **Company**: PhilmanSecurityInc

**Tools Used**: Manual analysis, cross-referencing


---

### 📧 Step 4: Email Address Discovery

**Objective**: Identify email addresses used by the target (expecting 2)

**Process**:
1. Search blog "Contact Me" sections
2. Look for email addresses in website source code

**Key Discoveries**:
- Email 1:d1ved33p@gmail.com

![[Assets/Pasted image 20250926190822.png]]

Found in the blog he had an email that can be extracted with the Developer tools of the website


- Note: Exclude fake Twitter registration email as instructed

**Tools Used**: TheHarvester, Source code analysis, WHOIS data


---


**Final Intelligence Package**:
```
[1] First Name: Sammie
[2] Last Name: Woods
[3] Age: 23
[4] Country: United Kingdom
[5] Interests (5 minimum): Security, Reading, Photograpy, Gaming, Camping
[6] Hacker's employer: PhilmanSecurityInc
[7] Hacker's position: Junior Penetration Tester
[8] Self-Owned Website: redhunt.net
[9] Other Websites: sammiewoodsec.blogspot.com, sp1ritfyrehackerstories.blogspot.com
[10] Email addresses: d1ved33p@gmail.com
```


---

## 💡 Lessons Learned

### OSINT Methodology Effectiveness:
- **Base64 Decoding**: Critical for uncovering hidden information in social media
- **Cross-Platform Correlation**: Information spread across multiple platforms requires systematic approach
- **Blog Platform Intelligence**: Personal blogs often contain most detailed personal information
- **WHOIS Analysis**: Essential for confirming domain ownership and establishing connections

### Tool Performance Analysis:
- **Most Valuable**: CyberChef for decoding, Google Dorks for discovery, WHOIS for verification
- **Correlation Importance**: Manual analysis crucial for connecting disparate information sources
- **Timeline Analysis**: Critical for establishing patterns and confirming activities

### Professional Investigation Skills:
- **Systematic Approach**: Following methodical steps prevented missing critical intelligence
- **Evidence Documentation**: Proper documentation essential for court admissibility
- **Legal Compliance**: Staying within public information boundaries maintained investigation integrity
- **Multi-Source Verification**: Confirming information through multiple sources increased reliability


---

#lab #osint #investigation #law-enforcement #msp-breach #challenge