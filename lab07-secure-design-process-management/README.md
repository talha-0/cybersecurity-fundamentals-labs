# Lab 7: Secure design principles and Linux process management

## Goal

Match five case studies to the security design principle that fits each best, then complete auto-graded exercises on I/O redirection, pipes, `strace`, `cron` and process control (Mission 5).

## Tools and concepts

- Design principles: isolation, encapsulation, modularity, minimization of implementation, separation of privilege
- Redirection of stdout and stderr (`>`, `2>`), pipes, input redirection (`<`)
- `grep` with `wc -l`
- `strace` to see which files a program opens
- `crontab` with an every-minute schedule and absolute paths
- `ps` with VSZ and RSS columns and sorting, `top`, `kill -9`, `killall -r`
- Virtual versus resident memory

## What I did

Written part, my picks:

| Case | Principle |
| --- | --- |
| One service per container, so a compromise of one does not reach the other | Isolation |
| Kernel internals change while the system call interface stays the same | Encapsulation |
| Drivers loaded as kernel modules without changing the core kernel | Modularity |
| A container with a stripped-down kernel versus a full guest OS | Minimization of implementation |
| A launch that needs two officers acting independently | Separation of privilege |

Hands-on part (five exercises):

1. Ran a program and split its stdout and stderr into two separate log files, then counted matching lines in one of them with `grep` and `wc`.
2. Fed a long key from a file into a program that expected it on stdin.
3. Traced a program with `strace` and filtered the output to find the single text file it opened.
4. Scheduled a program with `crontab` to run once a minute. The grader watched for three minutes.
5. Started a background process and read its VSZ and RSS. Then, with a 20-second limit each: found and killed a process using more than 200 MB of physical memory, found and killed a process using more than 50% CPU, and killed ten processes sharing a name prefix with one `killall -r`.

## Result

Trainer log, final attempt per exercise:

| # | Exercise | Points | Seconds |
| --- | --- | --- | --- |
| 1 | Sail Log | 10/10 | 77 |
| 2 | Heart of Ocean | 10/10 | 84 |
| 3 | Jack's Innocence | 15/15 | 81 |
| 4 | Watchstander | 20/20 | 420 |
| 5 | Saving Titanic | 25/25 | 116 |

Total 80/80. Exercise 5 took a second attempt. On the first run I only finished the memory question and ran out the clock on all three timed kills.

The crontab line and the exact `ps` options I used are not in the log, so they are not reproduced here.
