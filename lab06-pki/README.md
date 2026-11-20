# Lab 6: PKI and Apache HTTPS

## Goal

Replace a wrong TLS certificate on a local Apache site (Mission 4): decrypt an RSA message, inspect the current certificate, write a certificate signing request, sign it as a small certificate authority, and deploy the new key and certificate. A short written part covers the cost of factoring RSA moduli.

## Tools and concepts

- `openssl rsautl` for RSA decryption with a private key
- `openssl s_client -connect localhost:443` to read a live certificate
- `openssl req` to build a CSR from an existing key pair, and to check it with `-text -noout`
- `openssl x509` to sign a CSR with a CA key and CA certificate
- Apache 2: `sites-enabled` SSL virtual host, `SSLCertificateFile`, `service apache2 restart`, `error.log`
- `grep` across `/etc/apache2`
- Quadratic sieve and its running time

## What I did

Hands-on part (four exercises):

1. Decrypted a message that had been encrypted with a public key, using the matching private key in PEM format.
2. Read the Organization field of the certificate the site was serving, then generated a CSR for the existing key pair with the required subject fields (country, state, locality, organization, unit, common name `localhost`, email).
3. Acting as the CA, signed the CSR with the CA private key and CA certificate to produce the site certificate.
4. Found which Apache config file sets the certificate and key paths for port 443 (`/etc/apache2/sites-enabled/000-default-ssl.conf`), copied the site key and new certificate to the paths that file expects, restarted Apache, and checked that the served certificate now carried the new Organization name.

Written part:

- The quadratic sieve factors n by finding x and y with x^2 ≡ y^2 (mod n).
- Its running time is exp((1 + o(1)) * sqrt(ln n * ln ln n)), written L_n[1/2, 1].
- For a 2048-bit modulus: ln n ≈ 2048 × 0.693 ≈ 1419.6, ln ln n ≈ 7.26, sqrt(1419.6 × 7.26) ≈ 101.5, and e^101.5 ≈ 2^146. So the work is far below 2^2048, which is why a 2048-bit RSA key is rated well under its bit length. My figure is not the standard 112 bits. The question accepted any estimate under 160.

## Result

Trainer log, final attempt per exercise:

| # | Exercise | Points | Seconds |
| --- | --- | --- | --- |
| 1 | Jenny's Msg | 10/10 | 109 |
| 2 | Bubba-Gump Fish | 20/20 | 146 |
| 3 | Austin Power's CA | 30/30 | 40 |
| 4 | Deploy | 20/20 | 190 |

Total 80/80. Exercise 4 took a second attempt. The first run lasted 14 seconds and scored 0: empty answers to the config file question and three deploy checks against a site that still had the old certificate.

The log records the grader's checks, not the `openssl` command lines I typed, so those are not reproduced here. No keys or certificates from the lab are in this repository.
