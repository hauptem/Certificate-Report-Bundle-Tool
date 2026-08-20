# Certificate Report/Bundle Tool

A single HTML file that inspects X.509 certificates, verifies signed bundle releases, and exports certificate bundles. Open `Certificate Report Bundle Tool.html` in a browser.

<img width="1937" height="918" alt="Image" src="https://github.com/user-attachments/assets/9aa4be28-b68d-4402-907e-db9293e147c1" />

## Capabilities

**Verify Bundle.** Checks a signed release before you trust it. The tool verifies the signature on the publisher's hash manifest, validates the signer's certificate chain to a self-signed root, and compares each bundle file's hash against the signed manifest. Both hash values are displayed for each file. The root's fingerprint is displayed for comparison against the issuing authority's published value. Attached and detached CMS signatures are supported, with RSA PKCS#1 v1.5, RSA-PSS, and ECDSA (P-256/P-384/P-521). Files renamed after download are matched to their manifest entries by content hash.

**Import Certificates.** Reads DER, PEM, headerless Base64, and PKCS#7 bundles, detected by content rather than extension. Bundles expand to one row per certificate, named by subject CN. Optional Category, Version, and Release Date fields populate the corresponding report columns for each drop.

**Report.** One row per certificate: subject, issuer, validity dates, serial number, key and signature algorithms, SHA-1 thumbprint, OCSP and CRL URLs, and certificate type. Expired certificates are flagged in red. The search box highlights matching rows across all columns, including serials and thumbprints. Checkboxes select rows for export.

**Exports.** Exports include the selected certificates, or all certificates if none are selected, with duplicates removed automatically. Available formats: a single certificate as DER (.cer), a concatenated PEM bundle suitable for use as a CA file, a DER-encoded PKCS#7 bundle (.p7b), and CSV including SHA-256 thumbprints.

## Notes

- Revocation status is not checked. OCSP and CRL URLs are reported for use with external tools
- Signed manifests must be in sha256sum, sha384sum, or sha512sum format. Signature files are recognized by the extensions `.sha256`, `.sha384`, `.sha512`, `.p7s`, `.p7m`, and `.sig`
- Folder drag-and-drop is not supported for pages opened from disk. Select the files directly

## Documentation

A user guide is embedded in the tool, opened from the User Guide button. [USERGUIDE](USERGUIDE.md) contains the same material.

## License

MIT License. See [LICENSE](LICENSE).

This software is provided as is, without warranty of any kind. It is not endorsed by any certificate authority or vendor. The tool verifies signatures and reports certificate contents; trust decisions remain with the operator.
