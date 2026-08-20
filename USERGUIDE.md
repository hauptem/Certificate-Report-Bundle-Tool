# Certificate Report/Bundle Creator User Guide

Open `Certificate Report Bundle Creator.html` in a browser. Three sections: Verify, Import, Report. They work independently.

## Verify

Drop the signature file, the CA chain (if provided), and the bundle files. Any order, multiple drops. Clear resets the panel.

Results, in order: signer, signature validity, chain path, root fingerprints, then per-file hash comparison with both values shown. The root fingerprint lines are informational; compare them against the authority's published value to close the loop. A file matched by content under a different name is reported as such; the hash is the binding, not the filename.

Red stops the pipeline: invalid signature, altered content, broken chain link, hash mismatch. Amber is degraded: incomplete chain (drop the chain file) or an expired chain cert.

Detached signatures work; drop the manifest content file alongside the signature.

## Import

Set Category, Version, and Release Date, then drop files. The fields label the report rows for that drop; certificates are never modified. Blank Category/Version auto-fill from `certificates_pkcs7_v#_#_group` filenames; typed values win. Parse failures are listed by name without blocking the batch.

.p7b bundles expand to one row per certificate, named by subject CN.

## Report

Columns: Category, Name, Version, Release, Organization, Issuer CN, Not Before, Expiration, Serial, Key, Signature Alg, Thumbprint (SHA-1), OCSP, CRL, Type. Expired rows flag red. Sort by name or expiration.

Search highlights matching rows without filtering and covers every column. Paste a thumbprint or serial to confirm an exact cert is present.

Checkboxes select rows. Exports cover the selection, or everything when nothing is selected:

- **CSV** - all columns plus SHA-256 thumbprint
- **PEM bundle** - openssl print_certs style; works directly as a CAfile
- **P7B bundle** - DER PKCS#7, same structure as `openssl crl2pkcs7`
- One cert in scope relabels the buttons to **.pem** / **.cer** and exports a single file named after the cert

Byte-identical duplicates across imports are dropped from exports automatically.

## Troubleshooting

- **Signature file ignored** - rename it to a recognized extension (`.sha256` `.p7s` etc.). The signature covers content, not the filename
- **"Detached signature: none of the provided files match"** - drop the manifest content file. Line-ending changes are handled; altered content is not
- **"Signer certificate not found"** - the signature does not embed the signer cert. Drop the publisher's chain file
- **"Chain incomplete"** - drop the missing issuer. Certs in any dropped file join the chain pool
- **File "skipped (not in manifest)"** - matches no manifest entry by name or content. Normal for chain files and READMEs; suspicious for a bundle file you expected to verify
- **Folder drop does nothing** - browsers block it for file:// pages. Select the files instead
- **Fewer rows than expected** - parse failures are listed above the table with reasons
