A file descriptor **(FD)** in Unix/Linux operating systems is a reference, maintained by the kernel, that allows the system to manage Input/Output **(I/O)** operations. It acts as a unique identifier for an open file, socket, or any other I/O resource. In Windows-based operating systems, this is known as a file handle. Essentially, the file descriptor is the system's way of keeping track of active I/O connections, such as reading from or writing to a file.

Think of it as a ticket number you get when checking in your coat at a coatroom. The ticket (file descriptor) represents your connection to your coat (file or resource), and whenever you need to retrieve your coat (perform I/O), you present the ticket to the attendant (operating system) who knows exactly where your coat is stored (which resource the file descriptor refers to). Without the ticket, you'd have no way of efficiently accessing your coat among the many others stored, just as without a file descriptor, the operating system wouldn't know which resource to interact with. You will soon see why file descriptors are so important and why understanding them is crucial as we dive into the upcoming examples

## Redirect STDIN Stream to a File

We can also use the double lower-than characters (<<) to add our standard input through a stream. We can use the so-called **End-Of-File (EOF)** function of a Linux system file, which defines the input's end. In the next example, we will use the cat command to read our streaming input through the stream and direct it to a file called "stream.txt."

```shellsession
villegasjb@htb[/htb]$ cat << EOF > stream.txt
```

## Pipes

Another way to redirect **STDOUT** is to use pipes **(|)**. These are useful when we want to use the **STDOUT** from one program to be processed by another. One of the most commonly used tools is grep, which we will use in the next example. **Grep** is used to filter **STDOUT** according to the pattern we define. In the next example, we use the find command to search for all files in the **"/etc/"** directory with a **".conf"** extension. Any errors are redirected to the **"null device"** **(/dev/null)**. Using grep, we filter out the results and specify that only the lines containing the pattern **"systemd"** should be displayed.

```shellsession
villegasjb@htb[/htb]$ find /etc/ -name *.conf 2>/dev/null | grep systemd
```

By adding **wc -l** we can count and list the number of found results
## Summary

This section explains **File Descriptions And Redirections**. It focuses on Redirect STDIN Stream to a File, Pipes.

## What I Did

I read through the Hack The Box material, followed the examples, and reviewed the tools and steps shown in this section.

## What I Learned

I learned the basic ideas behind **File Descriptions And Redirections** and how they can help me investigate and respond to security activity.
