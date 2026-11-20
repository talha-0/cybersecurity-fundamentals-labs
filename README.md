# Cybersecurity Fundamentals Labs

Lab write-ups from CSC 210, Fundamentals of Cybersecurity, at Hofstra University, Spring 2026. I took the course as part of my master's in computer science.

There were eleven labs. Most had a short written part and a hands-on part done in a Linux virtual machine. Each folder has a README that says what the lab asked for, what I used, what I did and how it went, including the parts that took more than one try.

## Labs

| # | Folder | Topic | Skills |
| --- | --- | --- | --- |
| 1 | [lab01-vm-and-vim](lab01-vm-and-vim/) | VM setup and VIM basics | VirtualBox import, snapshots and tuning; VIM movement and basic editing |
| 2 | [lab02-advanced-vim-openra](lab02-advanced-vim-openra/) | Advanced VIM, OpenRA build | VIM substitution, ranges and split windows; reading compiler errors; `sed`, `make` |
| 3 | [lab03-security-models-file-permissions](lab03-security-models-file-permissions/) | Security models, file permissions | Bell-LaPadula; `mkdir`, `cp`, `mv`, `rm`, `chmod`, reading `ls -l` |
| 4 | [lab04-hashing-linux-commands](lab04-hashing-linux-commands/) | Hashing, more Linux commands | `md5sum`, SUID/SGID bits, `sed`, `grep`, `find -exec`, `xxd`, `file` |
| 5 | [lab05-symmetric-crypto-suid](lab05-symmetric-crypto-suid/) | Symmetric crypto, SUID project | `base64`, `openssl` AES-256-CBC, `useradd`, SUID/SGID permission design |
| 6 | [lab06-pki](lab06-pki/) | PKI | RSA decryption, CSR, signing as a CA with `openssl`, Apache HTTPS deployment |
| 7 | [lab07-secure-design-process-management](lab07-secure-design-process-management/) | Secure design, process management | Design principles; redirection, pipes, `strace`, `crontab`, `ps`, `kill`, `killall` |
| 8 | [lab08-linux-networking](lab08-linux-networking/) | Linux networking | `netplan` static IP, `ssh`, `sftp`, Apache, BIND 9 zone, `nslookup` |
| 9 | [lab09-ldap](lab09-ldap/) | LDAP | OpenLDAP `slapd`, LDIF, `ldapscripts`, NSS/PAM login, debugging with `strace` |
| 10 | [lab10-nfs](lab10-nfs/) | NFS | `nfs-kernel-server`, `/etc/exports`, `/etc/fstab`, LDAP home directories on NFS |
| 11 | [lab11-dvwa-patching](lab11-dvwa-patching/) | Patching DVWA | SQL injection and command injection in PHP, with patches |

## Lab environment

- Oracle VirtualBox on my laptop.
- A course-provided 32-bit Ubuntu 18.04 image with a lightweight desktop. Labs 8 to 10 used a second VM cloned from it, joined to the first over a private link-local network.
- Labs 3 to 10 were graded by a trainer program from the instructor. It runs in one terminal, sets up a scenario, and checks the state of the system or asks for an answer. The work is done in a second terminal. It times each exercise, deducts points for going over, and allows retries.
- Lab 11 used Damn Vulnerable Web Application v1.10 served by Apache on the same VM.

## What is and is not here

- The READMEs are summaries written from my submitted reports and the trainer logs.
- The score tables come from the trainer logs. They show the final attempt for each exercise. The notes under each table say where earlier attempts failed or ran over time.
- The trainer logs record the grader's checks and my typed answers, not the shell commands I ran in the other terminal. Where a README names a command, it is one the exercise called for. Config files I edited on the VMs were not part of the submissions and are not here.
- The original reports, screenshots, trainer logs, the trainer programs and the course VM are not in this repository. The assignment text belongs to the instructor.
- The only code is in `lab11-dvwa-patching/patches/`. Those are my changes to DVWA source files, shown as small diffs. DVWA itself is a separate open source project.
