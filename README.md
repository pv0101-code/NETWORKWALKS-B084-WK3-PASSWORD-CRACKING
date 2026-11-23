# NETWORKWALKS-B084-WK3-PASSWORD-CRACKING
Password Cracking with JTR &amp; NW
# Week 3 Lab Report: Password Cracking with John the Ripper & Networkwalks Tools

A hands-on cybersecurity lab documentation covering password hash extraction and dictionary-based password recovery on password-protected PDF file (`My Locked PDF1.pdf`,`My Locked PDF2.pdf`, `My Locked PDF3.pdf`).

---

## 🎯 Lab Objectives

* Understand how password hashes differ from encryption and why weak passwords fail under dictionary attacks.
* Extract crackable `$pdf$` hashes from a password-protected PDF document.
* Perform password recovery using **John the Ripper (JTR)** (CLI / Johnny GUI).
* Practice browser-based hash extraction and cracking using **Networkwalks Hash Calculator** and **Networkwalks Password Cracker**.
* Document commands, workflows, troubleshooting steps, and security takeaways.

---

## 🛡️ Overview & Scope

Password cracking evaluates password resilience by testing candidate guesses against cryptographic verification data rather than relying on manual trial-and-error. In this lab, two complementary approaches were explored on `My Locked PDF1.pdf`:

1. **Module 1 (`W3-PM1`):** Recovering the PDF password using **John the Ripper** (`pdf2john` + `john` / Johnny GUI).
2. **Module 2 (`W3-PM2`):** Extracting the PDF hash and running a dictionary attack using **Networkwalks Hash Calculator** and **Networkwalks Password Cracker**.

> **Ethical Note:** All testing in this lab was performed strictly on authorized training/lab material for educational purposes.

---

## 🧪 Environment & Tools Used

* **Operating System:** Kali Linux (VM) / Windows
* **Password Cracking Suite:** John the Ripper Jumbo (`pdf2john`, `john`) and Johnny GUI
* **Wordlist:** `rockyou.txt` (and built-in/custom wordlists)
* **Browser Utilities:** Networkwalks Hash Calculator & Networkwalks Password Cracker

---

## 🪜 Execution Workflow

### Module 1: Cracking with John the Ripper (JTR)

1. **Obtain the Target File:** Downloaded `My Locked PDF1.pdf` into the working directory (using `gdown` for direct Drive downloads rather than `wget` on folder URLs).
2. **Extract the PDF Hash:** Extracted the hash string (`$pdf$...`) into a text file using `pdf2john`:
   ```bash
   pdf2john "My Locked PDF1.pdf" > pdf_hash.txt
   ```
3. **Run Dictionary Attack with John:** Executed `john` against the extracted hash using a wordlist:
   ```bash
   john --wordlist=/usr/share/wordlists/rockyou.txt pdf_hash.txt
   ```
4. **Verify & Unlock:** Checked recovered credentials with `john --show --format=PDF pdf_hash.txt` and used the discovered password to open the protected PDF.

*(Alternative GUI path: Configured Johnny GUI with the `john` executable path, loaded the saved `$pdf$` hash file, and started the attack.)*

---

### Module 2: Cracking with Networkwalks Web Tools

1. **Extract Hash via Hash Calculator:** Opened the Networkwalks Hash Calculator in the browser, provided `My Locked PDF1.pdf`, and copied the generated `$pdf$` hash string.
2. **Run Dictionary Attack via Password Cracker:** Pasted the `$pdf$` hash into the Networkwalks Password Cracker, selected a wordlist, and launched the attack until a match was found.
3. **Access the Document:** Used the recovered password in a PDF reader to unlock and view the file contents.




---

## 💡 Key Takeaways

1. **Hashing vs. Encryption:** Encryption protects data with a key for decryption, whereas hashing produces a one-way digest/verification value that attackers test against using high-speed guesses.
2. **Weak Passwords Fall Fast:** Simple or common passwords—even when locking a file—can be recovered quickly via dictionary attacks.
3. **Strong Password Hygiene:** Longer, unpredictable passwords with mixed character types significantly raise cracking effort and time.
4. **Clear Documentation Matters:** Recording commands, errors, fixes, and outcomes makes lab reports easy to review and reproduce.
