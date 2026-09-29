## Description/Explanation

This HTB Academy section, **Detecting Windows Attacks with Splunk – Detecting Common User/Domain Recon**, explains how attackers perform Active Directory reconnaissance and how defenders can detect it using Splunk. It focuses on native Windows recon commands and BloodHound/SharpHound LDAP-based reconnaissance.

## Summary

The section covers common AD recon techniques such as:
- `whoami /all`
- `net user /domain`
- `net group "Domain Admins" /domain`
- `nltest /domain_trusts`
- `arp -a`
- `wmic computersystem get domain`

It also explains **BloodHound/SharpHound**, which performs many LDAP queries against the Domain Controller.

For detection, Windows does not log LDAP queries by default. Event `1644` can help but may miss BloodHound activity. A better option is the ETW provider `Microsoft-Windows-LDAP-Client`, often collected with **SilkETW/SilkService**. Splunk can detect native recon using Sysmon `EventID=1` process creation logs, and detect BloodHound activity using `WinEventLog:SilkService-Log` by searching for LDAP filters like `*(samAccountType=805306368)*`.

## What I did

In the HTB Academy module, I:
- Reviewed the section content.
- Spawned the target system.
- Accessed Splunk at `http://[Target IP]:8000`.
- Launched the **Search & Reporting** app.
- Examined the provided Splunk searches:
  - Native Windows recon detection using `XmlWinEventLog:Microsoft-Windows-Sysmon/Operational` and `EventID=1`.
  - BloodHound detection using `WinEventLog:SilkService-Log`, `spath`, `rename`, `table`, `search SearchFilter="*(samAccountType=805306368)*"`, `stats`, `where`, and `convert`.

## What I learned

I learned how to detect AD user/domain reconnaissance in Splunk by:
- Monitoring process creation events.
- Analyzing LDAP search filters.
- Identifying BloodHound/SharpHound behavior.
- Using Event `1644` and understanding its limitations.
- Leveraging ETW logging via SilkETW/SilkService.
- Applying Yara rules for hunting suspicious LDAP queries.
- Using Microsoft’s LDAP recon filter list.
- Applying Splunk SPL techniques such as `stats`, `values`, `dc`, `where`, `spath`, `rename`, and `convert`.