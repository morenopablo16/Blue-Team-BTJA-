
# 📝 TCPDump — Study Notes

**Module**: Network Analysis | **Date**: 2025-09-27

---

Purpose: practical, student-style notes for using tcpdump to capture and analyse traffic from the command line. Includes concise examples and exact commands to answer the PCAP activity questions (PCAP4 & PCAP5).

---

1) What tcpdump is and why use it
- Command-line packet capture and analysis tool. Good for remote shells, automation, scripting, and quick inspections where GUIs are not available.
- Use cases: capture live traffic, save to .pcap, read pcap files, pipe output to grep/awk, and integrate with scripts.

2) Useful display/output options
- -A  : print packets in ASCII (good for HTTP payloads)
- -x  : print hex of packets
- -X  : print hex + ASCII
- -v / -vv / -vvv : increase verbosity (show more header fields)
- -tt / -ttt / -tttt : control timestamp verbosity/format

3) BPF filters (capture & read-time filters)
- Basic examples:
	- tcpdump -i eth0 tcp
	- tcpdump -i eth0 udp
	- tcpdump -i eth0 src 10.0.0.5
	- tcpdump -i eth0 dst port 22
	- tcpdump -i eth0 "host 192.168.1.5 and tcp port 80"
- Logical operators: and, or, not (or &&, || in some shells).

4) Inspecting PCAPs with tcpdump
- Read a pcap: tcpdump -r file.pcap -nn -tttt
	- -nn: don't resolve host/service names (keeps numeric addresses and ports)
	- -tttt: human readable full timestamp
- For text payload (HTTP): tcpdump -r file.pcap -nn -A 'tcp port 80'

5) Header-level and byte-offset filters
- TCP flags via byte offsets: tcp[13] gives the flags byte (offset 13 in TCP header). Use bitmasks:
	- SYN = 0x02, ACK = 0x10, SYN+ACK = 0x12
	- Example: filter SYN+ACK packets: 'tcp[13] & 0x12 == 0x12'
- IP TTL is ip[8] (TTL is the 9th byte of IPv4 header): ip[8] == 38 checks TTL == 38
- ICMP type byte is icmp[0] (e.g., icmp[0] == 8 for Echo Request)

6) Piping and text tools (practical patterns)
- Count UDP packets in a pcap:
	tcpdump -r SBT-PCAP4.pcap -nn udp | wc -l
- Print readable HTTP and search for User-Agent (Chrome version):
	tcpdump -r SBT-PCAP4.pcap -nn -A 'tcp port 80' | grep -i "User-Agent" | uniq -c
- Use awk to extract fields or grep for filenames:
	tcpdump -r SBT-PCAP5.pcap -nn -A 'tcp port 80 and host 192.168.56.111' | grep -i "GET .*\.png\|Content-Type: image/png"
- When tcpdump output is noisy, prefer tshark for field extraction (examples below).

---

Activity: exact commands & steps to answer PCAP questions

PCAP 4 — tcpdump/tshark GUI-free steps

Q1) How many UDP packets have been captured?
- tcpdump approach (fast):
	tcpdump -r SBT-PCAP4.pcap -nn udp | wc -l
- tshark (field extraction, recommended):
	tshark -r SBT-PCAP4.pcap -Y udp -T fields -e frame.number | wc -l

![](../../Assets/Pasted%20image%2020250927201224.png)
**Answer**=3290

Q2) How many TCP packets have both the SYN and ACK flags set?
- BPF (tcpdump) filter for SYN+ACK: tcp[13] & 0x12 == 0x12
	tcpdump -r SBT-PCAP4.pcap -nn 'tcp[13] & 0x12 == 0x12' | wc -l
- tshark equivalent (recommended):
	tshark -r SBT-PCAP4.pcap -Y 'tcp.flags.syn == 1 && tcp.flags.ack == 1' -T fields -e frame.number | wc -l

![](../../Assets/Pasted%20image%2020250927201400.png)

**Answer**=20

Q3) Which version of Chrome was used to connect to securityblue.team?
- tcpdump (ASCII scan):
	tcpdump -r SBT-PCAP4.pcap -vvv | grep -i chrome
	- Inspect the User-Agent string for "Chrome/version".
- tshark (clean extraction):
	tshark -r SBT-PCAP4.pcap -Y 'http.host == "securityblue.team" && http.user_agent' -T fields -e http.user_agent | sort | uniq -c

![](../../Assets/Pasted%20image%2020250927201534.png)

**Answer**=80.0.3987.87

Q4) How many packets have a TTL value of 38?
- tcpdump byte-offset filter:
	tcpdump -r SBT-PCAP4.pcap -nn 'ip[8] == 38' | wc -l
- tshark (field extraction):
	tshark -r SBT-PCAP4.pcap -Y 'ip.ttl == 38' -T fields -e frame.number | wc -l


![](../../Assets/Pasted%20image%2020250927201619.png)

**Answer**=710

PCAP 5 — tcpdump/tshark steps

Q1) What is the name of the PNG file on the webserver at 192.168.56.111?
- tcpdump approach:
	tcpdump -A -r SBT-PCAP5.pcap | grep png
	
![](../../Assets/Pasted%20image%2020250927202546.png)

**Answer**: proprietary.png


Q2) Which version of OpenSSH is running on the server?
- SSH server banners are sent in plaintext on connection. Use tcpdump to capture ASCII on port 22:
	tcpdump -vv -r SBT-PCAP5.pcap | grep OpenSSH
	
We get two results. The first one is the client connecting to the server. The next one is the server connecting to the client. We need to check the SSH version of the second result.

![](../../Assets/Pasted%20image%2020250927202715.png)

**Answer:** 7.9p1

Q3) On which port is the .zip file being served?
- Search for HTTP GET requests for ".zip" and note the port in the packet header lines:
	tcpdump -r SBT-PCAP5.pcap -nn -A | grep -i -n ".*\.zip" -n


![](../../Assets/Pasted%20image%2020250927203004.png)


**Answer:** 3016

Q4) When was a packet with a TCP checksum value of 53203 captured? (Format: xx:xx:xx.xxxxxx)
- Convert decimal checksum to hex: 53203 decimal = 0xCFD3. Use tshark to find packets by tcp.checksum:
	tshark -r SBT-PCAP5.pcap -Y 'tcp.checksum == 0xCFD3' -T fields -e frame.time
	- Output will contain timestamps in human readable format; extract the time (xx:xx:xx.xxxxxx) portion.

![](../../Assets/Pasted%20image%2020250927203132.png)

**Answer:** 11:04:46.207925000




---

#theory #network-analysis #tcpdump #pcap