# 03 - Linux CLI (Navigation & File Inspection)

**Module**: Digital Forensics | **Date**: 2025-09-25

---

## Executive summary (6–7 lines)

Linux command-line basics let analysts navigate file systems, locate evidence, and inspect content quickly without a GUI. Start in your home directory (`pwd`) and use `ls`/`ls -a` to list files (hidden files shown with `-a`). Move with `cd` using absolute or relative paths and `cd ..` to go up. Use `find` with wildcards to locate files when paths are unknown. Inspect files with `strings`, `cat`, and `head` to reveal readable text or preview contents. Confirm true types with `file` and restore correct extensions with `mv` before extracting or further analysis.

---

## Student-style notes (concise)

- Start in home: opening a terminal places you in your user home (e.g., `/root/`); confirm with `pwd`.
- List files: `ls` (normal), `ls -a` (includes dotfiles / hidden files).
- Change directory:
  - Absolute: `cd /root/Desktop/DesktopFolder`
  - Relative: `cd Images`
  - Parent: `cd ..`
- Finding files: `find <start-path> -name "pattern"` — use `*` wildcards (e.g., `*secret*`).
- Read file contents:
  - `strings file` extracts printable strings from binaries or mixed files.
  - `cat file` outputs the full file.
  - `head file` shows first 10 lines (use `head -n N`).
- Identify true file type: `file filename` (reads header/magic). Use before `unzip`/extract operations.
- Fix incorrect extensions: `mv oldname.zip newname.jpeg` to restore correct handling and thumbnails.
- Hidden evidence: `ls -a` reveals `.private`-style dirs; `cd .private` + `cat secret.txt` to inspect.
- Practical workflow: combine `cd`, `ls -a`, `find`, `file *`, `strings`, `cat`, `head` to locate evidence and hidden content.

---

## Quick examples

- Find a file named `findme.txt` under `/root`:
  - `find /root -name "findme.txt"`
- Search for filenames containing `secret` in `/Elise`:
  - `find /Elise -name "*secret*"`
- Check type and rename a mislabelled file:
  - `file babyyoda2.zip`
  - `mv babyyoda2.zip babyyoda2.jpeg`
- Reveal hidden files and view a flag:
  - `ls -a`
  - `cd .private`
  - `cat flagfile.txt`

---

## Metadata / Tags

- tags: #digital-forensics #linux-cli #03-linux-cli
- difficulty: Introductory
- est_time: 20-40 minutes
- filename: 05-Digital-Forensics/Theory/03-linux-cli.md

---