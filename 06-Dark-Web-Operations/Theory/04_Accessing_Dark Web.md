
# 📝 04_Accessing the Dark Web (Tor)

**Module**: Dark Web Operations | **Date**: 2025-09-27

---

## Short history and how Tor works

Tor (The Onion Router) started in the 1990s as a research project at the U.S. Naval Research Laboratory. David Goldschlag, Mike Reed and Paul Syverson developed onion routing to mitigate network surveillance: traffic is wrapped in multiple layers of encryption and forwarded through a sequence of independent nodes. Each node removes one layer of encryption and forwards the packet; no single node knows both the origin and the final destination. The Tor code became open-source in 2002. In the mid-2000s, developers (notably Roger Dingledine and Nick Mathewson) and supporters such as the EFF formalized development and founded The Tor Project to steward the code and community.

---

## Warning and legal disclaimer

- Tor improves privacy but does not guarantee complete anonymity. Adversaries and law enforcement monitor and may correlate activity.
- Using Tor to access illegal content, purchase contraband, or perform criminal acts is unlawful and out of scope for this course.
- Avoid downloading or executing files from unknown .onion sites. Use isolated analysis environments if you must retrieve files for research.

---

## Minimum safety checklist before using Tor Browser

1. Update your OS and all installed applications.
2. Use an isolated virtual machine or dedicated analysis host with snapshots.
3. Run up-to-date endpoint protection on the host (antivirus / EDR).
4. Consider using a trustworthy VPN before Tor Browser if your threat model requires it (understand trade-offs).
5. Download Tor Browser only from https://www.torproject.org and verify signatures or checksums when possible.

---

## Practical steps to access Tor

1. Download and verify Tor Browser for your OS.
2. Install and launch Tor Browser; choose Connect (or configure bridges if you are in a censored network).
3. Allow the browser to build a circuit. The status UI shows the Tor circuit and exit node.
4. Use the built-in privacy settings: do not enable plugins or additional extensions; block scripts when possible.
5. Avoid logging into personal accounts or reusing personal identifiers while browsing.

---

## Clear Web vs Dark Web (concise)

- Clear Web: indexed, reachable via regular DNS and HTTP(S). ISPs and network operators can observe and log requests.
- Dark Web (.onion): reachable only through Tor circuits. .onion addresses are not resolved via public DNS and typically end with the .onion TLD.

---

## Example .onion resources (educational / generally safe)

- Facebook (official onion mirror): https://www.facebookcorewwwi.onion/ — accessible via Tor for censored regions.
- SecureDrop (journalistic whistleblower submission system): http://secrdrop5wyphb5x.onion/ — used by newsrooms.
- ProtonMail onion access: https://protonirockerxow.onion/ — privacy-focused email provider.
- Note: many crypto mixers, wallets or marketplace sites are often linked to illegal activity and are unreliable; do not interact with them for coursework.

Important: .onion URLs change frequently; verify sources before using them.

---

## Operational best practices (concise)

- Use ephemeral VMs and rollback snapshots after sessions.
- Do not download or open files on your host; if necessary, download only inside an isolated VM and compute file hashes (SHA256) for record.
- Collect metadata (page HTML, timestamps, SHA256 of saved files) rather than interacting with sellers or forum members.
- Maintain a research log with actions, timestamps (UTC), and reasons for access; involve legal/compliance if material appears criminal.

---

## Troubleshooting and availability

- Many .onion services are unstable or migrate to new addresses. If a site is offline, consult reputable indexes or the official project's channels.
- If Tor Browser cannot connect, try using bridges, check local firewall rules, or verify that your network permits outbound TLS connections to Tor relays.

---

## Legal and ethical notes

- Accessing public information for defensive research, journalism or academics is typically permissible; however, possession or dissemination of illegal content is not.
- If you encounter illegal material, stop and escalate to your legal or incident-response teams according to policy.

---

## Class activity (structured)

1. Using Tor Browser, locate the current .onion mirror for a public service (e.g., CIA mirror, ProPublica) and record the exact URL and UTC access time.
2. Open the site's About or Mission page and copy the first sentence under the main heading.
3. Save the page HTML to a local file, compute its SHA256 checksum, and include the filename and checksum in your lab report.
4. Lab deliverable: .onion URL, UTC access timestamp, quoted sentence, saved filename, and SHA256 checksum. Do not include screenshots that reveal your personal identifiers.

---

## References

- The Tor Project: https://www.torproject.org
- EFF resources on privacy and anonymous communication
- SecureDrop documentation

---

#theory #dark-web-operations #tor #onion