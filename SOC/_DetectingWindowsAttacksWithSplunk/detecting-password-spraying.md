## Description/Explanation

This HTB Academy section explains **password spraying** attacks and how to detect them using **Splunk**. It focuses on Windows Security event logs, especially **Event ID 4625 (Failed Logon)**, and shows how to identify multiple failed logons from the same source IP across different user accounts in a short time window.

## Summary

Password spraying differs from brute-force because it tries a small number of common passwords across many accounts to avoid account lockouts. Detection relies on spotting patterns such as many failed logons from one source IP against multiple users.

Relevant Windows event logs include:
- `4625` — Failed Logon
- `4768` with `ErrorCode 0x6` — Kerberos Invalid Users
- `4768` with `ErrorCode 0x12` — Kerberos Disabled Users
- `4776` with `ErrorCode 0xC0000064` — NTLM Invalid Users
- `4776` with `ErrorCode 0xC000006A` — NTLM Wrong Password
- `4648` — Authenticate Using Explicit Credentials
- `4771` — Kerberos Pre-Authentication Failed

The provided Splunk search:
```spl
index=main earliest=1690280680 latest=1690289489 source="WinEventLog:Security" EventCode=4625
| bin span=15m _time
| stats values(user) as Users, dc(user) as dc_user by src, Source_Network_Address, dest, EventCode, Failure_Reason
```

Key SPL breakdown:
- Filters `index=main`, `source="WinEventLog:Security"`, and `EventCode=4625`.
- Restricts events to the given Unix timestamp range.
- Uses `bin span=15m _time` to group events into 15-minute buckets.
- Uses `stats` to aggregate by `src`, `Source_Network_Address`, `dest`, `EventCode`, and `Failure_Reason`.
- `values(user) as Users` collects unique usernames.
- `dc(user) as dc_user` counts distinct usernames per group.

## What I did

In the HTB Academy module, I:
- Reviewed the password spraying section.
- Spawned the target system.
- Accessed the Splunk interface at `http://[Target IP]:8000`.
- Opened the **Search & Reporting** app.
- Ran the provided Splunk search to detect failed logon attempts.
- Analyzed results for patterns of password spraying, such as multiple users failing authentication from the same source IP.

## What I learned

I learned:
- How password spraying differs from traditional brute-force attacks.
- Which Windows event IDs are useful for detecting password spraying.
- How to use Splunk SPL commands like `bin`, `stats`, `values`, and `dc` to analyze failed logon events.
- How to group failed logons by source IP, destination host, and failure reason.
- How to identify suspicious authentication patterns that may indicate password spraying activity.