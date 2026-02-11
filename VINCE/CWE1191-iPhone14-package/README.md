# CVE 2026-25251 CWE-1191
## iPhone 14 Pro Max - A16 Bionic

**Cross-platform confirmation** of CVE-2026-25251 hardware vulnerability initially reported on iPhone 15 Pro Max (A17 Pro).

## Package Contents (5 Files - VINCE Submission)
| File | Purpose | Verification Command |
|------|---------|---------------------|
| `CWE-1191_EVIDENCE_REPORT.txt` | Executive summary + register analysis | `cat CWE-1191_EVIDENCE_REPORT.txt` |
| `powerlog_2026-01-18_14-17_ADE45F6B.PLSQL` | Raw powerlog w/ register 0x2081 dump | Used by `cwe1191_triage.py` |
| `log_2026-01-18_14-17_1CD45F2D.BGSQL` | BGSQL w/ 756 ghost wakes | `bgsql_ghost_wake_analyzer.py log_*.BGSQL` |
| `cwe1274_triage.py` | Extracts unfused security bits (0x2081 → Bits 4-6=0) | `python3 cwe1191_triage.py powerlog_*.PLSQL log_*.BGSQL` |
| `bgsql_ghost_wake_analyzer.py` | Proves 756 hardware-initiated wakes bypassing iOS | `python3 bgsql_ghost_wake_analyzer.py log_*.BGSQL` |


## Key Findings (iPhone 14 Pro Max)

Register 0x2081: 0b0010000010000001
1. → Bits 4,5,6 = 0 (UNFUSED in PRODUCTION hardware)
2. → 756 SLEEP-state ghost wakes (~6min intervals)
3. → 27-28mAh capacity drops (HW manipulation signature)
4. → ZERO iOS task correlation = direct hardware access


