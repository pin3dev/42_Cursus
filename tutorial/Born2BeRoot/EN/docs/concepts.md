## 🖥️ Virtual Machine <a id="vm"></a>

### What is a Virtual Machine?
Let's start with the basics: **virtual machines (VMs)** are virtual environments created by software that simulate a complete additional operating system within your physical computer.  

Essentially, it's like having a **virtual computer inside your physical computer**. These virtual machines use a type of **virtualization software**, known as a **hypervisor**, to manage and share **hardware resources** such as CPU, memory, and storage across multiple VMs.

<p align="center">
    <img src="https://webimages.mongodb.com/_com_assets/cms/lh54s33za1fuqrg98-VM.jpg?auto=format%252Ccompress"/>
</p>

### Why use Virtual Machines?
The major advantage of virtual machines is their ability to allow **multiple operating systems** and **applications** to run simultaneously on a single physical computer, as if they were separate and isolated computers. Each VM has its own **operating system**, **virtualized hardware** (including resources like **disk**, **memory**, and **network interfaces**), and functions **independently**. 

This flexibility allows for `better utilization of hardware resources`, ensuring that previously underused CPU, memory, and storage can be shared efficiently among different systems. Furthermore, because VMs are not tied to specific physical hardware, they provide `hardware independence`, which results in `cost savings`. You can run multiple systems or legacy software on the same machine, without needing to invest in new hardware.

Another significant benefit of virtual machines is the `greater control` they offer. They create a perfect environment for testing different software configurations, running **isolated servers**, and experimenting without affecting the rest of the system. This makes VMs ideal for **development** and **testing** environments, as well as for running applications in **secure, isolated** setups, increasing **security** since issues in one VM don’t spill over into others.

### Considerations  
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

- **APT** (Advanced Packaging Tool): It is a command-line toolset that allows you to install, update, and remove packages on Linux systems. It uses a list of software repositories to locate and download packages, automatically taking care of all the **dependencies**. Although it doesn’t have a graphical user interface (GUI), APT is extremely powerful and straightforward, giving users the ability to manage software efficiently. With it, you can ensure that installed packages are always up to date and functioning correctly.

- **APTITUDE**: It is a user interface for APT, offering both a graphical interface and a command-line interface for managing packages. APTITUDE is a more intuitive and user-friendly alternative for package management, with additional features such as more advanced package search capabilities, the ability to easily handle obsolete packages, and a simpler way to install **optional dependencies**.

## 🛡️ Security System <a id="ssystem"></a>

### Security Module <a id="smodule"></a>

A **Security Module** is a software extension that adds additional layers of control and protection to the operating system, working directly within the kernel. Modules like **AppArmor** and **SELinux** are designed to enforce security policies that strictly control how applications and processes interact with the system, offering more granular control over access permissions.

For example, **AppArmor** acts as a "policeman" within the system, checking programs against predefined security profiles. These profiles specify which resources and permissions each application can access, restricting access to sensitive files and preventing malicious programs from compromising the system's integrity. If an application is compromised, the damage is limited to the resources it was permitted to access.

These security modules are crucial for maintaining system protection, reinforcing access permissions, and ensuring that unauthorized actions are not executed. **AppArmor** comes pre-installed on Debian by default and can be checked using the following command:

```
sudo apparmor_status
```

### Password Policy <a id="password"></a>

A **Password Policy** is a set of rules that defines the requirements a password must meet, such as minimum length, complexity, validity, and reuse. The primary goal of these policies is to ensure that the passwords used in the system are strong enough to withstand brute-force attacks or guessing attempts. A Password Policy may include, for example, the requirement for uppercase letters, numbers, special characters, and the prohibition of using common passwords.

However, as with everything in life, there are disadvantages. Highly complex passwords can be difficult to remember, which may lead users to adopt insecure "solutions," such as writing down passwords in places where others can access them, thus making them more vulnerable.

