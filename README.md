# Week 3 — Linux System Auditing

## 📌 Overview

This project documents a practical Linux system auditing exercise performed in a controlled WSL2 Ubuntu environment.

The objective was to inspect privilege configuration, sudo access, SUID binaries, and sudoers file permissions to identify potential security risks and understand Linux privilege management.

---

## 🎯 Objectives

- Audit Linux sudo configuration
- Review user sudo privileges
- Identify SUID-enabled binaries
- Check permissions of sudoers configuration files
- Document security findings with evidence
- Practice basic Linux security auditing techniques

---

## 🖥️ Environment

| Component | Details |
|---|---|
| Operating System | Ubuntu 26.04.1 LTS |
| Environment | WSL2 |
| Kernel | Linux 6.18.33.2-microsoft-standard-WSL2 |
| User | injma |
| Shell | Bash |
| Host System | Windows 11 |

---

## 🔐 1. Sudo Configuration Audit

The sudo configuration was reviewed to understand how administrative privileges are assigned.

The configuration was validated using:

```bash
sudo visudo -c

The configuration was successfully parsed, indicating that the sudoers configuration syntax was valid.
Evidence

👤 2. Sudo Privilege Audit
The current user's sudo privileges were examined using:
sudo -l

The audit confirmed that the injma user has administrative sudo privileges in the test environment.
Evidence

⚙️ 3. SUID Binary Audit
SUID-enabled executables were identified using:
sudo find /usr/bin /sbin /lib -type f -perm -4000 -ls 2>/dev/null

SUID binaries allow an executable to run with the permissions of its file owner, which is commonly root.

The audit identified several SUID-enabled binaries, including standard Linux utilities such as:
- sudo
- su
- passwd
- mount
- umount
- chsh
- chfn
- gpasswd
- fusermount3
SUID binaries should be reviewed regularly because improperly configured or vulnerable SUID programs can potentially lead to privilege escalation.
Evidence

🛡️ 4. Sudoers Permission Audit
The /etc/sudoers.d/ directory and its files were inspected to verify ownership and permissions.

The audit also checked for world-writable files using:
sudo find /etc/sudoers.d -type f -perm /o+w -ls

No world-writable sudoers files were identified.

This is an important security check because unauthorized modification of sudoers configuration could allow privilege escalation.
Evidence

📊 Findings Summary
Audit Area	Result
Sudoers Syntax	Valid
User Sudo Access	Administrative access available
SUID Binaries	Multiple SUID binaries identified
World-Writable Sudoers Files	None identified
Configuration Ownership	Root-owned configuration observed


🧠 Key Learnings
Through this practical audit, the following Linux security concepts were explored:
- Linux privilege management
- Sudo and sudoers configuration
- SUID permissions
- File ownership and permissions
- Privilege escalation risks
- Basic system security auditing
- Evidence collection and documentation
📁 Project Structure
week-3-linux-system-auditing/
│
├── findings/
├── logs/
├── screenshots/
│   ├── 01-sudo-configuration.png
│   ├── 02-sudo-privilege-audit.png
│   ├── 03-suid-binaries-audit.png
│   └── 04-sudoers-permission-audit.png
│
├── scripts/
└── README.md

⚠️ Ethical Scope
All auditing activities were performed in a controlled personal WSL2 environment for educational and cybersecurity learning purposes.

No unauthorized systems, networks, or devices were targeted.
👨‍💻 Author
Injmam Ansari

Cybersecurity Intern
BCA Student


