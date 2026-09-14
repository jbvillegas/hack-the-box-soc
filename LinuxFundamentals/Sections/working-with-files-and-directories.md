
The primary difference between working with files in Linux, as opposed to Windows, lies in how we access and manage those files. In Windows, we typically use graphical tools like Explorer to find, open, and edit files. However, in Linux, the terminal offers a powerful alternative where files can be accessed and edited directly using commands. This method is not only faster, but also more efficient, as it allows you to edit files interactively without even needing editors like vim or nano.

The terminal's efficiency stems from its ability to access files with just a few commands, and it allows you to modify files selectively using regular expressions (regex). Additionally, you can run multiple commands at once, redirecting output to files and automating batch editing tasks, which is a major time-saver when working with numerous files simultaneously. This command-line approach streamlines workflow, making it an invaluable tool for tasks that would be more time-consuming through a graphical interface.

Next, we will explore working with files and directories to effectively manage the content on our operating system.

## Create, Move, & Copy

Let us begin by learning how to perform key operations like creating, renaming, moving, copying, and deleting files. Before we execute the following commands, we first need to SSH into the target (using the connection instructions at the bottom of the section). Now, let's say we want to create a new file or directory. The syntax for this is the following:

```shellsession
villegasjb@htb[/htb]$ touch <name>

villegasjb@htb[/htb]$ touch <name>

```

**-p:** allows us to create parent directories.

**.tree:** allows us to view the whole folder tree.

You can create files directly within specific directories by specifying the path where the file should be stored, and you can use the single dot **(.)** to indicate that you want to start from the current directory. This is a convenient way to work within your current location, without needing to type the full path. Therefore, the command for creating another empty file looks like this:

With the command **mv**, we can move and also rename files and directories. The syntax for this looks like this:

```shellsession
villegasjb@htb[/htb]$ mv <file/directory> <renamed file/directory>
```
## Summary

This section explains **Working With Files And Directories**. It focuses on Create, Move, & Copy.

## What I Did

I read through the Hack The Box material, followed the examples, and reviewed the tools and steps shown in this section.

## What I Learned

I learned the basic ideas behind **Working With Files And Directories** and how they can help me investigate and respond to security activity.
