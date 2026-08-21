# Certificate Report/Bundle Tool - User Guide

Usage: Open `Certificate_Report_Bundle_Tool.html` in a modern browser

The tool has three sections: Verify, Import, and Report. They work independently.

## Verify

Use this section to check a signed release before trusting it. Drop the signature file, the CA chain file if one was provided, and the bundle files. The tool verifies the signature on the manifest, validates the signer's certificate chain, and compares each file's hash against the signed manifest. Results are shown as a table listing each file's status, manifest hash, and computed hash, with certificate files listed first.

The chain is verified up to a self-signed root. Every link in the chain must be a CA certificate (Basic Constraints), so an end-entity certificate cannot be used as an issuer. Because the root arrives in the same download, the tool displays its fingerprint rather than trusting it. Compare the fingerprint against the value published by the issuing authority.

Red results indicate the bundle cannot be trusted: an invalid signature, altered content, a broken chain, a non-CA certificate used as an issuer, or a file hash mismatch. Amber results indicate a warning, such as a missing chain file or an expired certificate.

A file that was renamed after download is matched to its manifest entry by content hash and reported accordingly. For detached signatures, include the manifest file in the drop.

Files containing certificates show an Import button in the results, and an Import all button appears when several are present. These add the file's certificates to the report directly, using the same batch fields, filename-derived metadata, and duplicate skipping as the import drop zone, so verified bundles do not need a second drop.

Recognized signature extensions are `.sha256`, `.sha384`, `.sha512`, `.p7s`, `.p7m`, and `.sig`. Manifests must be in sha256sum, sha384sum, or sha512sum format. Supported signature algorithms are RSA PKCS#1 v1.5, RSA-PSS, and ECDSA on P-256, P-384, and P-521.

The Clear button resets the panel for another bundle.

## Import

Drop certificate files to add them to the report. Supported formats are DER, PEM, headerless Base64, and PKCS#7 bundles. Bundles expand to one row per certificate, and each row is named by the certificate's subject CN. A certificate already in the report is skipped rather than added again, so dropping the same bundle in multiple encodings does not create duplicate rows; a notice above the table shows the skipped count. Files that fail to parse are listed above the table without affecting the rest of the drop.

The Category, Version, and Release Date fields are optional and populate the corresponding report columns for each drop. When Category or Version is blank, filenames following the `certificates_pkcs7_v5_14_dod` convention fill them automatically; values you type take precedence.

## Report

Each certificate appears as one row showing its subject, issuer, validity dates, serial number, key and signature algorithms, SHA-1 thumbprint, revocation URLs, and certificate type. Expired certificates are flagged in red. Click the Certificate Name or Expiration header to sort.

The search box highlights matching rows across all columns, including serials and thumbprints, without hiding the other rows. Use the checkboxes to select rows for export.

## Compare

The Compare button opens a two-sided comparison. Drop certificates or bundles on the Reference and Comparison sides. Either side accepts the same formats as import, across multiple files. Results appear once both sides hold certificates.

Differences are shown as a table with the same fields as the report. A certificate present in the reference but not the comparison is marked MISSING IN COMPARISON BUNDLE in red; the reverse is marked MISSING IN REFERENCE BUNDLE in amber. A certificate with the same subject but different content is marked CHANGED, with one row per version. Matching uses the full subject rather than the common name. The Comparison drop zone is outlined red when entries are missing from it and amber when it only differs.

Certificates present in both sets are summarized as a count. The Show all button adds them to the table as IN BOTH rows.

## Export

Exports include the selected certificates, or all certificates if none are selected. Duplicate certificates are removed automatically. Each export prompts for the filename, with a default supplied, and a status line under the Report header confirms the result.

- Export .cer writes a single certificate as DER, named after the certificate. Available when exactly one certificate is in scope
- Export PEM bundle writes a concatenated PEM file suitable for use as a CA file
- Export P7B bundle writes a DER-encoded PKCS#7 bundle
- Export CSV writes the report table, including SHA-256 thumbprints

## Notes

- Revocation status is not checked. OCSP and CRL URLs are reported for use with external tools
- Windows may block downloaded .cer files. Right-click the file, open Properties, and select Unblock

## Troubleshooting

- If a signature file is not recognized, rename it to one of the recognized extensions. The signature covers the file content, so renaming does not affect verification
- If a detached signature reports that no files match, include the manifest file in the drop
- If the signer certificate is not found, drop the publisher's chain file. The signature file does not embed the signer's certificate
- If the chain is incomplete, drop the missing issuer. Certificates from any dropped file are used for chain building
- A file reported as skipped matches nothing in the manifest by name or content. This is expected for chain files and documentation included in a release
- Folder drag-and-drop is not supported for pages opened from disk. Select the files directly
- If fewer rows appear than expected, check the notices above the table for files that failed to parse
