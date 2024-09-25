## 🖥️ Virtual Machine <a id="vm"></a>

### What is a Virtual Machine? <a id="vm-definition"></a>  
Let's start with the basics: **virtual machines (VMs)** are virtual environments created by software that simulate a complete additional operating system within your physical computer.  

Essentially, it's like having a **virtual computer inside your physical computer**. These virtual machines use a type of **virtualization software**, known as a **hypervisor**, to manage and share **hardware resources** such as CPU, memory, and storage across multiple VMs.

<p align="center">
    <img src="https://webimages.mongodb.com/_com_assets/cms/lh54s33za1fuqrg98-VM.jpg?auto=format%252Ccompress"/>
</p>

### Why use Virtual Machines? <a id="vm-purpose"></a>  
The major advantage of virtual machines is their ability to allow **multiple operating systems** and **applications** to run simultaneously on a single physical computer, as if they were separate and isolated computers. Each VM has its own **operating system**, **virtualized hardware** (including resources like **disk**, **memory**, and **network interfaces**), and functions **independently**. 

This flexibility allows for `better utilization of hardware resources`, ensuring that previously underused CPU, memory, and storage can be shared efficiently among different systems. Furthermore, because VMs are not tied to specific physical hardware, they provide `hardware independence`, which results in `cost savings`. You can run multiple systems or legacy software on the same machine, without needing to invest in new hardware.

Another significant benefit of virtual machines is the `greater control` they offer. They create a perfect environment for testing different software configurations, running **isolated servers**, and experimenting without affecting the rest of the system. This makes VMs ideal for **development** and **testing** environments, as well as for running applications in **secure, isolated** setups, increasing **security** since issues in one VM don’t spill over into others.

### Considerations <a id="vm-considerations"></a>  
However, it’s important to keep in mind that this isolation and virtualization can sometimes result in **performance impacts**, as the physical resources are shared among several virtual machines. Depending on the workload, running multiple VMs simultaneously can consume a significant amount of **memory** and **processing power**.

## 📟 Operating Systems <a id="os"></a>

### Operating System Definition <a id="os-definition"></a>  
**Operating systems** are fundamental software for the functioning of any computer or mobile device. They play the role of managing all the **hardware and software resources** of the system. This includes allocating **processing power**, **memory**, and controlling **input and output devices**, such as **disks** and **network interfaces**.

Additionally, operating systems offer different ways for users to interact with the system, such as **graphical user interfaces** (GUI) and **command-line interfaces** (CLI). These interfaces allow users to perform tasks, configure the system, and operate applications in an intuitive way or through more advanced commands. Among other essential functions, operating systems ensure **security**, efficient management of files and folders, and monitor the execution of processes.

### Difference Between Debian and CentOS <a id="debian-centos"></a>  
Although both are based on the Linux kernel, they have distinct philosophies and purposes:

- **Debian**: Focused on being flexible and committed to **free software**, Debian is widely used on both desktops and servers. It is known for its **stability** and offers different versions, ranging from the most stable to the most experimental. It is ideal for environments that prioritize **freedom of choice**, where **security** and stability are crucial.

- **CentOS**: Based on **Red Hat Enterprise Linux (RHEL)**, CentOS is more oriented towards enterprise environments that require a robust and **reliable** solution with a longer lifecycle. It is widely used in **corporate servers**, where the priority is **stability** and long-term support. With the recent shift to **CentOS Stream**, there is now a closer alignment with continuous updates and upstream development from RHEL.

## 🧰 Packaging Tool <a id="pack"></a>

When you need to install a program on your PC, something needs to take on the responsibility of installing, updating, configuring, and removing all the "packages" on your machine. This is where the **package manager** comes in, and in the case of **Debian**, the main ones are **APT** or **APTITUDE**. Although they have some differences, both perform this task efficiently and simplify software management on the system.

### APT - Advanced Packaging Tool <a id="apt"></a>  
**APT** (Advanced Packaging Tool) is a command-line toolset that allows you to install, update, and remove packages on Linux systems. It uses a list of software repositories to locate and download packages, automatically taking care of all the **dependencies**. Although it doesn’t have a graphical user interface (GUI), APT is extremely powerful and straightforward, giving users the ability to manage software efficiently. With it, you can ensure that installed packages are always up to date and functioning correctly.

### APTITUDE <a id="aptitude"></a>  
**APTITUDE** is a user interface for APT, offering both a graphical interface and a command-line interface for managing packages. APTITUDE is a more intuitive and user-friendly alternative for package management, with additional features such as more advanced package search capabilities, the ability to easily handle obsolete packages, and a simpler way to install **optional dependencies**.

## 🛡️ Security System <a id="ssystem"></a>

### Security Module <a id="smodule"></a>

A **Security Module** is a software extension that adds additional layers of control and protection to the operating system, working directly within the kernel. Modules like **AppArmor** and **SELinux** are designed to enforce security policies that strictly control how applications and processes interact with the system, offering more granular control over access permissions.

For example, **AppArmor** acts as a "policeman" within the system, checking programs against predefined security profiles. These profiles specify which resources and permissions each application can access, restricting access to sensitive files and preventing malicious programs from compromising the system's integrity. If an application is compromised, the damage is limited to the resources it was permitted to access.

These security modules are crucial for maintaining system protection, reinforcing access permissions, and ensuring that unauthorized actions are not executed. **AppArmor** comes pre-installed on Debian by default and can be checked using the following command:

```
sudo apparmor_status
```

### Password Policy <a id="password"></a>
### Firewall <a id="firewall"></a>
### SSH <a id="ssh"></a>
## ⛽ Logical Volume Manager <a id="lvm"></a>
## 🛤️ Automation <a id="automation"></a>
