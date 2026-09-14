![[Pasted image 20260722090853.png]]

## Advanced Package Manager (APT)

Debian-based Linux distributions use the APT package manager. A package is an archive file containing multiple ".deb" files. The dpkg utility is used to install programs from the associated ".deb" file. APT makes updating and installing programs easier because many programs have dependencies. When installing a program from a standalone ".deb" file, we may run into dependency issues and need to download and install one or multiple additional packages. APT makes this easier and more efficient by packaging together all of the dependencies needed to install a program.

Each Linux distribution uses software repositories that are updated often. When we update a program or install a new one, the system queries these repositories for the desired package. Repositories can be labeled as stable, testing, or unstable. Most Linux distributions utilize the most stable or "main" repository. This can be checked by viewing the contents of the /etc/apt/sources.list file. The repository list for Parrot OS is at /etc/apt/sources.list.d/parrot.list.
## Summary

This section explains **Package Management**. It focuses on Advanced Package Manager (APT).

## What I Did

I read through the Hack The Box material, followed the examples, and reviewed the tools and steps shown in this section.

## What I Learned

I learned the basic ideas behind **Package Management** and how they can help me investigate and respond to security activity.
