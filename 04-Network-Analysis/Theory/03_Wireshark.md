
# 📝 Wireshark — Concise Study Notes

**Module**: Network Analysis | **Date**: 2025-09-27


---

1) GUI essentials
- Startup: choose interface, set capture filter, start capture.
- Main: Packet List | Packet Details | Hex view. Use Display Filter bar to focus results.
- Quick actions: Right-click field -> Apply as Filter / Apply as Column. Follow Stream -> shows full conversation.

2) Capture vs Display filters (examples)
- Capture (pcap-level): tcp port 80
- Display (rich fields): http.request  OR  ip.addr == 192.168.1.5

3) Capture workflow (short)
- Choose interface -> optional capture filter -> Start -> reproduce activity -> Stop -> Save .pcapng

4) Quick analysis steps
- Start: Statistics -> Protocol Hierarchy / Endpoints / Conversations
- Isolate: apply display filters, follow streams, add columns
- Evidence: note packet number and timestamp for answers

5) Essential display filter cheats
- udp
- dns.flags.response == 1
# 📝 Wireshark — Study Notes 

**Module**: Network Analysis | **Date**: 2025-09-27

---

Purpose: clear, study-focused notes written like a student's notebook. Balanced length: enough context to remember concepts and enough concision to review quickly.

---

1) GUI essentials
- Startup window: choose interface, set an optional capture filter, open saved captures, start/stop capture.
- Main window: three panes — Packet List (summary), Packet Details (protocol tree), Hex/ASCII (raw bytes). Use the Display Filter bar to focus results.
- Quick actions: right-click a field -> Apply as Filter / Apply as Column. Right-click a packet -> Follow -> TCP/UDP/HTTP Stream to view the whole conversation.

2) Capture vs Display filters (practical)
- Capture filters (BPF): applied while capturing, simple syntax, reduces captured volume. Examples:
  - tcp port 80
  - not arp
- Display filters: applied after capture, protocol-aware and powerful. Examples:
  - http.request
  - ip.addr == 192.168.1.5

Tip: when in doubt, capture everything (no capture filter) and filter later unless storage or privacy constraints exist.

3) Capture workflow (practical steps)
1. Select the correct interface (watch the activity graphs).
2. Optional: add a capture filter for noisy networks.
3. Start capture, reproduce the action to trace (e.g., open a webpage or run the sample in a VM).
4. Stop capture, save as .pcapng.
5. Export subsets via Display Filter -> File -> Export Specified Packets -> Displayed.

4) Analysis workflow — fast method
- Triage: Statistics -> Protocol Hierarchy to spot odd protocols.
- Host focus: Statistics -> Endpoints and Conversations to find noisy hosts and important ports.
- Filter: apply display filters to isolate traffic (protocols/ports/addresses/fields).
- Context: Follow Stream to reconstruct application-layer activity.
- Evidence: note packet number(s), timestamps, and filters used for any answer.

5) Useful display filters (memorize these)
- udp
# 📝 Wireshark — Study Notes (medium)

**Module**: Network Analysis | **Date**: 2025-09-27

---

Purpose: study-focused notes with moderate length — clear GUI steps, practical filters, a short workflow, and GUI-only methods to solve the exercise questions.

---

1) GUI essentials
- Startup window: choose the interface, set an optional capture filter, open saved captures, and start/stop capture.
- Main window: three panes — Packet List (summary), Packet Details (protocol tree), Hex/ASCII (raw bytes). Use the Display Filter bar to focus results.
- Quick actions: right-click any field -> Apply as Filter or Apply as Column. Right-click a packet -> Follow -> TCP/UDP/HTTP Stream to view the full conversation.

2) Capture vs Display filters (practical)
- Capture filters (BPF): applied while capturing. Simple examples:
  - tcp port 80
  - not arp
- Display filters: applied after capture and protocol-aware. Examples:
  - http.request
  - ip.addr == 192.168.1.5

Tip: capture everything if you can, then filter with display filters during analysis.

