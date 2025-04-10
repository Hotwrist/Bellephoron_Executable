# Bellephoron_Executable
This program, Bellephoron, scans ELF (Executable and Linkable Format) files and checks for hidden or non-standard sections that may indicate the presence of a userland rootkit (hidden sections), RELRO not enabled or NX bit not set.

---

## **Table of Contents**
- [Overview](#overview)
- [Features](#features)
- [Usage](#usage)
- [License](#license)

---

## **Overview**

Rootkits are malicious software designed to gain unauthorized access to a computer system, often while hiding their presence. A **userland rootkit** runs in user space (rather than kernel space) and can manipulate processes, files, and network traffic to achieve persistent access. 

This **Bellephoron** is a tool that scans for signs of such rootkits by analyzing the system for suspicious behavior, hidden processes, files, and modules. It's designed to help security professionals, system administrators, and researchers detect potential userland rootkits on compromised Linux system ELF binaries.

---

## **Features**
- **Hidden ELF Binary Section Detection**: Scans Linux ELF binaries for hidden or non-standard ELF sections, which is a common technique used by userland rootkits to hide their presence by manipulating ELF file structures. This detection helps identify suspicious modifications or hidden sections within ELF binaries that could indicate the presence of a rootkit.
- **File Integrity Check**: Generate hashes of malicious ELF binaries found, for logging or future checks.
- **Logging**: Generates detailed logs for further analysis of detected anomalies.

---

## **Usage**

### Running Bellephoron
To run the rootkit scanner (Bellephoron), simply execute the script with the following command:

```bash
./bellephoron
```

This will start the scan for userland rootkits and ELF binaries that don't have RELRO or NX bit enabled. The script will log any findings to a log file (bellerophon_scan_report.log)

### Command-Line Options:
By default, running Bellephoron without any commandline argument will scan the directories: "/bin", "/sbin", "/usr/bin", "/usr/sbin". If you have a specific directory containing Linux ELF binaries to scan, put them in a text file and pass it to Bellephoron. The directories should be entered one per line e.g let's say this is the content of dir.txt:
/home/kali/Documents
/bin
/etc

- `./bellephoron dir.txt`: Scan the Linux ELF binaries in the file: dir.txt.

Example:
```bash
./bellephoron dir.txt
```

### Example Output:
```
===== ELF Security Scan Report =====
[!] Hidden section detected (Possible Rootkit!): .chimera
[+] Section Header Number: [31]
[+] SHA-256 (/home/kali/LIBELF/LIBELF_PROJS/ls): f38ca21a964a92d0b6233ae2cbb2e8f7d64e49f4a535b347653fde4b5a06cb34
```

---

## **License**

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
