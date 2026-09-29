# Password Cracking: Penetration Testing Project

**Pentester:** Aboderin Semilore Gold
**Program:** Networkwalks, Cybersecurity (Batch B083)
**Date:** 29 September 2026

## Overview
This project covers password cracking, a technique used to test how strong a password is by recovering it from a file's password hash. Two locked PDF files were provided, each cracked using a different toolset, to compare a desktop cracking tool against a browser-based one.

## Scope and Authorization
Both PDF files were provided by the Networkwalks program specifically for this lab exercise. No systems outside the lab task were tested.

## Background: Encryption vs Hashing
- **Encryption** is a two-way function: data encrypted with a key can be decrypted back to plain text with the right key.
- **Hashing** is a one-way function: it scrambles input into a fixed value (a hash) that cannot be reversed directly. Passwords are usually stored as hashes, not plain text, which is why cracking works by generating guesses, hashing each one, and comparing it to the stored hash rather than "decrypting" it.

## Part 1: W3-PM1 — Password Cracking with John the Ripper (JTR) & Johnny
**Tools:** John the Ripper, Johnny (GUI), Online Hash Extractor
**Target file:** My Locked PDF1.pdf

### Steps
1. Downloaded John the Ripper and the Johnny GUI for Windows from the official Openwall site.
2. Installed Johnny and pointed it to `john.exe` under Settings.
3. Uploaded the locked PDF to an online PDF hash extractor (pdf2john-based) to pull out its crackable hash.
4. Saved the hash to a text file (`hash1.txt`), starting exactly with `$pdf$`.
5. Opened the hash file in Johnny and clicked **Start new attack**.
6. Johnny cracked the password, which I then used to unlock the PDF in Adobe Acrobat.

### Result
- **Cracked password:** `password1`
- **Flag captured:** `nw{networkwalks_persistence_jtr_270521}`

![Hash value extracted](Hash%20value.png)
![Password cracker cracking the hash](password%20cracker.png)
![Flag captured](flag%20captured.png)

## Part 2: W3-PM2 — Password Cracking with Networkwalks Tools
**Tools:** Networkwalks Hash Calculator, Networkwalks Password Cracker (both browser-based, no install)
**Target file:** My Locked PDF2.pdf

### Steps
1. Opened the Networkwalks Hash Calculator (`networkwalks.com/hash-calculator/`) and uploaded the locked PDF.
2. The tool extracted a crackable hash in pdf2john/hashcat-compatible format, starting with `$pdf$`.
3. Copied the full hash and pasted it into the Networkwalks Password Cracker (`networkwalks.com/password-cracker/`).
4. Ran the dictionary attack using the built-in wordlist (100 passwords).
5. The tool tried different common passwords (service, canada, hockey, killer, george...) until it found a match.
6. Used the cracked password to open the PDF.

### Result
- **Cracked password:** `password1`
- **Flag captured:** `nw{cybersecurity_flag_captured_2608}`

![Hash calculator extracting the hash](Hash%20calculator.png)
![Capture the flag result](capture%20the%20flag.png)

## Comparison: JTR/Johnny vs Networkwalks Tools
| | JTR + Johnny | Networkwalks Tools |
|---|---|---|
| Install required | Yes (John the Ripper + Johnny GUI) | No, runs in browser |
| Hash extraction | Separate online tool needed | Built in (Hash Calculator) |
| Attack method | Dictionary/wordlist attack via John | Dictionary attack via built-in wordlist |
| Best for | Offline use, more attack modes, industry-standard tool | Quick browser-based testing, no setup |

## Problems Encountered & Solutions
- **Problem:** Downloaded the `.rpm` version of John the Ripper by mistake.
  **Cause:** RPM packages are for Red Hat-type Linux, not Windows.
  **Fix:** Downloaded the correct Windows `.zip` build from the official Openwall site instead.
- **Problem:** Wasn't sure Johnny could see John the Ripper.
  **Cause:** Johnny needs the exact path to `john.exe` set manually.
  **Fix:** Used Settings → Browse in Johnny to point directly to the `run` folder's `john.exe`.

## What I Learned
- The difference between encryption (reversible) and hashing (one-way).
- How a password hash is extracted from a protected file before it can be attacked.
- How a dictionary attack works: trying real words/common passwords instead of every possible combination.
- Why short or common passwords (like "password1") are cracked almost instantly, which is why strong, unique passwords matter.
- A desktop tool like John the Ripper offers more control and attack modes, while browser tools are faster to get started with for quick testing.

## Security & Ethical Use
Password cracking tools were used strictly on files provided for this authorised lab exercise. These techniques must never be used against real accounts, files, or systems without explicit written permission.

## Disclaimer
This work was done for educational purposes as part of the Networkwalks Cybersecurity Internship.
