### Containerization

Containerization is the process of packaging and running applications in isolated environments, typically referred to as containers. These containers provide lightweight, consistent environments for applications to run, ensuring that they behave the same way, regardless of where they are deployed. Technologies like Docker, Docker Compose, and Linux Containers (LXC) make containerization possible, primarily in Linux-based systems. Containers differ from virtual machines in that they share the host system's kernel, making them far more lightweight and efficient. With these technologies, users can quickly create, deploy, and manage applications with improved security, portability, and scalability.

Containers are highly configurable, allowing users to tailor them to their specific needs, and their lightweight nature makes it easy to run multiple containers simultaneously on the same host system. This feature is particularly advantageous for scaling applications and managing complex microservice architectures.

Imagine you're organizing a big concert, and each band needs their own customized stage setup. Instead of building a completely new stage for each band (which would be like using a virtual machine), you create portable, self-contained "stage pods" that include everything the band needs lights, instruments, speakers, etc. These pods are lightweight, reusable, and can be easily moved from venue to venue. The key is that the pods all work seamlessly on the same main stage (the host system), but each one is isolated enough that no band's setup interferes with the others.

In the same way, containers package an application with all its required tools and settings, allowing it to run consistently across different systems without conflict, all while sharing the same "main stage" (the underlying system's resources).

Security is a critical aspect of containerization. Containers isolate applications from the host system and from each other, providing a barrier that reduces the risk of malicious activities affecting the host or other containers. This isolation, along with proper configuration and hardening techniques, adds an additional layer of security. However, it's important to note that containers do not offer the same level of isolation as traditional virtual machines. If not properly managed, vulnerabilities such as privilege escalation or container escapes can be exploited to gain unauthorized access to the host system or other containers.

In addition to enhanced security and resource efficiency, containers make applications easier to deploy, manage, and scale. Since containers encapsulate everything the application needs (e.g., libraries, dependencies), they allow for consistency across development, testing, and production environments. This portability ensures that applications run reliably across different environments.

However, it is important to recognize that, despite their advantages, containers are not immune to security risks. There are methods that we can use to escalate privileges or escape the isolation that containers provide.

## Dockers

Docker is an open-source platform for automating the deployment of applications as self-contained units called containers. It uses a layered filesystem and resource isolation features to provide flexibility and portability. Additionally, it provides a robust set of tools for creating, deploying, and managing applications, which helps streamline the containerization process.

Imagine Docker containers as a sealed lunchbox. You can eat the food (run applications) inside, but once you close the box (stop the container), everything resets. To make a new lunchbox (new container) with updated contents (modified configurations), you create a new recipe (Dockerfile) based on the original. When serving multiple lunchboxes in a restaurant (production), you'd use a kitchen system (Kubernetes/Docker Compose) to manage all the orders smoothly.

![[Pasted image 20260722102037.png]]

## Linux Containers

Linux Containers (LXC) is a lightweight virtualization technology that allows multiple isolated Linux systems (called containers) to run on a single host. LXC uses key resource isolation features, such as control groups (cgroups) and namespaces, to ensure that each container operates independently. Unlike traditional virtual machines, which require a full OS for each instance, containers share the host's kernel, making LXC more efficient in terms of resource usage.

LXC provides a comprehensive set of tools and APIs for managing and configuring containers, making it a popular choice for containerization on Linux systems. However, while LXC and Docker are both containerization technologies, they serve different purposes and have unique features.

Docker builds upon the idea of containerization by adding ease of use and portability, which has made it highly popular in the world of DevOps. Docker emphasizes packaging applications with all their dependencies in a portable "image", allowing them to be easily deployed across different environments. However, there are some differences between the two that can be distinguished based on the following categories:

![[Pasted image 20260722102124.png]]

As penetration testers, we often face situations where we need to test software or systems that have complex dependencies or configurations that are difficult to replicate on our local machines. This is where Linux containers become extremely useful. A Linux container is a lightweight, standalone package that includes everything needed to run a specific piece of software such as the code, libraries, and configuration files. Containers offer an isolated environment, allowing the software to run consistently across any Linux machine, regardless of the host system’s configuration.

Containers are particularly useful because they allow us to quickly create and run isolated environments tailored to our specific testing needs. For instance, if we need to test a web application that depends on a particular version of a database or web server, we can create a container with the exact versions and configurations we need. This eliminates the hassle of manually setting up these components on our machine, which can be time-consuming and prone to errors.

We can also use them to test exploits or malware in a controlled environment where we create a container that simulates a vulnerable system or network and then use that container to safely test exploits without risking damaging our machines or networks. However, it is important to configure LXC container security to prevent unauthorized access or malicious activities inside the container. This can be achieved by implementing several security measures, such as:

- Restricting access to the container
- Limiting resources
- Isolating the container from the host
- Enforcing mandatory access control
- Keeping the container up to date

LXC containers can be accessed using various methods, such as SSH or console. It is recommended to restrict access to the container by disabling unnecessary services, using secure protocols, and enforcing strong authentication mechanisms. For example, we can disable SSH access to the container by removing the openssh-server package or by configuring SSH only to allow access from trusted IP addresses. Those containers also share the same kernel as the host system, meaning they can access all the resources available on the system. We can use resource limits or quotas to prevent containers from consuming excessive resources. For example, we can use cgroups to limit the amount of CPU, memory, or disk space that a container can use.

### Securing LXC

Let us limit the resources to the container. In order to configure cgroups for LXC and limit the CPU and memory, a container can create a new configuration file in the /usr/share/lxc/config/<container name>.conf directory with the name of our container. For example, to create a configuration file for a container named linuxcontainer, we can use the following command:
## Summary

This section explains **Containerization**. It focuses on Dockers, Linux Containers.

## What I Did

I read through the Hack The Box material, followed the examples, and reviewed the tools and steps shown in this section.

## What I Learned

I learned the basic ideas behind **Containerization** and how they can help me investigate and respond to security activity.
