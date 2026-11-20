# Lab 5: Symmetric crypto and an SUID integrated project

## Goal

Written answers on Base64 versus AES and on linear cryptanalysis, then an auto-graded project (Mission 3) built around a small local mail program supplied by the instructor. The project combines Base64, AES decryption with `openssl`, user management and SUID/SGID permission design.

## Tools and concepts

- `base64` and `base64 -d`
- `openssl` AES-256-CBC decryption with a passphrase (`-pass pass:...`)
- `cp`, `chmod`, `chown`, SUID and SGID
- `useradd`, `passwd`, `su`
- Output redirection, trimming a dump in VIM
- Least privilege for a shared program that writes to per-user files

## What I did

Written part:

- Base64 is an encoding. It has no key and anyone can reverse it. AES is encryption and needs the secret key to reverse.
- Linear cryptanalysis is a known-plaintext attack. It uses linear relations between plaintext, ciphertext and key bits that hold with probability slightly off 1/2, and many plaintext/ciphertext pairs, to recover key bits.

Hands-on part (four exercises):

1. Install the mail program into `/usr/bin` with the right execute bits, read a message with it, send a message with it.
2. Base64-encode a word without a trailing newline (`echo -n`), decode a file, then recover a PNG that arrived as Base64 text in a mail: dump the mailbox to a file, cut everything except the Base64 block, decode it to a `.png`, open it.
3. Decrypt an AES-256-CBC file with `openssl` and a passphrase, then do the same for a mail that was encrypted and then Base64-encoded (decode first, then decrypt).
4. Make the mail program work for two users while keeping each mailbox private. The mailbox must be readable and writable only by its owner and by the mail program. The approach is a dedicated account that owns the program, SUID or SGID on the binary so it runs with that account's rights, and owner, group and mode on each mailbox set to match. Each run also needs a new user created with `useradd` and `passwd`, with a `ygm/` folder and an empty `mailbox` file in its home directory.

## Result

Trainer log, final attempt per exercise:

| # | Exercise | Points | Seconds |
| --- | --- | --- | --- |
| 1 | You've Gotta Mail | 15/15 | 261 |
| 2 | Base64 and Media | 20/20 | 192 |
| 3 | Symmetric Crypto | 15/15 | 261 |
| 4 | Permission Config | 30/30 | 57 |

Total 80/80.

Exercise 4 was the hard one. The log shows six failed runs before the one that passed. In most of them mail sent between the two users did not show up in the recipient's mailbox, and in one the other user could read a mailbox directly. The grader picks a new random user name on each run, so each retry meant building the user, folder and mailbox again. The final run passed in 57 seconds because by then I had the sequence worked out.

The log does not record whether I ended on SUID or SGID, or the exact owner, group and mode values, so they are not listed here.

## Not included

The mail program and the mission files are the instructor's and are not in this repository.
