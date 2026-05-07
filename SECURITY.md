# Security Verification Guide

This repository distributes signed release artifacts for verification purposes.

The application binaries are distributed together with:

- SHA-256 hashes
- Detached GPG signatures
- Public verification key

This allows users to independently verify:

1. File integrity
2. File authenticity
3. That the distributed hash matches the distributed binary

---

# Files

| File                   | Purpose                                 |
| ---------------------- | --------------------------------------- |
| `SeuApp Setup.exe`     | Application installer                   |
| `SeuApp Setup.exe.sig` | Detached GPG signature of the installer |
| `SHA256SUMS.txt`       | SHA-256 hashes                          |
| `SHA256SUMS.txt.sig`   | Detached GPG signature of the hash list |
| `PUBLIC_KEY.asc`       | Public verification key                 |

---

# Install GPG

Windows users can install:

- Gpg4win

Official website:
https://www.gpg4win.org/

---

# Import Public Key

Import the provided public key:

```bash
gpg --import PUBLIC_KEY.asc
```

---

# Verify Installer Signature

Verify that the installer was signed by the maintainer:

```bash
gpg --verify "SeuApp Setup.exe.sig" "SeuApp Setup.exe"
```

Expected result:

```plaintext
Good signature from ...
```

This confirms:

- The installer was signed using the maintainer private key
- The installer has not been modified after signing

---

# Verify SHA256SUMS Signature

Verify the authenticity of the hash list:

```bash
gpg --verify SHA256SUMS.txt.sig SHA256SUMS.txt
```

Expected result:

```plaintext
Good signature from ...
```

This confirms:

- The hash list is authentic
- The hash list was not modified

---

# Verify Installer Hash

Generate the installer hash locally:

```bash
certutil -hashfile "SeuApp Setup.exe" SHA256
```

Compare the generated SHA-256 value with the corresponding value inside:

```plaintext
SHA256SUMS.txt
```

The values must match exactly.

---

# Verification Chain

The complete verification chain is:

1. Verify `SHA256SUMS.txt.sig`
2. Verify `SeuApp Setup.exe.sig`
3. Verify installer SHA-256 matches `SHA256SUMS.txt`

If all validations succeed:

- The installer integrity is confirmed
- The installer authenticity is confirmed
- The distributed hash authenticity is confirmed

---

# Important Notes

- Never trust unsigned binaries
- Never trust modified hash files
- Always verify signatures before executing binaries
- The private signing key is never distributed

---

# Fingerprint

Public key fingerprint:

```plaintext
8AEA 02BA AFD4 DBCC A6B4 ABF0 08BD 0E61 A44F C2C5
```
