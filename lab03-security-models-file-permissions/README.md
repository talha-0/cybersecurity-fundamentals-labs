# Lab 3: Security models and Linux file permissions

## Goal

Two written answers on the Bell-LaPadula model, then a timed, auto-graded set of Linux file system exercises (the course calls it Mission 1).

## Tools and concepts

- Bell-LaPadula: no read up, no write down, tranquility, trusted subjects
- Mandatory access control, reference monitor, trusted computing base
- `mkdir -p`, `ls -l`, `cd` with relative paths, `rm`, `rm -r`, wildcards, `cp -r`, `mv`, `chmod`
- Reading owner, group and `rwx` bits from a listing

## What I did

Written part:

- Limits of Bell-LaPadula: it covers confidentiality only and says nothing about integrity, it assumes labels do not change, it does not model creating or deleting subjects and objects, and declassification needs trusted subjects that the model does not define.
- How I would enforce it in Linux: security labels on files and processes, the two rules checked in the kernel, and a small reference monitor that sees every access.

Hands-on part (eight exercises):

1. Create nested directories in one command.
2. Read the owner, group and owner permissions of a file from `ls -l`.
3. Move between sibling and parent directories with one `cd` each.
4. Delete a file, a whole directory, and all `.o` files with a wildcard.
5. Copy a single file over another, copy a directory tree, copy and rename a tree.
6. The same three cases with `mv`.
7. Set five different permission patterns on a file with `chmod`.
8. Fix the permission bits on a shell script so it runs, then read its output.

The grader ran in one terminal and I worked in a second one, so the log has the grader's checks and my typed answers but not the commands themselves.

## Result

Trainer log, final attempt per exercise:

| # | Exercise | Points | Seconds |
| --- | --- | --- | --- |
| 1 | Create Dir | 5/5 | 43 |
| 2 | Simple List | 5/5 | 50 |
| 3 | Dir Navigation | 10/10 | 159 |
| 4 | Kill Files | 10/10 | 101 |
| 5 | Make Copies | 15/15 | 193 |
| 6 | Move Files | 10/10 | 150 |
| 7 | Set Permissions | 15/15 | 233 |
| 8 | Run Shell Script | 10/10 | 24 |

Total 80/80. Exercises 2, 4, 5 and 8 took a second attempt. On the first pass I lost points for time on two of them and failed parts of the delete and copy exercises.
