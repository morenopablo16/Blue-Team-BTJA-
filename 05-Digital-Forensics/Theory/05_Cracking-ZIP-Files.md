# 05 - Cracking ZIP Files

**Module**: Cracking ZIP Files | **Date**: 2025-09-25

---

## Executive summary (6–7 lines)

- Password-protecting ZIP archives provides a basic confidentiality layer but is commonly encountered in investigations and often must be cracked to access evidence.
- Creating protected archives: `zip --encrypt Protected.zip file.txt` produces a password-encrypted ZIP that prompts for a password on extraction.
- Two common cracking approaches: brute-force (try all combinations) and dictionary (try likely human-chosen passwords from wordlists like rockyou.txt).
- Tools: `fcrackzip` is frequently used for brute-force and dictionary attacks against ZIP archives; performance depends on charset and length limits.
- Brute-force guarantees recovery eventually but is exponential in time; dictionary attacks are faster when the password is human-chosen but fail if it's not in the list.
- The module provides hands-on tasks and sample answers demonstrating both methods and how to extract flags from recovered archives.

---

## Student-style notes (concise)

- Protecting a ZIP: install zip (`sudo apt-get install zip`) and create an encrypted archive: `zip --encrypt Protected.zip text.txt` (enter password when prompted).
- Always record provenance: keeper of archive, acquisition method, and hashes — encryption does not remove chain-of-custody needs.
- Brute-force with `fcrackzip`:
	- Install: `sudo apt-get install fcrackzip`.
	- Basic brute-force flags: `fcrackzip -b -u -c <charsets> -l <len-range> target.zip`.
	- `-b`: brute-force; `-u`: try to unzip when candidate found; `-c a1`: choose character classes (e.g., `a`=lowercase, `1`=digits);
		`-l 4-6` restricts length to speed the search.
- Dictionary attack with `fcrackzip`:
	- Use `-D -p /path/to/wordlist` (e.g., `/usr/share/wordlists/rockyou.txt`).
	- Example: `fcrackzip -D -u -p /usr/share/wordlists/rockyou.txt DictionaryAttack.zip`.
- Wordlists: Kali/OffSec systems often include `rockyou.txt` (may be gzipped as `rockyou.txt.gz`; use `gunzip` to extract: `gunzip rockyou.txt.gz`).
- Practical guidance: constrain charset/length when you have intelligence (password policies) to drastically reduce brute-force time; prefer dictionaries first if social/target context suggests human passwords.
- Verify and extract: once password found, unzip with `unzip -P <password> target.zip` or `unzip target.zip` and enter the password interactively.

---

## Quick examples

- Create a passworded ZIP:
	- `zip --encrypt Protected.zip text.txt`  # prompts to set a password
- Brute-force (example):
	- `fcrackzip -b -u -c a1 -l 6-6 BruteForceAttack.zip`  # lowercase+digits, length exactly 6
- Dictionary attack (example):
	- `fcrackzip -D -u -p /usr/share/wordlists/rockyou.txt DictionaryAttack.zip`
- Extract after recovery:
	- `unzip -P a1b3c5 BruteForceAttack.zip`  # or interactive `unzip BruteForceAttack.zip` and enter password

---

## Quiz answers / Walkthrough (from module)

- Working password to unlock `BruteForceAttack.zip`: a1b3c5
- Working password to unlock `DictionaryAttack.zip`: FRIENDSHIPSTARS
- Text string inside `FLAG1.txt` (from BruteForceAttack.zip): J201AKKLO
- Text string inside `FLAG2.txt` (from DictionaryAttack.zip): 91MD0QL11

---

## Metadata / Tags

- tags: #digital-forensics #cracking-zip-files #05-cracking-zip-files
- difficulty: Introductory
- est_time: 30-60 minutes
- filename: 05-Digital-Forensics/Theory/05-cracking-zip-files.md

---