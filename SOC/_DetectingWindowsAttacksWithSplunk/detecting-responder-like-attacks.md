- **Topic:** Detecting Responder-Like Attacks

- **Quick short description:** this section analyzes **LLMNR (Link-Local Multicast Name Resolution)** and **NBT-NS (NetBIOS Name Service)** poisoning and its steps

- **Summary:** LLMR and NBT-NS poisoning are also referred as NBNS spoofing, and they are network level attacks that exploit inefficiencies in name resolution protocols. Both are used to resolve hostnames to IP addresses on local networks when the **Fully Qualified Domain Name (FQDN)** resolution fails.

These are the attack steps: 

    1. A victim device sends a name resolution query for a mistyped hostname.
    2. DNS fails to resolve the mistyped hostname.
    3. The victim device sends a name resolution query for the mistyped hostname using LLMNR/NBT-NS.
    4. The attacker's host responds to the LLMNR (**UDP 5355**)/NBT-NS (**UDP 137**) traffic pretending to know the identity of the requested host. This **poisons** the service, directing the victim to communicate with the adversary-controlled system. 
    5. Result (SUCCESS): the attacker obtains the victim's NetNTLM hash.


`Responder Detection Opportunities:` They are certain ways to detect LLMNR, NBT-NS, and mDNS poisoning, but they are not easy. These are the following: 

    - Deploy network monitoring solutions to detect unusual LLMNR and NBT-NS traffic patterns.
    - Use a honeypot approach where name resolution for non-existent hosts should fail. 

We can use a PowerShell script to automate an scheduled task to aid in detection, and log everything by using `New-EventLog`. 

`Detecting Responder-Like Attacks with Splunk:` 

    ```shellsession
    index=main earliest=1690290814 latest=1690291207 EventCode IN (4648) 
    | table _time, EventCode, source, name, user, Target_Server_Name, Message
    | sort 0 _time
    ```


- **What I did:** I read and studied the material to then modify and use the Sysmon Event 22 event provided by the activity in Splunk. I wrote a Splunk script to identify all the names whose locations were spoofed. 

- **What I learned:** I learned that these attacks focuse on attacking ineficiencies in DNS resolution systems. I have also learned some effective ways to prevent, detect and log these types of poisonous attacks. 
Splunk as always is a great tool for analyzing and filtering this, and to sort out names. 