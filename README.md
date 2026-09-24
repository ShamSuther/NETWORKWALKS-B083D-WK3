# PASSWORD CRACKING REPORT
### W3-FINAL | CYBERSECURITY | NETWORKWALKS

---

| Field | Details |
|---|---|
| **Pentester Name** | *Sham Sunder* |
| **Program/Batch** | *B083 – Networkwalks* |
| **Date** | *24 September 2026* |
| **Modules completed** | *W3-PM1-2* |

---

## Overview

| Module  | Title | Tools Used |
|---|----|----|
| W3-PM1  | *Password Cracking with JTR* | *John the Ripper (Jumbo) & Johnny GUI* |
| W3-PM2  | *Password Cracking with Networkwalks Tools*   | *Hash Calculator & Password Cracker*    |


---

## Disclaimer

All activities documented in this report were performed strictly within the **authorized scope of the Networkwalks Cybersecurity Internship (Batch B083D)** and against lab-provided files only.

These activities were carried out for **educational and research purposes**. Password cracking against systems or files without proper authorization can be illegal and unethical.

---

## Module 1: John the Ripper & Johnny GUI

### Workflow

Download *John the Ripper* and *Johnny GUI* from [`openwall.com`](https://www.openwall.com/john/) install directly using `sudo apt install john` & `sudo apt install johnny`.

1. You could extract the `$pdf$` hash from the locked PDF using the following options:
    - [OnlineHashCrack](http://onlinehashcrack.com/) 
    - [NetworkWalks/hash-calculator](https://networkwalks.com/hash-calculator/) 
2. Save the hash to `hash1.txt`, must start with `$pdf$`.
3. Open Johnny > `Open password file` > select `hash1.txt`.
4. Click `Start new attack`: Johnny uses a built-in wordlist by default.
5. Once cracked, open the PDF and enter the recovered password.

---

### Command-Line Equivalent

1. Extract hash and save to `hash1.txt`:
    - `pdf2john.pl My-Locked-PDF1.pdf > hash1.txt`

2. Cracking the password:
    - `john --wordlist=/usr/share/wordlists/john.lst hash1.txt`
    - *NOTE:* If the the wordlist doesn't work you could specify any other wordlist in the `.txt` format.

3. Show Result:
    - `john --show --format=PDF hash1.txt`

---

### Results

| PDF File | Password | Flag Captured
|------|-------|---|
| `My-Locked-PDF1`  | `good-luck`| `nw{cybersecurity_flag_captured_2608}`
| `My-Locked-PDF2`  | `password1`| `nw{networkwalks_persistence_jtr_270521}`
| `My-Locked-PDF3`  | `1qaz2wsx` | `nw{networkwalks_flag_260821_1}`

---

## Module 2: Networkwalks Browser Tools

### Workflow

1. Open [NetworkWalks/hash-calculator](https://networkwalks.com/hash-calculator/)
2. Upload the locked PDF > the tool extracts the `$pdf$` hash locally in your browser.
3. Copy the full `$pdf$` hash.
4. Open [NetworkWalks/password-cracker](https://networkwalks.com/password-cracker/)
5. Paste the hash > click `Start Cracking`.
    - If the password is not found you upload a custom wordlist in `.txt` format.
6. The tool reports the password, open the PDF and enter it.
7. Verify the results, if you have completed module 1.


---

## Evidence Collected

All screenshots referenced in this report are included in this repository:

**Module 1**

Johnny GUI

![PM1_Johnny_GUI](<Module 1/0_Johnny_GUI.png>)

![PM1_Johnny_John_patj](<Module 1/1_Johnny_GUI_John_path.png>)

---

*File 1*

![PM1_Hash_Extraction](<Module 1/2_Hash_Extraction.JPG>)

![PM1_Saving_hash_to_hash1](<Module 1/3_Saving_hash_to_hash1.txt.png>)

![PM1_Johnny_Results](<Module 1/4_Johnny_Results.png>)

![PM1_Verify_the_results](<Module 1/5_Verify_the_results.png>)

*Using JTR Jumbo:*

![PM1_CMD_Hash_Extraction](<Module 1/6_CMD_Hash_Extraction.png>)

![PM1_CMD_Password_Cracking](<Module 1/7_CMD_Password_Cracking.png>)

---

*File 2:*

![PM1_locked_pdf_2](<Module 1/8_locked_pdf_2.png>)

![PM1_verify_locked_pdf_2_result](<Module 1/9_verify_locked_pdf_2_result.png>)

---

*File 3:*

![PM1_locked_pdf_3](<Module 1/10_locked_pdf_3.png>)

![PM1_verify_locked_pdf_3_result](<Module 1/11_verify_locked_pdf_3_result.png>)

---

**Module 2**

*File 1:*

![PM2_Hash_Exctraction_PDF_File_1](<Module 2/0_HE_locked_pdf_1.JPG>)

![PM2_Password_Cracking_PDF_File_1_Failed](<Module 2/1_PC_locked_pdf_1_Failed.JPG>)

*Retrying with a different wordlist*

![PM2_Password_Cracking_PDF_File_1_Passed](<Module 2/2_PC_locked_pdf_1_Passed.JPG>)

*Passed! Result > `good-luck`, Verified!*

---

*File 2:*

![PM2_Password_Cracking_PDF_File_2_Passed](<Module 2/3_PC_locked_pdf_2_Passed.JPG>)

*Results: `password1`, Verified!*

---

*File 3:*

![PM2_Password_Cracking_PDF_File_3_Passed](<Module 2/4_PC_locked_pdf_3_Passed.JPG>)

*Results: `qaz2wsx`, Verified!*

---

## Key Takeaways

* **Weak and common passwords can be cracked within seconds** using dictionary attacks.
  `password1` and `1qaz2wsx` are good examples of passwords that can be found in common wordlists.

* **Both offline (Johnny/JTR) and online (Networkwalks) methods recovered the same passwords**, showing that the underlying weakness remains the same regardless of how the attack is carried out.

* **Two of the three lab PDFs used the same password and flag.** This shows how password reuse can increase the impact of a single successful crack across multiple files or systems.

* **Hash extraction is not the same as hashing.** PDF password protection uses encryption and hashing mechanisms. Tools such as `pdf2john` and the Networkwalks Hash Calculator extract and convert the PDF's encryption parameters into a crackable `$pdf$` format.

* **Strong and unique passwords are one of the simplest defenses against dictionary attacks.** Using a longer password with a mix of uppercase and lowercase letters, numbers, and symbols makes basic dictionary attacks much less effective.
