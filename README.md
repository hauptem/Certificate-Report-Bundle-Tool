# Certificate Report/Bundle Tool

A single HTML file that inspects X.509 certificates, verifies signed bundle releases, exports certificate bundles in various formats, and exports a csv for certs/bundles displaying all relevant information. 

Usage: Open `Certificate Report Bundle Tool.html` in a modern browser.

<img width="2576" height="1153" alt="Image" src="https://github.com/user-attachments/assets/a0a1c2aa-9b87-4a6d-bae3-6ddb28a81548" />

<img width="2576" height="1070" alt="Image" src="https://github.com/user-attachments/assets/adf71261-95bf-447a-89d0-708b01531536" />

## Capabilities

**Verify.** This checks a signed release against a manifest file to ensure integrity. The tool verifies the signature on the publisher's hash manifest, validates the signer's certificate chain to a self-signed root, and compares each bundle file's hash against the signed manifest. Chain links are required to be CA certificates (Basic Constraints), so an end-entity certificate cannot be used as an issuer. Results are shown as a table listing each file's status, manifest hash, and computed hash. The root's fingerprint is displayed for comparison against the issuing authority's published value. Attached and detached CMS signatures are supported, with RSA PKCS#1 v1.5, RSA-PSS, and ECDSA (P-256/P-384/P-521). Files containing certificates carry an Import button in the results, so a verified bundle can be added to the report without a second drop.

**Import.** Reads DER, PEM, headerless Base64, and PKCS#7 bundles. Certificates already in the report are skipped rather than added again, so importing the same bundle in multiple encodings does not create duplicate rows.

**Report.** One row per certificate: subject, issuer, validity dates, serial number, key and signature algorithms, SHA-1 thumbprint, OCSP and CRL URLs, and certificate type. Expired certificates are flagged in red. The search box highlights matching rows across all columns, including serials and thumbprints. Checkboxes select specific rows for export.

**Compare** Diffs two certificate sets in a report-style table. 

**Export.** Exports include the selected certificates, or all certificates if none are selected, with any duplicates removed automatically if present. Available export formats: a single certificate as DER (.cer), a concatenated PEM bundle suitable for use as a CA file, a DER-encoded PKCS#7 bundle (.p7b), CSV, and a standalone HTML copy of the report. A status line under the Report header confirms each export.

## Notes

- This tool does not perform revocation status. OCSP and CRL URLs are captured from the certs and presented for review. 
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
