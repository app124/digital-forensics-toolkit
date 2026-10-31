# Digital Forensics Toolkit: Insider Data Theft Investigation

A simulated insider data theft case investigated with Volatility 3, FTK Imager, Autopsy and The Sleuth Kit on Kali Linux.

## Scenario
An employee of a fictional company, TechNova, copies three confidential files to a USB drive and then deletes them to hide the theft. The goal is to preserve the evidence, recover the deleted files and prove the evidence was not changed.

## Tools Used
- Kali Linux (VirtualBox)
- FTK Imager (RAM capture on Windows)
- Volatility 3 (RAM analysis)
- Autopsy and The Sleuth Kit: fsstat, fls, icat (disk analysis)
- dd and sha256sum (imaging and integrity check)

## Steps Performed
1. Installed Autopsy, Sleuth Kit, dosfstools and Volatility 3 on Kali.
2. Simulated a USB drive (FAT16, label TECHNOVA) and added 3 confidential files: Salary_Sheet.txt, Client_List.txt, Project_Phoenix.txt.
3. Deleted the files and unmounted the drive, as an insider would.
4. Captured the Windows RAM with FTK Imager and hashed it with SHA256.
5. Made a forensic copy of the USB with `dd`.
6. Verified the original and the copy have the same SHA256 hash, so the evidence is intact.
7. Ran `fsstat` and `fls` and found all 3 deleted files.
8. Recovered the files with `icat` and hashed them.
9. Opened the image in Autopsy, where the deleted files show in red, and ran a keyword search for "CONFIDENTIAL" (3 hits).
10. Analysed the RAM dump with Volatility 3 (pslist, cmdline, netscan).

## Key Findings
- 3 deleted confidential files were fully recovered.
- The original and the evidence copy have the same SHA256 hash: `a4a262aa3bcba4a3d289ce7403501b5c5a752feccefbda2a6935daf463c26c8e`
- Autopsy keyword search found "CONFIDENTIAL" in sectors 440, 444 and 448.
- Volatility 3 listed the running processes, including cmd.exe, and the command lines from memory.

## Evidence
All screenshots are in [Digital_pics.pdf](Digital_pics.pdf).

## Conclusion
Deleting a file does not erase its data. Using hashing to preserve the evidence and forensic tools to recover it, the stolen files were fully recovered.

*All data in this project is fictional and created in a lab for learning.*
