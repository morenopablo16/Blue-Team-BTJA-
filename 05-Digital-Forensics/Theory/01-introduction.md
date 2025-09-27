# 01 - Introduction to Digital Forensics

**Module**: Digital Forensics | **Date**: 2025-09-25

---

## Executive summary (SOC-focused)

Digital forensics is the disciplined practice of collecting, preserving, analyzing and presenting digital evidence so it can support incident investigations, intelligence sharing and (when required) legal action. From a Security Operations perspective, forensics bridges detection and response: it provides the technical proof needed to validate alerts, reconstruct timelines, and inform remediation. In modern DFIR workflows, fast triage (memory capture, critical log collection) and remote artefact extraction are often more valuable during an active incident than full disk imaging. Analysts should prioritise integrity (hashing, chain-of-custody), reproducibility (scripts and documented commands) and correlation with telemetry (SIEM/EDR) to deliver actionable findings.

---

## Topic notes — key concepts and operational takeaways

1) What is digital forensics
- Definition: investigation, preservation, analysis and presentation of digital evidence with integrity and auditability.

## Executive summary 

Digital forensics collects and validates digital evidence for investigations and legal use. In SOC operations, focus on quick, reproducible artifact capture (memory, critical logs, targeted files) and maintain integrity (hashes, chain-of-custody). Correlate findings with SIEM/EDR to expand scope and inform containment.

---

## Notes 

- Definition: digital forensics = preserve → analyze → present evidence with integrity.
- Main types: Computer (disk/MFT), Network (pcap, DNS, proxy), Memory (RAM dumps), Mobile (phone images).
- SOC priorities: memory + critical logs first; full disk later if needed.
- Key artifacts: MFT (NTFS), Windows Event Logs, Sysmon, browser history, prefetch, registry hives, pcap.
- Essential tools (collection): KAPE, FTK Imager, dc3dd, EnCase, Cellebrite (mobile).
- Essential tools (analysis): Autopsy, SleuthKit, Plaso/log2timeline, Volatility, Wireshark/Zeek.
- Integrity: compute SHA256, record operator, timestamp, case ID; keep original images read-only.
- Workflow tip: automate repeatable collection with scripts/KAPE to avoid mistakes and speed triage.

---

## Tools & short notes

- KAPE: fast targeted artifact collection; useful during live triage.
- FTK Imager / dc3dd: create disk and memory images; verify with hashes.
- Volatility: memory analysis; list processes, network sockets, loaded modules.
- Autopsy/SleuthKit: file system analysis, deleted files, timeline support via plaso.
- Wireshark/Zeek: network capture and analysis for C2/exfiltration patterns.

---

## Metadata / Tags

- tags: #digital-forensics #dfir #01-introduction
- difficulty: Introductory
- est_time: 30-60 minutes
- filename: 05-Digital-Forensics/Theory/01-introduction.md

---

Notes updated to follow user preferences: shorter executive summary, student-style concise notes; triage and study prompt sections removed.


---
