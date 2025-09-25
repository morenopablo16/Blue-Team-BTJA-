	# 04 - Steganography

**Module**: Steganography | **Date**: 2025-09-25

---

## Executive summary (6–7 lines)

- Steganography is the practice of hiding data inside other files (cover files) so that the presence of the hidden data is not obvious. Typical covers are images or audio files. 
- Analysts should detect stego content by checking file headers (`file`), using detection tools (e.g., StegDetect), and attempting extraction with known stego tools.
- `steghide` is a common tool for embedding and extracting files in images/audio; it uses a passphrase to protect embedded data and supports `-cf`, `-ef`, and `-sf` flags.
- Embedding workflow: compress secret data (zip), then `steghide embed -cf cover.jpg -ef secret.zip` or use `-sf` to write a new stegofile.
- Extraction workflow: `steghide extract -sf stegofile.jpg` and provide the passphrase; multiple passphrases may need to be attempted during triage.
- The module includes a hands-on quiz where students try candidate passphrases and extract three flags from stego files.

---

## Student-style notes (concise)

- Definition: steganography hides a secret file or message inside a cover file so it looks benign to casual inspection.
- Common covers: JPEG/PNG images and various audio formats (cover file structure matters for what can be embedded).
- Tools mentioned: `steghide` (embed/extract) and `StegDetect` (detection aid).
- Install steghide on Debian-based systems: `sudo apt-get install steghide`.
- Embedding example:
	- Zip secret folder: `zip -r secret.zip secret/`
	- Embed: `steghide embed -cf laptop.jpg -ef secret.zip` (or `-sf laptop2.jpg` to output a new stegofile).
- Extraction example:
	- `steghide extract -sf laptop2.jpg` (enter passphrase when prompted). Extracted file will appear in the current directory.
- Passphrase strategy: try candidate passwords (module lists: `christmastree`, `darksky123`, `goldenwatch`) against each stegofile; failures will print errors.
- Detection tip: use `file` to verify file headers and `StegDetect` to flag likely stego images before brute-force extraction attempts.

---

## Quick examples / Quiz answers

- Embed command (question example):
	- `steghide embed -ef secretmessage.txt -cf coverfile.jpg -sf hiddenmessage.jpg`
- Quiz walkthrough answers (from module):
	- FLAG1 (from pizza.jpg, passphrase `christmastree`): kAN105KS
	- FLAG2 (from verypretty.jpg, passphrase `darksky123`): 001JDANL
	- FLAG3 (from car.jpeg, passphrase `goldenwatch`): 1LRBA9IU

---

## Metadata / Tags

- tags: #digital-forensics #steganography #04-steganography
- difficulty: Introductory
- est_time: 20-40 minutes
- filename: 05-Digital-Forensics/Theory/04_Steganography.md

---