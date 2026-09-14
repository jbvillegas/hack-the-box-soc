## Editing Files

After learning how to create files and directories, let’s move on to working with these files. There are several ways to edit a file in Linux, with some of the most common text editors being **Vi** and **Vim**. However, we will start with the **Nano** editor, which is less commonly used but easier to understand.

To create and edit a file using Nano, you can **specify** the file name directly as the first parameter when launching the editor. For example, to create and open a new file named notes.txt, you would use the following command:

```shellsession
villegasjb@htb[/htb]$ nano notex.txt
```


This command will open the **Nano** editor, allowing you to start editing the file notes.txt immediately. Nano’s straightforward interface (also called **"pager"**) makes it a great choice for quickly editing text files, especially when you’re just getting started

Below we see two lines with short descriptions. The caret (^) stands for our "[CTRL]" key. For example, if we press [CTRL + W], a "Search:" line appears at the bottom of the editor, where we can enter the word or words we are looking for. If we now search for the word "we" and press [ENTER], the cursor will move to the first word that matches.

 
Now we can save the file by pressing [CTRL + O] and confirm the file name with [ENTER].

 
To view the contents of the file, we can use the command cat.

```shellsession
villegasjb@htb[/htb]$ cat notes.txt
```

Here we can type everything we want and make our notes.

On Linux systems, there are several files that can be tremendously beneficial for **penetration testers**, due to misconfigured permissions or insufficient security settings by the administrators. One such important file is the /etc/passwd file. This file contains essential information about the users on the system, such as their usernames, user IDs (UIDs), group IDs (GIDs), and home directories.

Historically, the **/etc/passwd** file also stored password hashes, but now those hashes are typically stored in **/etc/shadow**, which has stricter permissions. However, if the permissions on **/etc/passwd** or other critical files are **not** set correctly, it may expose sensitive information or lead to privilege escalation opportunities.

As penetration testers, identifying files with improper rights or permissions can provide key insights into potential vulnerabilities that might be exploited, such as weak user accounts or misconfigured file access that should otherwise be restricted. Understanding these files is vital when assessing the security posture of a system.
**VIM**

**Vim** is an open-source editor for all kinds of ASCII text, just like Nano. It is an improved clone of the previous Vi. It is an extremely powerful editor that focuses on the essentials, namely editing text. For tasks that go beyond that, Vim provides an interface to external programs, such as **grep**, **awk**, **sed**, etc., which can handle their specific tasks much better than a corresponding function directly implemented in an editor usually can. This makes the editor small and compact, fast, powerful, flexible, and less error-prone.

**Vim** follows the Unix **principle** here: many small specialized programs that are well tested and proven, when combined and communicating with each other, resulting in a flexible and powerful system.

In contrast to **Nano**, Vim is a modal editor that can distinguish between text and command input. Vim offers a total of six fundamental modes that make our work easier and make this editor so powerful:



When we have the Vim editor open, we can go into command mode by typing **":"** and then typing **"q"** to close Vim.

Vim offers an excellent opportunity called vimtutor to practice and get familiar with the editor. It may seem very difficult and complicated at first, but it will only feel that way for a short time. The efficiency we gain from Vim once we get used to it is enormous. Entering the tutor mode in vim editor can be done using the Command mode :Tutor or by using the vimtutor command in the shell.
VimTutor
## Summary

This section explains **Editing Files**. It focuses on the main ideas and practical examples.

## What I Did

I read through the Hack The Box material, followed the examples, and reviewed the tools and steps shown in this section.

## What I Learned

I learned the basic ideas behind **Editing Files** and how they can help me investigate and respond to security activity.
