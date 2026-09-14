## Network Services

When working with Linux, managing various network services is essential. Proficiency in handling these services is crucial for several reasons. Network services are designed to perform specific tasks, many of which enable remote operations. It is important to have the knowledge and skills to communicate with other computers over the network, establish connections, transfer files, analyze network traffic, and configure these services effectively. This expertise allows us to identify potential vulnerabilities during penetration testing. Additionally, understanding the configuration options of each service enhances our overall comprehension of network security.

Consider a scenario where we are conducting a penetration test and encounter a Linux host being assessed for vulnerabilities. By monitoring network traffic, we observe that a user on this Linux host is connecting to another server via an unencrypted FTP server. Consequently, we are able to capture the user's credentials in plain text. This situation would be much less likely if the user were aware that FTP does not encrypt connections or the data transmitted. For a Linux administrator, this represents a critical oversight, as it not only exposes security weaknesses within the network but also reflects poorly on the administrators responsible for maintaining the network's security.

While it is not feasible to cover every network service, we will focus on the most important ones. This approach is beneficial not only for administrators and users, but also for penetration testers who need to understand the interactions between different hosts and their own systems.

## SSH

Secure Shell (SSH) is a network protocol that allows the secure transmission of data and commands over a network. It is widely used to securely manage remote systems and securely access remote systems to execute commands or transfer files. In order to connect to our or a remote Linux host via SSH, a corresponding SSH server must be available and running.

The most commonly used SSH server is the OpenSSH server. OpenSSH is a free and open-source implementation of the Secure Shell (SSH) protocol that allows the secure transmission of data and commands over a network.

Administrators use OpenSSH to securely manage remote systems by establishing an encrypted connection to a remote host. With OpenSSH, administrators can execute commands on remote systems, securely transfer files, and establish a secure remote connection without the transmission of data and commands being intercepted by third parties.

## NFS

Network File System (NFS) is a network protocol that allows us to store and manage files on remote systems as if they were stored on the local system. It enables easy and efficient management of files across networks. For example, administrators use NFS to store and manage files centrally (for Linux and Windows systems) to enable easy collaboration and management of data. For Linux, there are several NFS servers, including NFS-UTILS (Ubuntu), NFS-Ganesha (Solaris), and OpenNFS (Redhat Linux).

It can also be used to share and manage resources efficiently, e.g., to replicate file systems between servers. It also offers features such as access controls, real-time file transfer, and support for multiple users accessing data simultaneously. We can use this service just like FTP in case there is no FTP client installed on the target system, or NFS is running instead of FTP.

![[Pasted image 20260722093410.png]]

## Web Server

Understanding the operation of web servers is essential for penetration testers, as these servers are integral to web applications and frequently serve as primary targets during security assessments. A web server is software that delivers data, documents, applications, and various functions over the Internet. It utilizes the H**ypertext Transfer Protocol (HTTP)** to transmit data to clients such as web browsers and to receive requests from these clients. The received data is then rendered as Hypertext Markup Language (HTML) within the client's browser, facilitating the creation of dynamic web pages that respond interactively to user requests. Consequently, a thorough comprehension of web server functionalities is vital for developing secure and efficient web applications and for maintaining overall system security. Among the most widely used web servers on Linux platforms are Apache, Nginx, Lighttpd, and Caddy, with Apache being particularly popular due to its broad compatibility with operating systems including Ubuntu, Solaris, and Red Hat Linux.

For **penetration testers**, web servers offer various utilities. They can be employed to facilitate file transfers, enabling testers to log in and interact with target systems through HTTP or HTTPS ports. Additionally, web servers can be leveraged to conduct phishing attacks by hosting replicas of target pages, thereby attempting to capture user credentials. Beyond these applications, web servers provide numerous other opportunities for testing and exploiting vulnerabilities within a network.

Apache web server has a variety of features that allow us to host a secure and efficient web application. Moreover, we can also configure logging to get information about the traffic on our server, which helps us analyze attacks.

## VPN

A Virtual Private Network (VPN) functions like a secure, invisible tunnel that connects us to another network, allowing seamless and protected access as if we were physically present within it. This is achieved by establishing an encrypted tunnel between the client and the server, ensuring that all data transmitted through this connection remains confidential and safeguarded from unauthorized access.

Organizations primarily utilize VPNs to grant their employees secure access to the internal network without requiring them to be on-site. This flexibility enables employees to reach internal resources and applications from any location, enhancing productivity and mobility. Additionally, VPNs serve to anonymize internet traffic and block external intrusions, further bolstering security.

Among the most widely used VPN solutions for Linux servers are OpenVPN, L2TP/IPsec, PPTP, SSTP, and SoftEther. OpenVPN stands out as a popular open-source option compatible with various operating systems, including Ubuntu, Solaris, and Red Hat Linux. Administrators leverage OpenVPN to facilitate secure remote access to corporate networks, encrypt network traffic, and maintain user anonymity online.

For penetration testers, OpenVPN offers invaluable capabilities. It allows testers to securely connect to internal networks, especially when direct access is not feasible due to geographical constraints. By utilizing OpenVPN, penetration testers can perform comprehensive security assessments of internal systems, identifying and addressing potential vulnerabilities. The versatility of OpenVPN, with features such as encryption, tunneling, traffic shaping, network routing, and adaptability to dynamic network environments, makes it an essential tool in the arsenal of both network administrators and security professionals. We can install the server and client with the following command:
## Summary

This section explains **Network Services**. It focuses on SSH, NFS, Web Server, VPN.

## What I Did

I read through the Hack The Box material, followed the examples, and reviewed the tools and steps shown in this section.

## What I Learned

I learned the basic ideas behind **Network Services** and how they can help me investigate and respond to security activity.
