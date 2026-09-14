Services, also known as **daemons**, are fundamental components of a Linux system that run silently in the background **"without direct user interaction"**. They perform crucial tasks that keep the system operational and provide additional functionalities. Generally, services can be categorized into two types:

### System Services

These are internal services required during system startup. They perform essential hardware-related tasks and initialize system components necessary for the operating system to function properly. These are like the engine and transmission systems. They start when you turn the ignition key and are essential for the car to run. Without them, the car wouldn't move.
### User-Installed Services

These services are added by users and typically include server applications and other background processes that provide specific features or capabilities. These types of services are like the car's air conditioning or GPS navigation system. While not critical for the car to operate, they enhance functionality and provide additional features based on the driver's preferences.

Daemons are often identified by the letter d at the end of their program names, such as sshd (SSH daemon) or systemd. Just as a car relies on both its core components and optional features to provide a complete experience, a Linux system utilizes both system and user-installed services to function efficiently and meet user needs.

In general, there are just a few goals that we have when we deal with a service or a process:

- Start/Restart a service/process
- Stop a service/process
- See what is/was happening with a service/process
- Enable/Disable a service/process on boot
- Find a service/process

Most modern Linux distributions have adopted systemd as their initialization system (init system). It is the first process that starts during the boot process and is assigned the Process ID (PID). All processes in a Linux system are assigned a PID and can be viewed under the /proc/ directory, which contains information about each process. Processes may also have a Parent Process ID (PPID), indicating that they were started by another process (the parent), making them child processes.

### Most Commonly Used Signals

## Summary

This section explains **Service And Process Management**. It focuses on the main ideas and practical examples.

## What I Did

I read through the Hack The Box material, followed the examples, and reviewed the tools and steps shown in this section.

## What I Learned

I learned the basic ideas behind **Service And Process Management** and how they can help me investigate and respond to security activity.
