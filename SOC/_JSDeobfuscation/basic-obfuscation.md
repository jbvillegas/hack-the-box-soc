## Minifying JavaScript code

A common way of reducing the readability of a snippet of JavaScript code while keeping it fully functional is JavaScript minification. Code minification means having the entire code in a single (often very long) line. Code minification is more useful for longer code, as if our code only consisted of a single line, it would not look much different when minified.

Many tools can help us minify JavaScript code, like javascript-minifier. 

A **packer** obfuscation tool usually attempts to convert all words and symbols of the code into a list or a dictionary and then refer to them using the (p,a,c,k,e,d) function to re-build the original code during execution. The (p,a,c,k,e,d) can be different from one packer to another. However, it usually contains a certain order in which the words and symbols of the original code were packed to know how to order them during execution.

While a packer does a great job reducing the code's readability, we can still see its main strings written in cleartext, which may reveal some of its functionality. This is why we may want to look for better ways to obfuscate our code.
## Summary

This section explains **Basic Obfuscation**. It focuses on Minifying JavaScript code.

## What I Did

I read through the Hack The Box material, followed the examples, and reviewed the tools and steps shown in this section.

## What I Learned

I learned the basic ideas behind **Basic Obfuscation** and how they can help me investigate and respond to security activity.
