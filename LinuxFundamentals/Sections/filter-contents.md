In the previous section, we explored how to use redirection to send the output of one program into another for further processing. Now, let's talk about reading files directly from the command line, without needing to open a text editor.

There are two powerful tools for this - **more** and **less**. These are known as **pagers**, and they allow you to view the contents of a file interactively, one screen at a time. While both tools serve a similar purpose, they have some differences in functionality, which we'll touch on later.

Using **more** and **less**, you can easily scroll through large files, search for text, and navigate forward or backward without modifying the file itself. This is especially useful when you're working with large logs or text files that don't fit neatly into one screen.

The goal for this section is to learn how to filter content and handle the redirected output from previous commands. But before we dive into filtering, we need to become familiar with some essential tools and commands that are specifically designed to make filtering more efficient and powerful.

Before we start filtering the output of commands, let’s explore a few foundational tools that will help you efficiently sift through and manipulate text. These tools are crucial when working with large amounts of data or when you need to automate tasks that involve searching, sorting, or processing information.

Let's look at some examples to understand how these tools work in practice.

## More

```shellsession
villegasjb@htb[/htb]$ cat /etc/passwd | more
```

The **/etc/passwd** file in Linux is like a phone directory for users on the system. It includes details such as the username, user ID, group ID, home directory, and the default shell they use.

After we read the content using **cat** and redirected it to **more**, the already mentioned **pager** opens, and we will automatically start at the beginning of the file.

## Less

If we now take a look at the tool **less**, we will notice on the man page that it contains many more features than more.

```shellsession
villegasjb@htb[/htb]$ less /etc/passwd
```

## Head

Sometimes we will only be interested in specific issues either at the beginning of the file or the end. If we only want to get the **first** lines of the file, we can use the tool **head**. By default, **head** prints the **first** ten lines of the given file or input, if not specified otherwise.

## Tail 

If we only want to see the **last** parts of a file or results, we can use the counterpart of head called **tail**, which returns the last ten lines.

## Sort 

Depending on which results and files are dealt with, they are rarely sorted. Often it is necessary to sort the desired results alphabetically or numerically to get a better overview. For this, we can use a tool called **sort**.

## Grep

In many cases, we will need to search for specific results that match patterns we define. One of the most commonly used tools for this purpose is grep, which provides a wide range of powerful features for pattern searching. For instance, we can use grep to search for users who have their default shell set to **/bin/bash**.

```shellsession
villegasjb@htb[/htb]$ cat /etc/passwd | grep "/bin/bash"

root:x:0:0:root:/root:/bin/bash
mrb3n:x:1000:1000:mrb3n:/home/mrb3n:/bin/bash
cry0l1t3:x:1001:1001::/home/cry0l1t3:/bin/bash
htb-student:x:1002:1002::/home/htb-student:/bin/bash
```

This is just one example of how grep can be applied to efficiently filter data based on predefined patterns. Another possibility is to exclude specific results. For this, the option **"-v"** is used with **grep**. In the next example, we exclude all users who have disabled the standard shell with the name **"/bin/false"**** or **"/usr/bin/nologin**". 

## Tr

Another possibility to replace certain characters from a line with characters defined by us is the tool **tr**. As the first option, we define which character we want to replace, and as a second option, we define the character we want to replace it with. In the next example, we replace the colon character with space.

## Awk

As we may have noticed, the line for the user **"postgres"** has one column too many. To keep it as simple as possible to sort out such results, the **(g)awk** programming is beneficial, which allows us to display the first **($1) and last ($NF)** result of the line.
## Summary

This section explains **Filter Contents**. It focuses on More, Less, Head, Tail.

## What I Did

I read through the Hack The Box material, followed the examples, and reviewed the tools and steps shown in this section.

## What I Learned

I learned the basic ideas behind **Filter Contents** and how they can help me investigate and respond to security activity.
