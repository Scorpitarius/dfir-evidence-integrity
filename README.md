# DFIR-001 | Forensic File Integrity Verification

## Investigation Overview

**Case ID:** DFIR-001  
**Examination Date:** October 31, 2026  
**Classification:** Controlled Laboratory Exercise  
**Status:** Completed

This investigation demonstrates the use of SHA-256 cryptographic hashing to verify digital file integrity in a controlled Windows forensic laboratory.

An original text file was created and duplicated for examination. Initial SHA-256 comparisons confirmed matching file contents. Following a controlled modification to the working copy, subsequent hash verification identified a difference.

## Objectives

- Generate synthetic digital test evidence.
- Preserve an original file and create a working copy.
- Calculate and compare SHA-256 hashes.
- Introduce a controlled modification.
- Detect the modification through hash comparison.
- Document examination procedures and findings.

## Laboratory Environment

| Component | Configuration |
|---|---|
| Operating System | Windows 10 |
| Virtualization | VMware Workstation Pro |
| Network | Isolated VMnet2 host-only network |
| Examination Tool | Windows PowerShell |
| Hashing Command | Get-FileHash |
| Hash Algorithm | SHA-256 |

## Evidence Description

| Evidence Item | Filename |
|---|---|
| Original evidence | `original.txt` |
| Working copy | `original-working-copy.txt` |
| Final hash records | `final-hashes.csv` |
| Verification results | `integrity-verification.txt` |
| Screenshot hash records | `screenshot-hashes.csv` |

## Examination Methodology

### 1. Evidence Creation

Generated a synthetic text file using PowerShell and stored it in a designated evidence directory.

### 2. Working Copy Creation

Created a duplicate in a separate working directory to preserve the original evidence.

### 3. Initial Integrity Verification

Calculated SHA-256 hashes using PowerShell's `Get-FileHash` cmdlet.

The original and working copy produced matching hash values, indicating identical file contents at the time of verification.

### 4. Controlled Modification

Appended additional text to `original-working-copy.txt` without modifying the original evidence file.

### 5. Post-Modification Verification

Recalculated the SHA-256 hashes and compared the results.

```powershell
(Get-FileHash "$Evidence\original.txt").Hash -eq (Get-FileHash "$Working\original-working-copy.txt").Hash
```

**Result:** `False`

The comparison established that the working copy no longer matched the original.

### 6. Documentation

Exported final hash values to `final-hashes.csv` and verification results to `integrity-verification.txt`.

Calculated SHA-256 hashes of three supporting screenshots and recorded them in `screenshot-hashes.csv`.

## Findings

| Test | Result | Interpretation |
|---|---|---|
| Initial SHA-256 comparison | True | Original and working copy matched |
| Controlled modification | Completed | Working copy contents changed |
| Final SHA-256 comparison | False | Working copy no longer matched original |

**Finding 001:** The original and working copy initially produced identical SHA-256 hashes.

**Finding 002:** Following modification, the working copy produced a different SHA-256 hash.

**Finding 003:** The comparison successfully detected the intentional content modification.

## Limitations

- The investigation used synthetic evidence in a controlled virtual laboratory.
- No forensic disk imaging, write-blocking, formal acquisition, or complete chain-of-custody process was performed.
- Saved verification files contain final hash values; initial matching values and the post-modification comparison were documented through screenshots.
- SHA-256 verification supports content integrity assessment but does not independently establish evidence origin, authenticity, or custody history.

## Conclusion

This investigation demonstrated the importance of preserving original evidence, examining working copies, and verifying file integrity using cryptographic hashes.

The controlled modification produced a different SHA-256 hash, illustrating how hashing can identify changes to digital evidence.

## Supporting Documentation

The investigation report, screenshots, and sanitized supporting artifacts will be added after review.
