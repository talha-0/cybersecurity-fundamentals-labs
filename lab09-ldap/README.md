# Lab 9: LDAP and single sign-on

## Goal

Two short written answers on cybersecurity across computing environments, then set up an OpenLDAP directory on the second VM, add groups and users, and make Linux logins authenticate against it (Mission 7). Part of the mission is debugging a client misconfiguration with `strace`.

## Tools and concepts

- OpenLDAP server `slapd`, `dpkg-reconfigure slapd`, base DN from a DNS domain (`dc=...,dc=...`)
- LDIF files and `ldapadd`, `ldapsearch -x -h <host> -b <base>`
- `ldapscripts`: `ldapscripts.conf` (SUFFIX, GSUFFIX, USUFFIX, BINDDN), `ldapaddgroup`, `ldapadduser`, group membership, setting passwords
- `libnss-ldap`, NSS, PAM, `auth-client-config`, `pam-auth-update`
- `strace` on `su` and on `ldapsearch`, socket families `AF_INET` and `AF_UNIX`
- `ldap://` versus `ldapi://` versus `ldaps://`
- `xxd`, `ls -l`, `lsof -i`, `ping`, `nslookup`, `route -n`

## What I did

Written part:

- Threats differ by environment: ransomware and insiders in enterprises, misconfiguration and data leaks in cloud systems, weak authentication on IoT devices, and physical disruption in industrial systems.
- Cyber defense in the US is shared between federal agencies (CISA, FBI), state and local government, and industry, through information sharing groups (ISACs), joint response, and frameworks such as NIST's.

Hands-on part (three exercises):

1. Checked that both VMs, DNS names and internet access from Lab 8 still worked. Installed `slapd` on the second VM and reconfigured it for the lab's domain with an MDB database.
2. Wrote an LDIF file with the two base entries (`People` and `Groups`) and imported it with `ldapadd`. Installed `ldapscripts` and edited its config for the lab's suffix and bind DN. Then worked through a planted failure: after typing the bind password into the password file with VIM, `ldapaddgroup` failed with LDAP error 49 (invalid credentials). `ls -l` showed the file was one byte longer than the password and `xxd` showed a trailing `0x0a`. VIM had added a newline. Rewriting the file with `echo -n` fixed it. After that I created two groups and two users and put each user in the right group.
3. Installed `libnss-ldap` on the second VM with the server URI the instructions gave, which was wrong on purpose. `su <ldap-user>` reported no passwd entry. `strace su ...` showed that the lookup read `/etc/passwd` and then tried to connect to the server and got -1. `strace` on a working `ldapsearch` showed an `AF_INET` socket, while the failing lookup used `AF_UNIX`. The cause was the `ldapi://` scheme, which means a local Unix socket and cannot reach another host. I changed the URI to `ldap://` with `dpkg-reconfigure`, and SSH login as an LDAP user then worked.

## Result

Trainer log, final attempt per exercise:

| # | Exercise | Points | Seconds |
| --- | --- | --- | --- |
| 1 | Vegas Headquarter | 20/20 | 360 |
| 2 | Corleone Family | 30/30 | 421 |
| 3 | SSO | 30/30 | 110 |

Total 80/80. Exercise 3 took a second attempt because the first one finished over the time limit and lost 20%. Within the diagnosis questions I got one multiple-choice answer wrong on the first try: I said the working connection succeeded because of root privilege, when the real difference was the socket type.

The LDIF file and the edited config files stayed on the VM and were not submitted, so they are not in this repository.
