## Find Files and Directories

It is crucial to be able to find the files and folders we need. Once we have gained access to a Linux based system, it will be essential to find configuration files, scripts created by users or the administrator, and other files and folders. We do not have to manually browse through every single folder and check when modified for the last time. There are some tools we can use to make this work easier.

## Which

One of the common tools is **which**. This tool returns the path to the file or link that should be executed. This allows us to determine if specific programs, like **cURL**, **netcat**, **wget**, **python**, **gcc**, are available on the operating system. Let us use it to search for Python in our interactive instance.

## Find

Another handy tool is **find**. Besides the function to find files and folders, this tool also contains the function to filter the results. We can use filter parameters like the size of the file or the date. We can also specify if we only search for files or folders.

![[Pasted image 20260717105205.png]]

## Locate 

It will take much time to search through the whole system for our files and directories to perform many different searches. The command **locate** offers us a quicker way to search through the system. In contrast to the **find** command, **locate** works with a local database that contains all information about existing files and folders. We can update this database with the following command.
## Summary

This section explains **Find Files And Directories**. It focuses on Which, Find, Locate.

## What I Did

I read through the Hack The Box material, followed the examples, and reviewed the tools and steps shown in this section.

## What I Learned

I learned the basic ideas behind **Find Files And Directories** and how they can help me investigate and respond to security activity.