3) Capture workflow (practical steps)
1. Select interface (watch activity graphs) and set capture filter if needed.
2. Start capture and reproduce the activity (web browse, file transfer, run VM sample).
3. Stop capture, save as .pcapng, and export subsets using Display Filter -> File -> Export Specified Packets -> Displayed.

4) Analysis workflow (fast)
- Triage: Statistics -> Protocol Hierarchy to find dominant or unexpected protocols.
- Hosts: Statistics -> Endpoints and Conversations to find noisy hosts and main ports.
- Narrow: apply display filters to isolate traffic for the suspected host/protocol.
- Context: Follow Stream to reconstruct sequences (HTTP, TCP, UDP, SSL streams).
- Evidence: record packet numbers and timestamps for final answers.

5) Useful display filters (memorize)
- udp
- icmp
- dns.flags.response == 1
- tcp.port == 80
- http.request
- smb2.filename

---

6) GUI-only walkthrough for the PCAP exercise

PCAP1 — GUI steps

1) Which protocol was used over port 3942?  
 - Open the PCAP in Wireshark.
 - Enter in the Display Filter bar: tcp.port == 3942 || udp.port == 3942 and press Enter.
 - Check the "Protocol" column in the Packet List for the shown packets.
 
![](../../Assets/Pasted%20image%2020250927191330.png)

**Answer**= SSDP


1) What is the IP address of the host that was pinged twice?
 - Filter: icmp and press Enter.
 - Look for "Echo (ping)" entries in the Info column. Note the Destination IP for Echo requests.

![](../../Assets/Pasted%20image%2020250927191546.png)

**Answer**= 8.8.4.4

3) How many DNS query response packets were captured?
 - Filter: dns.flags.response == 1 and press Enter.
 - Read the displayed packet count in the bottom-left status bar (Displayed: X/Y) — X is the number of matching DNS responses.

![](../../Assets/Pasted%20image%2020250927191721.png)

**Answer**=90

4) Which IP sent the most number of bytes?
 - Open Statistics -> Endpoints -> IPv4.
 - Click the "Bytes" column to sort descending; the top entry shows the IP that sent the most bytes.

![](../../Assets/Pasted%20image%2020250927191903.png)

**Answer**=192.168.1.7

PCAP2 — GUI steps

1) What is the WebAdmin password?
 - Filter: http.request.method == GET and press Enter.
 - Identify GET packets aimed at the WebAdmin path 
 - Right-click the GET packet and choose Follow -> HTTP Stream to view the request body.

![](../../Assets/Pasted%20image%2020250927192201.png)

**Answer**=sbt123

2) What is the version number of the attacker’s FTP server?
 - Filter: ftp or tcp.port == 21 and press Enter.
 - Find the first FTP server response (code 220) in the Packet List.


![](../../Assets/Pasted%20image%2020250927192424.png)


**Answer**=pyftpdlib 1.5.5


3) Which port was used to gain access to the victim Windows host?
 - Identify the victim: Statistics -> Endpoints (IPv4) to spot unusual hosts.
 - Right-click the victim IP in Endpoints -> Apply as Filter -> Selected.
 - With that IP filtered, open Statistics -> Conversations -> TCP and inspect destination ports; sort by Bytes to find the session used to gain access and note its destination port.

![](../../Assets/Pasted%20image%2020250927195452.png)



**Answer**=8081


4) What is the name of a confidential file on the Windows host?
 - If you follow the TCP stream of the previous question you can find that confidential file

![](../../Assets/Pasted%20image%2020250927195726.png)

**Answer**=Employee_Information_CONFIDENTIAL.txt

5) What is the name of the log file that was created at 4:51 AM on the Windows host?
 - If you keep follow the TCP stream you ca nsee that i file was created on 4:51 AM


![](../../Assets/Pasted%20image%2020250927195934.png)


**Answer**=LogFile.log

Notes: All answers can be produced using Wireshark GUI tools: Display Filter bar, Packet List, Packet Details, Follow Stream, Statistics -> (Protocol Hierarchy / Endpoints / Conversations), and Find (Ctrl+F).

---

#theory #network-analysis #wireshark #pcap