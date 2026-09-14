
## Commands (man)

One such method is using the **man** command, which displays the manual pages for commands and provides detailed information about their usage.

### Syntax

```shellsession  
villegasjb@htb[/htb]$ man <tool> 
```

Example: 

```shellsession
villegasjb@htb[/htb]$ man ls
```

## Commands (apropos)

As we can see, the results from each other do not differ in this example. Another tool that can be useful in the beginning is **apropos**. Each manual page has a short description available within it. This tool searches the descriptions for instances of a given keyword.

### Syntax

```shellsession
villegasjb@htb[/htb]$ apropos <keyword>
```

Example: 

```shellsession
villegasjb@htb[/htb]$ apropos sudo

sudo (8)             - execute a command as another user
sudo.conf (5)        - configuration for sudo front end
sudo_plugin (8)      - Sudo Plugin API
sudo_root (8)        - How to run administrative commands
sudoedit (8)         - execute a command as another user
sudoers (5)          - default sudo security policy plugin
sudoreplay (8)       - replay sudo session logs
visudo (8)           - edit the sudoers file

```

Another useful resource to get help if we have issues to understand a long command is: https://explainshell.com/

Next, we'll be covering a large number of commands, many of which may be new to you. However, you now know how to seek help with any command you’re unfamiliar with, or unsure about its options. Also, we highly encourage you to explore your curiosity, taking as much time as needed to tinker and experiment with the tools presented. It will always be time well spent.
## Summary

This section explains **Getting Help**. It focuses on Commands (man), Commands (apropos).

## What I Did

I read through the Hack The Box material, followed the examples, and reviewed the tools and steps shown in this section.

## What I Learned

I learned the basic ideas behind **Getting Help** and how they can help me investigate and respond to security activity.
