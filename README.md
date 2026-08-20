# Certificate Report/Bundle Tool

A single HTML file that inspects X.509 certificates, verifies signed bundle releases, exports certificate bundles in various formats, and exports a csv for certs/bundles displaying all relevant information. 

Usage: Open `Certificate Report Bundle Tool.html` in a modern browser.

<img width="2732" height="1294" alt="Image" src="https://github.com/user-attachments/assets/8dd81efe-d1bb-42de-a6a4-1f29c2990765" />

<img width="2655" height="1103" alt="Image" src="https://github.com/user-attachments/assets/d9a476c6-076f-4e77-a9ea-424f0ac8f3e6" />

## Capabilities

**Verify Bundle.** This checks a signed release against a manifest file to ensure integrity. The tool verifies the signature on the publisher's hash manifest, validates the signer's certificate chain to a self-signed root, and compares each bundle file's hash against the signed manifest. Both hash values are displayed for each file. The root's fingerprint is displayed for comparison against the issuing authority's published value. Attached and detached CMS signatures are supported, with RSA PKCS#1 v1.5, RSA-PSS, and ECDSA (P-256/P-384/P-521). 

**Compare Bundles.** Diffs two certificate sets in a report-style table. 

**Import Certificates.** Reads DER, PEM, headerless Base64, and PKCS#7 bundles. 

**Report.** One row per certificate: subject, issuer, validity dates, serial number, key and signature algorithms, SHA-1 thumbprint, OCSP and CRL URLs, and certificate type. Expired certificates are flagged in red. The search box highlights matching rows across all columns, including serials and thumbprints. Checkboxes select specific rows for export.

**Export.** Exports include the selected certificates, or all certificates if none are selected, with any duplicates removed automatically if present. Available export formats: a single certificate as DER (.cer), a concatenated PEM bundle suitable for use as a CA file, a DER-encoded PKCS#7 bundle (.p7b), and CSV.

## Notes

- This tool does not perform revocation status. OCSP and CRL URLs captured from the certs and presented. 
- Signed manifests must be in sha256sum, sha384sum, or sha512sum format. Signature files are recognized by the extensions `.sha256`, `.sha384`, `.sha512`, `.p7s`, `.p7m`, and `.sig`
- Folder drag-and-drop is not supported for pages opened from disk. Select all the files directly and drop them into the tool.

## Documentation

A user guide is embedded in the tool, opened from the User Guide button. [USERGUIDE](USERGUIDE.md) contains the same material.

## License

MIT License - see [LICENSE](LICENSE) file for details.

**Technical Disclaimer:**
- This software is provided "AS IS" without warranty of any kind
- The authors and contributors are not responsible for any damages or issues that may arise from its use

By using this software, you acknowledge that you have read and understood these disclaimers and agree to use this solution at your own risk.
