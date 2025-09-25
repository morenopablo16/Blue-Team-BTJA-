# 02 - Digital Evidence

**Module**: Digital Forensics | **Date**: 2025-09-25

---

## Executive summary (6–7 lines)

Digital evidence is any data stored, transmitted or received by electronic devices that can support an investigation. Evidence origins fall into three practical categories for SOC work: computers (disk/file artifacts), networks (pcap, proxy/DNS logs, browser history) and mobiles (call logs, app data, GPS). Distinguish persistent (disk) from volatile (RAM) data and prioritize capture accordingly. Always protect integrity with hashing and record chain-of-custody metadata. Use targeted collection tools (KAPE) for fast triage and full imaging tools (FTK Imager/dc3dd) when required.

---

## Student-style notes (concise)

- Definition: digital evidence = data related to an investigation on electronic devices (stored, transmitted, received).
- Evidence origins: Computers | Network | Mobile — treat each with appropriate collection method.
- Computer evidence: files, emails, chat logs, deleted files, slack space, steganography in containers.
- Network evidence: browser history, proxy/router logs, DNS logs, PCAPs, social media posts, messaging apps.
- Mobile evidence: call history, SMS, contacts, apps, GPS/location, deleted app data — use specialist tools.
- Persistent vs volatile: persistent = storage media (disk/flash); volatile = RAM, active network sockets, ephemeral logs.

---

## Chain of Custody — quick rules

- Record: Received from, Received by, Date, Time, Case ID, Operator.
- Never analyse originals: create full-bit copies, hash originals and copies (SHA256), verify hashes match.
- Use write-blockers or read-only mounts where possible; if live capture required, document all commands and context.
- Sanitize forensic storage before use to avoid contamination.

---


## Quick facts / quiz answers (summary)

- Persistent data: stored on media (e.g., hard drive, USB).  
- Volatile data: lost on power-off (RAM, ephemeral system state).  
- To prove original == copy: compute and compare file hashes (SHA256 recommended).  
- Collecting evidence without authorization: generally illegal (warrants/permission needed).  
- Examples admitted in court: browsing history, ATM records, instant messages, GPS logs (when provenance established).

---

## Metadata / Tags

- tags: #digital-forensics #digital-evidence #02-digital-evidence
- difficulty: Introductory
- est_time: 30-60 minutes
- filename: 05-Digital-Forensics/Theory/02-digital-evidence.md

---
