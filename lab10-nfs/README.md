# Lab 10: NFS with LDAP users

## Goal

Two short written answers on access control and session management, then extend the Lab 9 setup (Mission 8): LDAP login on both VMs, an NFS server exporting home directories from the second VM, NFS clients on both VMs through `/etc/fstab`, and LDAP home directories pointing at the NFS mount.

## Tools and concepts

- MAC versus DAC, security labels
- Session IDs in cookies versus URL parameters, hidden fields or header tokens; `HttpOnly` and `Secure` flags
- `libnss-ldap` and PAM on a second machine, `openssh-server`
- `nfs-kernel-server`, `/etc/exports` with read-write access for a /24 network, `systemctl restart nfs-kernel-server`
- `mkdir`, `chown`, `chmod` for per-user home directories
- `/etc/fstab` NFS entries, `mount -a`, `mount`
- `ldapmodifyuser` to change the `homeDirectory` attribute
- VirtualBox snapshots before risky changes

## What I did

Written part:

- MAC fits military or classified systems better than DAC. Access follows labels set centrally, so a user cannot pass data on at their own discretion.
- Sessions can be kept without cookies by carrying the session ID in the URL, a hidden form field or a request header. That works for APIs and cookie-less clients, but IDs in URLs leak through logs and history. Cookies are easier to manage and can be restricted with flags.

Hands-on part (five exercises):

1. Repeated the LDAP client setup from Lab 9 on the main VM, so the LDAP users could log in there over SSH.
2. Installed the NFS server on the second VM, created the export directory, and added it to `/etc/exports` with read and write access for the lab subnet.
3. Created one home directory per LDAP user under the export, each owned by its user and closed to the other, with a small text file in each. The grader logged in as each user over SSH and checked that each could read their own file and not the other's.
4. Mounted the export on both VMs at the same mount point with `/etc/fstab` and `mount -a`. The grader then wrote a file as each user through the mount.
5. Changed each user's `homeDirectory` in LDAP to the path under the NFS mount with `ldapmodifyuser`, so that `cd` after login lands in the NFS home on either VM.

## Result

Trainer log, final attempt per exercise:

| # | Exercise | Points | Seconds |
| --- | --- | --- | --- |
| 1 | Single Sign On | 15/15 | 3 |
| 2 | NFS Server | 15/15 | 139 |
| 3 | Home | 15/15 | 318 |
| 4 | NFS Client | 20/20 | 8 |
| 5 | The Arts of Google | 15/15 | 2 |

Total 80/80. The very short times on 1, 4 and 5 are re-runs after the setup was already in place. The first passes took 739, 509 and 460 seconds and lost points for time. Exercise 4 also had a failed run before that: the mount was missing from the `mount` output and a write as an LDAP user failed because the path under the mount point did not exist yet. In exercise 5 the home directory was still the old path on the first two checks.

The `/etc/exports` and `/etc/fstab` lines I wrote are not in the log in full, so they are not reproduced here.
