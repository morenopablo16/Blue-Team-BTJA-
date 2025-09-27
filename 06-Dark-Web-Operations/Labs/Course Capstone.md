# 🧪 Lab: Dark Web Operations — Course Capstone

**Module**: Dark Web Operations | **Date**: {{date}}

---

## 🎯 Objective
Simulate a law-enforcement style investigation on a controlled, SBT-hosted dark site. You will gain access, collect intelligence about user activity, extract indicators of criminal behaviour, and produce forensically-sound evidence (saved files + checksums + timestamps).

---

## 🔧 Tools used
- Tor Browser (official) — for .onion access
- Web browser DevTools (Inspect → Console) — to run the JavaScript challenge
- CyberChef (or local Base64/hex tool) — decode Base64 and hex strings
- Steganography decoder (online or offline) — to extract hidden data from images
- Text editor and a checksum tool (sha256sum) — to save evidence and compute hashes

---

## Challenge scenario (brief)
After a major marketplace takedown, a remaining suspect operates a low-level dark website to “tell stories” and continue illicit trade. Your mission: access the site, identify evidence of drug trafficking, find locations where users congregate, and collect contact indicators for follow-up.

Site to use (SBT lab):
http://panznjcktrpezyln5frnjxf5gv4xoyi7wvd3ykeu6bejxvbynhfpasqd.onion

Primary tasks (deliverables):
1. Gain access: state the Console command used and provide the generated credentials.
2. List the three pinned post titles (decoded to ASCII) in order.
3. From the Messages board, provide the name of the linked illegal site mentioned.
4. From the Recent Transactions invoice, provide the customer full name, email, and purpose of the transaction (copy exactly as shown).
5. Determine the city and date/time for PJ's illegal party (use steganography as instructed).
6. Provide the email address of the user selling 'stolen' car parts.

---


## Walkthrough — step-by-step answers


Q1 — **What command is used in the Console to generate valid credentials? Provide the credentials, too**
1. Open Tor Browser and go to the lab .onion.
2. Click Login → Right-click → Inspect → Console.
3. Run: generateUserCredentials()


![](../../Assets/Pasted%20image%2020250927215032.png)


4. Copy the returned Base64 string and decode it


![](../../Assets/Pasted%20image%2020250927215119.png)

Credentials:
KF7ybuD1:Alyhfot0V9VIWm6W

Q2 — **After logging in, what are the titles of the three pinned posts seen on the website in ASCII text? Please place them in respective order.**?
1. After login, open the suspect's page. We can see the pinned posts right away. But they are encoded in Hex.

![](../../Assets/Pasted%20image%2020250927215429.png)


2. Use a hex decoder to convert the titles to ASCII.

![](../../Assets/Pasted%20image%2020250927215732.png)


**Answers**:
1. Drugs
2. Pleasure
3. Drops

Q3 — Look at the Messages board. They are mentioning another illegal site. Provide its name. (Format: Hacker Group Name)
1. Look on the page, in the Messages board, it is linked to another illegal site.

![](../../Assets/Pasted%20image%2020250927220113.png)

**Answer**: Midnite




Q4 — A transaction log is mistakenly visible under the “Recent Transactions” section. Provide the customer’s full name, email address, and the purpose of the transaction. (Format: Full Name, Email, Xxxxxxx and Xxxxx)?
1. If we click on the link over the 7000$ we can see the full invoice.
![](../../Assets/Pasted%20image%2020250927220533.png)

**Answer**: Frank Castle, frankcastle2093@gmail.com, Hookers and Drugs


Q5  — It looks like the user PJ is hosting an illegal party. What city is this taking place and when? We could catch him there and shut down this entire operation. (Format: City, Month DD, YYYY)
1. If we look at the posts we can see that PJ is mentioning a party. And we can extract the date of the party


![](../../Assets/Pasted%20image%2020250927221140.png)

2. He also says that the location is hidden in the image. We can download the image and use stego tools or strings to extract hidden text.
3. If we use a steganography tool to decode the image, we can find the hidden text containing the city.

![](../../Assets/Pasted%20image%2020250927221802.png)

3. Then we look which is the city whose capital is Cymru which is Cardiff.

**Answer**: Cardiff, February 14, 2025

Q7 — What is the email of the user selling ‘stolen’ car parts? (Format: Email)
1. Look in posts for long hex strings.

![](../../Assets/Pasted%20image%2020250927222011.png)

2. If we decode this block we get the email

![](../../Assets/Pasted%20image%2020250927222118.png)


**Answer**:twizzerichard@gmail.com

---


#lab #dark-web-operations #capstone #tor