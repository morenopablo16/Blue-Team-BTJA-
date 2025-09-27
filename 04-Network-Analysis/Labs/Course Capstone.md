# 🧪 Lab: Network Analysis Course Capstone - Network Forensics Challenge

**Module**: Network Analysis | **Date**: 2025-09-27

---

## 🎯 Objective

**Network Analyst Challenge**

An attacker has plugged a laptop into an unused switch port on the internal network and is attempting to capture SSH credentials to access a central server. Your task is to analyze the provided network capture and recover the evidence that identifies the attacker, the attack technique, the file downloaded from the server, and any credentials obtained.

This document provides a GUI-first Wireshark step-by-step workflow to answer each quiz question. Where a CLI shortcut is significantly faster I also include a tcpdump/tshark alternative.

---

## 🔧 Main tools (GUI-first)

- Wireshark (GUI) — interactive packet inspection
- tshark / tcpdump — quick command-line extraction and searches (optional)

---


### Question 1 — What is the attacker's MAC address?

Wireshark GUI steps:
1. Menu: Statistics -> Endpoints.
2. In Endpoints, select the "Ethernet" (or "MAC") tab.
3. Click the "Frames" or "Bytes" column header to sort descending.


![](../../Assets/Pasted%20image%2020250927204417.png)


**Answer:** 08:00:27:3d:27:5d

### Question 2 — What attack allows the attacker to listen to conversations between the central server and another host?

Most likely an man-in-the-middle (MITM) attack such as ARP spoofing/poisoning or DNS spoofing. Look for evidence of this in the capture.


**Answer:** man-in-the-middle



### Question 3 — What file was downloaded from the central server?

Wireshark GUI steps (HTTP):
1. Go to the Statistics -> Protocol Hierarchy.
2. Expand the "File Transfer Protocol" section to see counts of requests and responses.
3. Follow the HTTP stream of a GET request/response to find the filename.


![](../../Assets/Pasted%20image%2020250927204805.png)

**Answer:** Alevis_Employee_Information_Chart.csv

### Question 4 — What department does Borden Danilevich work in?

Wireshark GUI steps:
1. Edit -> Find Packet (Ctrl+F).
2. Choose "String" and set "Search in" to "Packet bytes"
3. Search for `Borden.

![](../../Assets/Pasted%20image%2020250927205357.png)


4. When a match is found follow the FTP stream


![](../../Assets/Pasted%20image%2020250927205336.png)

**Answer:** Sales

### Question 5 — What is the SSH password of the Domain Administrator?


Wireshark GUI steps:
1. If we continue following the FTP stream from the previous question we can see that the password is visible in cleartext.
2. Find by searching for `admin` in the packet bytes.


![](../../Assets/Pasted%20image%2020250927205640.png)


**Answer:** gMR<4eXf]e6W

---



#lab #network-analysis #pcap #wireshark #capstone #mitm #gui
