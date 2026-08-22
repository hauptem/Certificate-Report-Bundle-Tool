# Certificate Report/Bundle Tool - User Guide

Open `Certificate Report Bundle Tool.html` in a modern browser.

The tool has three sections: Verify checks a signed release, Import reads certificates into the report, and Report displays and exports them.

## Verify

To verify a release, drop all of its files into the zone: the signature file, the chain file if there is one, and the bundle files. The tool checks the manifest signature, builds the signer's chain, and compares every file against the signed manifest. Problems are marked in red, warnings in amber, and each file row shows the manifest hash next to the computed one.

The tool never trusts the root certificate, since it came in the same download. It shows the root's fingerprints instead. Compare one of them against the value the issuing authority publishes, and the release is verified once that matches and everything else is clean.

Use the Import buttons in the results to send a verified file's certificates to the report without dropping it again.

Signature files are recognized by their extension (`.sha256`, `.sha384`, `.sha512`, `.p7s`, `.p7m`, `.sig`), and the manifest must be sha256sum, sha384sum, or sha512sum output. Attached and detached signatures both work, with RSA PKCS#1 v1.5, RSA-PSS, or ECDSA on P-256, P-384, or P-521.

## Import

Drop certificate files into the zone. DER, PEM, headerless Base64, and PKCS#7 bundles are all accepted, and bundles expand to one row per certificate. Certificates already in the report are skipped, so the same bundle in two encodings won't create duplicates.

Fill in Category, Version, or Release Date before dropping to label everything in that drop. Filenames like `certificates_pkcs7_v2_1_internal` fill Category and Version automatically when you leave them blank.

## Report

Each certificate is a row showing its subject, issuer, validity, serial, algorithms, thumbprint, revocation URLs, and type, with expired and not-yet-valid certificates flagged. Sort by clicking the Certificate Name or Expiration header, and use the search box to highlight matches anywhere in the table. Check rows to select them for export, or remove them individually with the button at the end of each row. Click a certificate's name to view its PEM in a popup with a Copy button, for pasting into anything that accepts PEM directly.

## Compare

Compare, in the title bar, diffs two certificate sets. Drop the baseline on the Reference side and the set you're evaluating on the Comparison side; differences appear as a table once both sides have certificates. Matching uses the full subject, so same-named certificates from different organizations aren't confused.

## Export

Exports cover the checked rows, or the whole report if nothing is checked, with duplicates removed. Use PEM for an openssl-style CA file, P7B for Windows and Java trust stores, .cer for a single certificate as DER, CSV for a spreadsheet copy of the report with SHA-256 thumbprints added, and HTML for a standalone copy of the report you can share, archive, or print.

## Notes

- The tool doesn't check revocation. The OCSP and CRL URLs in the report are for use with external tools
- Windows may block a downloaded .cer file. Right-click it, open Properties, and select Unblock

## Troubleshooting

- The signature file isn't recognized: rename it to one of the recognized extensions. The signature covers the file's content, so the name doesn't affect verification
- A detached signature reports that no files match: include the manifest file itself in the drop
- The signer certificate isn't found: drop the publisher's chain file. The signature file doesn't embed the signer's certificate
- The chain is incomplete: drop the missing issuer certificate. Certificates from every dropped file are used for chain building
- A file shows as skipped: nothing in the manifest matches it by name or content. This is normal for chain files and documentation
- Folder drag-and-drop doesn't work when the page is opened from disk: select the files inside the folder instead
- Fewer rows appear than expected: check the notices above the Import drop zone for files that failed to parse
