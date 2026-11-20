# Lab 8: Linux networking

## Goal

Match five more case studies to design principles, then build a two-VM network (Mission 6): clone the course VM, give the clone a static address, set up SSH and SFTP between the two, publish a page through Apache on the clone, and run a DNS server with a small zone.

## Tools and concepts

- Design principles: fail-safe defaults, least privilege, layering, trust relationships, open design
- VirtualBox VM cloning and a host-only style second adapter
- `ifconfig`, MAC versus IPv4 addresses
- `netplan` static IPv4 configuration, routing, gateway conflicts
- `apt-get install openssh-server`, `ssh user@host`, `sftp` with `put`, `known_hosts`
- Apache 2 document root (`/var/www/html`), `wget`, `diff`
- BIND 9: `named.conf.local`, a zone file with A records, `nslookup` against a chosen server

## What I did

Written part, my picks:

| Case | Principle |
| --- | --- |
| Browsing limited to an allow-list of sites | Fail-safe defaults |
| A user who can change only their own course material | Least privilege |
| Directory login, locked BIOS and disk encryption on the same laptop | Layering |
| Session cookies accepted as proof of identity (which principle it breaks) | Trust relationships |
| A cipher whose design is kept secret (which principle it breaks) | Open design |

Hands-on part (four exercises):

1. Read the MAC and IPv4 address of the first adapter. Cloned the VM, named the clone "Vegas", and gave its second adapter a static link-local IPv4 address with `netplan`. Checked with `ping` from the main VM.
2. Installed and started the OpenSSH server on the main VM, then opened an SSH session from the clone as a different local user.
3. Installed OpenSSH on the clone, uploaded an HTML file to it with `sftp`, moved it into the Apache document root over `ssh`, made sure Apache was running, and confirmed with `wget` and `diff` from the main VM. The lab notes warn that `apt-get` fails on the clone until a netplan problem is fixed: two default routes conflict, and the gateway line on the link-local network has to be commented out so the VM can reach the internet. The log does not show this step, only that the exercise passed.
4. Installed BIND 9 on the clone, added a zone in `named.conf.local`, wrote the zone file with two A records (one name for each VM), and checked from the main VM with `nslookup <name> <dns-server-ip>`. BIND was not covered in class. I worked from a public tutorial.

## Result

Trainer log, final attempt per exercise:

| # | Exercise | Points | Seconds |
| --- | --- | --- | --- |
| 1 | Rise of New Empire | 30/30 | 265 |
| 2 | Frequent Flyer | 15/15 | 19 |
| 3 | Papa in Danger | 15/15 | 288 |
| 4 | Senator Corleone | 20/20 | 526 |

Total 80/80. Exercise 2 took a second attempt because the first one finished over the time limit. In exercise 4 the first check failed because the DNS server was not answering yet. The second check passed.

The netplan file, `named.conf.local` entry and zone file I wrote live on the VMs and were not part of the submission, so they are not in this repository.
