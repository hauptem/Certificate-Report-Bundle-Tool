# Certificate Report/Bundle Tool - User Guide

Open `Certificate Report Bundle Tool.html` in a browser. 

## Verify

Drop the signature file, the CA chain (if provided), and the bundle files. Any order, multiple drops. Clear resets the panel.

Detached signatures work; drop the manifest content file alongside the signature.

## Import

Set Category, Version, and Release Date if desired for reporting, then drop files. The fields label the report rows for that drop. 

## Report

Columns: Category, Name, Version, Release, Organization, Issuer CN, Not Before, Expiration, Serial, Key, Signature Alg, Thumbprint (SHA-1), OCSP, CRL, Type. 

Search highlights matching rows and covers every column. Paste a thumbprint or serial to confirm an exact cert is present.

Checkboxes select rows. Exports cover the selection, or everything when nothing is selected:

- **CSV** - all columns plus SHA-256 thumbprint
- **PEM bundle** - openssl print_certs style; works directly as a CAfile
- **P7B bundle** - DER PKCS#7, same structure as `openssl crl2pkcs7`

Byte-identical duplicates across imports are dropped from exports automatically.