In the **Debian** system, the password policy is managed by **PAM** (Pluggable Authentication Modules), which is a **Security Module** responsible for defining authentication rules, including password complexity. These policies can be adjusted by the administrator in the `common-password` file. **PAM** provides the flexibility to apply different levels of control over authentication and password usage, allowing the system to have personalized policies that balance security and usability.

### Firewall <a id="firewall"></a>

Uncomplicated Firewall, also known as UFW, is a firewall tool that analyzes the traffic between your PC and the internet, allowing or blocking incoming and outgoing traffic. There are many types of firewalls, with varying levels of complexity, but UFW stands out for its simplicity.

UFW is a command-line tool based on iptables, a powerful firewall tool for Linux systems. However, UFW simplifies the process of creating new rules, which is extremely useful for beginners who might find iptables complicated.

One interesting feature of UFW is how easily it allows configuring access from a virtual machine through the physical machine, which will be a very useful feature for our project. This makes it a popular choice for those who need a quick and efficient solution to manage network traffic.

### SSH <a id="ssh"></a>

Secure Shell (SSH) is a network protocol that allows secure and encrypted communication between two systems, such as between a computer and a remote server. SSH is widely used to securely access, manage, and transfer files between systems, ensuring that confidential information is not intercepted or stolen during transmission.

The main advantage of SSH lies in its security. It uses strong encryption to protect the data transmitted between systems, which means that even if someone intercepts the connection, they won't be able to access the transmitted information. This makes SSH a fundamental choice for those who need to securely access systems remotely.

Additionally, SSH allows authentication via passwords or encryption keys, adding an extra layer of security. This type of authentication is particularly important for preventing unauthorized access, making SSH one of the most secure and efficient solutions for managing remote servers and systems.

## ⛽ Logical Volume Manager <a id="lvm"></a>

**LVM (Logical Volume Manager)** helps manage storage space on Linux in a more flexible way. It allows resizing and moving disk partitions, or even combining multiple physical disks into a single logical volume, without interrupting the system's operation. Partitions, in this context, are digital divisions of the storage unit (whether HDD or SSD) that organize memory into separate blocks. Each block can have specific user control and other functionalities, such as separating the operating system (OS) from personal files.

<p align="center">
    <img src="https://contabo.com/blog/wp-content/uploads/2023/03/image.png.webp"/>
</p>

The foundation of the LVM scheme begins with the **PV (Physical Volume)**, which represents the physical disks (HDDs or SSDs) where the data will be effectively stored. These PVs are the fundamental building blocks of storage.

The **VG (Volume Group)**, or volume groups, are combinations of multiple PVs, forming a storage "pool." This pool can be expanded indefinitely by adding more PVs. In summary, the VG is the sum of the capacity of all PVs, creating a storage space that can grow as needed.

Within the VGs, we have **LV (Logical Volume)**, or logical volumes, which are created to manage the data as if it were a single continuous volume. Even though the data may be distributed physically in different locations, LVM makes it appear as if it is stored continuously. These logical volumes act as virtual partitions, offering greater flexibility and control over storage space.

For example, if your storage begins to fill up, you can easily add more space, much like extending a drawer in a cabinet without needing to dismantle it. This makes **LVM**, although it may seem advanced, a practical and efficient solution, especially when dealing with large volumes of data or when the storage structure needs to be adjusted over time.


## 🛤️ Automation <a id="automation"></a>

**Crontab** is a utility that allows users to schedule tasks to be executed at specific times. It edits the configuration file where you define the commands to be executed and the time of execution. **Cron**, on the other hand, is the service that monitors this file and ensures that the scheduled tasks are performed at the right time.

This system is widely used to automate repetitive tasks, such as **database backups**, **software updates**, or **temporary file cleanup**. With **Crontab**, you can configure schedules using a specific syntax, where you define the execution time (such as minutes, hours, days, weeks, or months) and the command to be executed. For example, you can schedule a task to run every day at 5 AM, ensuring that the system does something important, like cleaning logs or updating packages.

It’s important to note that tasks scheduled with **Crontab** are executed under the user who configured them. Therefore, these tasks have the same access permissions as the user, meaning that if you schedule a file backup, it will only have access to the files that your user can access.
