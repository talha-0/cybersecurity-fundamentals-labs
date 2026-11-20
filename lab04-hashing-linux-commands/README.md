# Lab 4: Hashing and more Linux commands

## Goal

Short written answers on hash functions, then a timed, auto-graded set of exercises on checksums, SUID/SGID bits and text and search tools (Mission 2).

## Tools and concepts

- Hash properties: collision resistance, preimage resistance, the birthday bound
- `md5sum`
- `chmod` with SUID and SGID bits, `chown`
- `wc -l`, `which`, `file`, `xxd`
- `echo` and `cat` with `>` and `>>`, `sed` substitution and `sed -i` line insert
- `grep -R`, `find` by size, permission and name
- `find -exec ... {} \;` versus `{} \+`

## What I did

Written part:

- A checksum published on the same server as the download does not protect against an attacker who controls that server, because they can replace both. This was in the context of the 2016 Linux Mint website compromise.
- Collision resistance is about finding any two inputs with the same hash. Preimage resistance is about finding an input for a given hash.
- Generic birthday attack on a 160-bit hash such as SHA-1: about 2^80 attempts, the square root of 2^160.

Hands-on part (six exercises):

1. Compare MD5 sums of four text files against a list to find the one that was altered.
2. Set permission patterns that include SUID and SGID on a root-owned script.
3. Count users and groups from `/etc/passwd` and `/etc/group`, locate a command with `which`, identify the one binary executable in a directory with `file`, and read its first byte with `xxd` (`7f`, the start of the ELF magic number).
4. Create a file with `echo`, concatenate three Python files with `cat`, rename an identifier with `sed`, and insert a header line with `sed`.
5. Search a directory tree under a time limit: `grep` for a keyword, `find` a file over 100 kB, `find` a file that everyone can execute, `find` a file by name pattern.
6. Use `find -exec` with `sed` to add a header to every `.cpp` file, with `rm` to remove all executable regular files, and with `wc -l` to total the lines of all `.py` files.

As in Lab 3, the log records the grader's side and my answers, not the commands I typed.

## Result

Trainer log, final attempt per exercise:

| # | Exercise | Points | Seconds |
| --- | --- | --- | --- |
| 1 | Checksum | 10/10 | 83 |
| 2 | Set SUID | 15/15 | 131 |
| 3 | File Info | 10/10 | 263 |
| 4 | Sed, Echo and Cat | 10/10 | 161 |
| 5 | Mission Impossible | 15/15 | 237 |
| 6 | Chain of Cmds | 20/20 | 194 |

Total 80/80. Exercises 1 and 2 took a second attempt. My first checksum answer was the right sentence with its first letter missing, and that exercise allows one try per run. On the first SUID pass I got 3 of 5 patterns.
