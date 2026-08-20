# Certificate Report/Bundle Tool v1.0

![License](https://img.shields.io/badge/license-MIT-green)
![Dependencies](https://img.shields.io/badge/dependencies-none-blue)

A single HTML file for inspecting, verifying, and rebuilding certificate bundles. Open it in a browser. Runs offline from disk; nothing leaves the machine.

### What it does

- **Verify** - Validates a publisher's signed hash manifest (CMS/PKCS#7, attached or detached; RSA, RSA-PSS, ECDSA), verifies the signer chain to a self-signed root, and checks every bundle file's hash against the manifest. Root fingerprints are displayed for out-of-band comparison; no root is implicitly trusted. Renamed files are matched by content hash
- **Import** - Reads DER, PEM, Base64, and .p7b. Bundles expand to one row per certificate: issuer, validity, serial, key, signature algorithm, thumbprint, OCSP/CRL URLs, type. Expired certs flag red
- **Search** - Highlights matches across every field, including serials and thumbprints. Answers "is this CA in the bundle" in one paste
- **Export** - CSV, concatenated PEM (a working CAfile), .p7b, or a single .pem/.cer. Exports honor row selection and deduplicate

### Limitations

- No revocation checking; the tool is offline. CRL/OCSP URLs are reported for external use
- Manifests must be sha256sum/sha384sum/sha512sum line format. Signature files are recognized by extension: `.sha256` `.sha384` `.sha512` `.p7s` `.p7m` `.sig`
- No folder drag-and-drop (browsers block it for file:// pages). Multi-select files instead

### Documentation

- [User Guide](USERGUIDE.md)

## License

MIT License - see [LICENSE](LICENSE).

Provided as is, without warranty. Not endorsed by any CA or vendor. The tool verifies signatures and reports facts; trust decisions are yours.
