# 🧪 Lab: Course Capstone (Final Challenge)

**Module**: Digital Forensics | **Date**: 2025-09-25

---

## 🎯 Objective

Analyze a forensic disk image to locate four pieces of hidden evidence using the techniques covered in this course: Linux CLI navigation, hidden files, incorrect extensions, steganography, and password cracking. Preserve provenance (hashes, notes) and extract discovered artifacts for reporting.

---

## 🔧 Tools Used

- Kali Linux command-line (ls, cd, pwd, find, file, strings, cat, head)
- steghide (embed/extract)
- fcrackzip (brute-force/dictionary for ZIPs)
- unzip / zip
- tree (optional, for directory overview)
- sha256sum (hashing evidence copies)

---

## 📝 Steps (investigative workflow)

1. Acquire and prepare
	- Download and unzip the provided challenge image/zip in the Kali VM.
	- Keep a copy of the original archive; work on a copy or mounted image.
	- Compute and record hashes: `sha256sum challenge-image.img` (record value in case file must be re-verified).

2. Inventory the filesystem
	- Use `tree` (or recursive `ls -la`) to get a quick view of directories: `tree -a` or `ls -laR`.
	- Note suspicious filenames (large image sizes, unusual extensions, filenames starting with a dot).

3. Look for hidden files and incorrect extensions
	- In each target directory run `ls -a` to reveal dotfiles.
	- Run `file *` to check true types and detect renamed images (`posidon.xml` flagged as PNG).

4. Search for likely evidence strings
	- Use `strings` and `grep` on suspicious files to find keywords (passwords, flag-like strings):
	  - `strings suspicious.jpg | grep -i password`

5. Steganography checks
	- Use `steghide` to attempt extraction from likely cover files (images/audio). Try common passphrases from evidence or wordlist.
	- Example: `steghide extract -sf laptop.jpg` (enter passphrase when prompted).

6. Crack password-protected archives
	- If a ZIP is found and password-protected, use `fcrackzip` for brute-force or dictionary attacks.
	- Brute-force example (lowercase + digits, length 6): `fcrackzip -b -u -c a1 -l 6-6 BruteForceAttack.zip`.
	- Dictionary example: `fcrackzip -D -u -p /usr/share/wordlists/rockyou.txt DictionaryAttack.zip`.

7. Extract and preserve
	- Once content recovered, extract files to a dedicated evidence folder and compute hashes: `sha256sum recovered/* > evidence_hashes.txt`.
	- Record the exact path where each artifact was found and the commands used to recover it (chain-of-custody notes).

8. Reporting
	- Prepare a short report listing each evidence item, file path, extraction method, and hash. Include commands used and timestamps.

---

## 🔍 Key Findings (evidence summary)

Evidence 1/4
- File: hidden zip `.a0415ns.zip` (contains a text file named `employee dump`)
- ![](../../Assets/Pasted%20image%2020250925193357.png)
- Directory: `to-do`

We can get the password using john the ripper

![](../../Assets/Pasted%20image%2020250925193520.png)

- Artifact type: Employee personal information discovered inside the extracted `employee dump` text file.


4. **File Recovery**

![](../../Assets/Pasted%20image%2020250925193617.png)



Evidence 2/4
- File: `laptop.jpg` (stegofile containing an embedded file named `passwords`)

![](../../Assets/Pasted%20image%2020250925195319.png)


- Directory: `Images`
- Artifact type: List of employee passwords (extracted from the stego image using `steghide` with passphrase `password`).

Evidence 3/4
- File: `posidon.xml` (file whose header indicated PNG image data)
- Directory: `week 10`
- Artifact type: Office locations graphic (revealed after correcting extension and viewing the image).

Evidence 4/4
- File: `bootstrap.min.abc` (misleading extension; contains text)


![](../../Assets/Pasted%20image%2020250925195853.png)


- Directory: `css`
- Artifact type: Personal information for an individual named Colin found by `cat`ting the file.

---

## 💡 Lessons Learned & Operational takeaways

- Always run `ls -a` and `file *` when triaging a new image — hidden files and mislabelled types are common evidence vectors.
- Use targeted tools in sequence: detection (`file`, `StegDetect`), extraction (`steghide`), cracking (`fcrackzip`), and string inspection (`strings`, `grep`).
- Constrain brute-force jobs with known charset/length and prefer dictionary attacks when human-chosen passwords are likely (use `rockyou.txt`).
- Maintain provenance: compute and store hashes for originals and extracted artifacts immediately.

---

## 🔗 References

- Course sections: Linux CLI, Digital Evidence, Steganography, Cracking ZIP Files
- Tools: `man steghide`, `man fcrackzip`, `man file`, `man strings`

---

#lab #digital-forensics #capstone #completed
