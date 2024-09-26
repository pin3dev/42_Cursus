## ⤵️ Downloads & Install <a id="downloading"></a>

### 1. Downloading VirtualBox
* Go to this [link](https://www.virtualbox.org/wiki/Downloads)
* Download the virtualization software.

### 2. Downloading and Installing Debian

* Go to this [link](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/)
* Download the ISO file `debian-11.6.0-amd64-netinst.iso`
* Save the file in `/sgoinfre/goinfre/Perso/your_username`

> 🧠 What is an ISO Image?  
An ISO Image is a file that contains all the data from an optical disc. In this case, it holds the data for the Debian operating system.

### 3. Setting Up the Virtual Machine
* Open `VirtualBox` program
* Click on `New` to create a new VM
* Configure the settings as follows:
*  | FIELD | SETTING |  
   |------|---------------|  
   | Name | `Born2beroot` |  
   |Machine Folder | `/sgoinfre/goinfre/Perso/your_username` |
   | Type | `Linux` |
   | Version | `Debian (64-bit)` |
   | Memory Size (RAM) | `1024MB` |
   | Hard Disk | `Create a virtual hard disk now` |
   | Hard Disk File Type | `VDI (VirtualBox Disk Image)` |
   | Storage on Physical Hard Disk | `Dynamically allocated` |
   | File Location and Size | `8.1GB` or `30GB` |
* Click `Create`
* Click on the created VM
* Go to `Settings`
* Go to `Storage`
* Go to `Controller`
* Go to  `IDE`
* Select `Empty`
* Click the disk icon next to `Optical Drive`
* Choose `Choose a disk file`
* Select the ISO file you downloaded
* Click `OK`

### 4. Installing Debian OS
* Selected VM created
* Click on `Start`
* Select `Install` on the Debian installation screen
* Configure the settings as follows:
*  | FIELD | SETTING |  
   |-------|---------|  
   | Language | `American English` |  
   | Location | `Other`, `Europe`, `Portugal` |  
   | Keyboard | `UTF-8` |  
   | Hostname | `youruser42` |  
   | Domain Name | Leave it blank |
   | Root Password | `654321` |  
   | Non-administrative User Password | `654321` |  
   | Non-administrative Username | `youruser` |  
   | Clock | `Lisbon` |  
   | Partition Disk | `Guided - use entire disk and set up encrypted LVM`, `YES` |  
   | Select Disk | `SCI3 (0,0,0) (sda) - 8.10GB ATA VBOX HARDDISK` |  
   | Partitioning Scheme | `Separate /home, /var, and /tmp partitions` or `Separate /home partition` |  
   | Confirm Partition Configuration | `YES` |  
   | Erasing Data Warning | `Cancel` |  
   | Passphrase (Disk Encryption) | `yourstrongpassword` |  
   | Verify Passphrase | `yourstrongpassword` |  
   | Volume Group Size | Set it to the maximum available space |  
   | Finish Partitioning | `Finish partitioning and write changes to disk`, `YES` |  
   | Scan Additional CD | `NO` |  
   | Debian Mirror | `Portugal`, `deb.debian.org` |  
   | HTTP Proxy Information | Leave it blank |  
   | Automatic Submission of Usage Stats | `NO` |  
   | Software Installation | Deselect all options (no software selected) |  
   | GRUB Boot Loader Installation | `YES` |  
   | Device for Boot Loader | `/dev/sda (ATA VBOX HARDDISK)` |  
   | Finish Installation | `Continue` |  

### 5. Starting Debian

* Select `Debian GNU/Linux` on the boot screen
* Enter your disk encryption passphrase (`yourstrongpassword`)
* Log in with your user credentials:
*  | FIELD | SETTING |  
   |-------|---------|  
   | Username | `youruser` |  
   | Password | `654321` | 
* Open a terminal and run the command:
   ```
   lsblk
   ```
  > 🧠 What is `lsblk`?  
  The **`lsblk`** command displays information about all available block devices (disks), such as their size and mount points, in a tree format.

## ⚙️ Config Files <a id="config"></a>

### 1. **Installing SUDO:**
* Log in as the root user:  
  Option 1  
   ```bash
   su
   ```
  Option 2  
   ```bash
   su-
   ```
* Enter the root password: `654321`
* Check for available updates:
   ```bash
   apt-get update -y && apt-get upgrade -y
   ```
* Install `sudo`:
   ```bash
   apt install sudo
   ```
* Reboot the machine to apply changes:
   ```bash
   sudo reboot
   ```
* After the reboot, log in as the root user again:
   ```bash
   su-
   ```
* Verify that `sudo` was installed successfully:
   ```bash
   sudo -V
   ```
* Create a new `user` named `<youruser>` (this might give an error if the user was already created during Debian installation):
   ```bash
   sudo adduser <youruser>
   ```
* Create a new `group` called `<youruser42>`:
    ```bash
    sudo addgroup <youruser42>
    ```
* Check if the group `user42` was created correctly:  
    Option 1  
    ```bash
    getent group user42
    ```
    Option 2  
    ```bash
    cat /etc/group
    ```
* Add the user `ivbatist` to the `user42` group:  
    Option 1  
    ```bash
    sudo adduser ivbatist user42
    ```
    Option 2  
    ```bash
    usermod -aG user42 ivbatist
    ```
* Add the user `ivbatist` to the `sudo` group:
    ```bash
    sudo adduser ivbatist sudo
    ```
* Verify that the user has been added to both `sudo` and `user42` groups:
    ```bash
    getent group sudo
    getent group user42
    ```

#### Concept Explanations:

> 🧠 **Getent**:  
A utility that extracts important information from system databases (e.g., groups, users, etc.) in a simple and efficient way.

> 🧠 **Usermod**:  
A command-line utility that allows you to modify user account information.

> 🧠 **GID (Group ID)**:  
The numeric identifier assigned to a group. Each group in a Linux system is associated with a unique GID.


### 2. **Installing Git and VIM:**

* Install Git:
   ```bash
   apt-get install git -y
   ```
  > 💡 The `-y` flag automatically confirms the installation prompts.

* Verify Git Installation:
   ```bash
   git --version
   ```
   > 💡 This command will display the installed version of Git, confirming that the installation was successful.

* Install VIM (a powerful text editor):
   ```bash
   apt-get install vim
   ```

### 3. **Installing and Configuring SSH**

* Check for available updates:
   ```bash
   sudo apt update
   ```
* Install OpenSSH Server:
   ```bash
   sudo apt install openssh-server
   ```
* Press `Y` to confirm the installation when prompted.

* Check SSH Service Status:
   ```bash
   sudo service ssh status
   ```
    > 💡 This should return a status showing that the SSH service is active and running.

* Edit SSH Configuration to customize your SSH settings:  
  ```bash
   sudo vim /etc/ssh/sshd_config
   ```
* **Modify SSH Port**:
  | BEFORE | AFTER |
  |--------|-------|
  | `#Port 22` | `Port 4242` |
  | `#PermitRootLogin` | `PermitRootLogin no` | 
    > 💡 

* Save the changes and close the editor.

* Edit the Client SSH Configuration:  
   ```bash
   sudo vim /etc/ssh/ssh_config
   ```
* **Modify SSH Port for Clients**:
  | BEFORE | AFTER |
  |--------|-------|
  | `#Port 22` | `Port 4242` |
    > 💡 

* Restart the SSH Service to apply the changes:
    ```bash
    sudo service ssh restart
    ```
* Verify SSH Service to ensure the updates were applied:
    Option 1  
    ```bash
    sudo service ssh status
    ```
    Option 2  
    ```bash
    sudo grep Port /etc/ssh/ssh_config
    ```
    > 💡 You should see `Port 4242` as the active port

#### Concept Explanations:
  
> 🧠 **OpenSSH**:
An open-source implementation of the SSH protocol. It provides secure network operations by encrypting communication.

> 🧠 **ssh vs sshd**:  
> **SSH**: The client-side application that connects to the server.  
> **sshd**: The server-side daemon that manages incoming SSH connections.  


### 4. **Installing and Configuring UFW (Uncomplicated Firewall)**

* Enable UFW to start the firewall service:
   ```bash
   sudo ufw enable
   ```
    > 💡 Once enabled, you’ll see a message confirming that UFW is active.

* Install UFW (if not already installed):  
   Option 1  
   ```bash
   sudo apt-get install ufw
   ```
   Option 2  
   ```bash
   sudo apt install ufw
   ```
    > 💡 Press **Y** to confirm the installation.

* Allow connections on Port 4242 (or any custom port you've configured for SSH):
   ```bash
   sudo ufw allow 4242
   ```
    > 💡 This allows SSH connections through the specified port, ensuring you can still remotely access your server.

* Check UFW status to verify that the rules have been updated:
   ```bash
   sudo ufw status
   ```
    > 💡 This will display the current firewall rules, showing that port 4242 is now allowed for connections.

### 5. **Configuring Sudo Password Security Policy**

* Create the Sudo security configuration file for defining sudo password security policies:
   ```bash
   sudo touch /etc/sudoers.d/sudo_config
   ```

* Create a directory for logging Sudo commands, to store the logs of all commands executed with sudo privileges:
   ```bash
   sudo mkdir /var/log/sudo
   ```
* Edit the Sudo security configuration file:
   ```bash
   sudo vim /etc/sudoers.d/sudo_config
   ```
* Insert the following configuration settings code into the file to enforce security policies for sudo access:
   ```bash
   Defaults  passwd_tries=3
   Defaults  badpass_message="YOUR ERROR MSG HERE"
   Defaults  logfile="/var/log/sudo/sudo_config"
   Defaults  log_input, log_output
   Defaults  iolog_dir="/var/log/sudo"
   Defaults  requiretty
   Defaults  secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
   ```
   #### Configuration Explanations:

   > ✒️ **passwd_tries**:  
    Limits the number of incorrect password attempts to 3.  
   > ✒️ **badpass_message**:  
    Displays a custom message when an incorrect password is entered.  
   > ✒️ **logfile**:  
    Specifies the log file where all sudo command activity will be recorded.  
   > ✒️ **log_input, log_output**:  
    Logs both input and output of sudo commands for auditing purposes.  
   > ✒️ **iolog_dir**:  
    Defines the directory for storing input/output logs.  
   > ✒️ **requiretty**:  
    Ensures that sudo commands are only executed from a terminal.  
   > ✒️ **secure_path**:  
    Defines the path for secure access to system binaries and prevents malicious programs from overriding important commands. 

* Save the changes and close the editor.
  
    > 💡 Once you've added the configuration, save the file and exit the editor. This will apply the password policy and command logging for all sudo activities.
 

### 6. **Configuring Non-Admin Password Security Policy**

* Edit the Login configuration file `login.defs`:
   ```bash
   sudo vim /etc/login.defs
   ```
* **Locate and Modify Password Settings**:
  | BEFORE | AFTER |
  |--------|-------|
  | `PASS_MAX_DAYS 9999` | `PASS_MAX_DAYS 30` |
  | `PASS_MIN_DAYS 0` | `PASS_MIN_DAYS 2` |
  | `PASS_WARN_AGE 7` | `PASS_WARN_AGE 7` |

   #### Configuration Explanations:

   > ✒️ **PASS_MAX_DAYS**:  
    Maximum password age (days) before expiration is 30 days.  
   > ✒️ **PASS_MIN_DAYS**:  
    Minimum days before a password can be changed is 2 days.  
   > ✒️ **PASS_WARN_AGE**:  
    Warns the user 7 days before password expiration..  

* Install the PAM password quality library:
   ```bash
   sudo apt-get install libpam-pwquality
   ```
  > 💡 The `-y` flag automatically confirms the installation prompts.

* Edit the PAM password security configuration file:
   ```bash
   sudo vim /etc/pam.d/common-password
   ```
* Locate the password configuration line:  
     Option 1  
     ```bash
     password  requisite  pam_deny.so
     ```  
     Option 2  
     ```bash
      password  requisite  pam_deny.so retry=3
     ``` 
* Add the password security rules to enforce strict password requirements:
   ```bash
   minlen=10
   ucredit=-1
   dcredit=-1
   lcredit=-1
   maxrepeat=3
   reject_username
   difok=7
   enforce_for_root
   ```

   #### Configuration Explanations:

   > ✒️ **minlen**:  
    Minimum password length of 10 characters.  
   > ✒️ **ucredit**:  
    Requires at least one uppercase letter.  
   > ✒️ **dcredit**:  
    Requires at least one digit.  
   > ✒️ **lcredit**:  
    Requires at least one lowercase letter.  
   > ✒️ **maxrepeat**:  
    Limits repeating characters to a maximum of 3.  
   > ✒️ **reject_username**:  
    Prevents the username from being used in the password.  
   > ✒️ **difok**:  
    Requires at least 7 different characters in the new password.  
   > ✒️ **enforce_for_root**:  
    Enforces these rules for the root user as well.  

* Update current user password:  
   Option 1
   ```bash
   passwd
   ```  
   Option 2
   ```bash
   sudo passwd USER_NAME
   ```

### 7. **Connecting Virtual Machine to Physical Machine via SSH**
   * Open VirtualBox and select the virtual machine you want to connect to, in this case, `Born2beroot`.
   * Go to `Settings`
   * Go to `Network`
   * Go to `Adapter 1`
   * Change the `Attached to` setting to `Bridged Adapter`
> 💡 This will allow the VM to use the same network as the host machine.
   * Proceed to `Advanced`
   * Click on `Port Forwarding`
   * **Add a new rule**:
     | FIELD | VALUE |
     |--------|-------|
     | Name | `Rule 1` |
     | Protocol | `TCP` |
     | Host IP | Leave it blank |
     | Host Port | `4242` |
     | Guest IP | Leave it blank |
     | Guest Port | `4242` |
   
  > 💡 

   * Restart the SSH service on the virtual machine:
      ```bash
      sudo systemctl restart ssh
      sudo service sshd status
      ```
   * Check the VM’s IP address:
      ```bash
      ip address
      ```
   > 💡 Note the IP address that appears after **inet**, for example: `inet 10.11.249.26`.  
   * Open the terminal on the physical machine (host) and connect to the virtual machine:
      ```bash
      ssh youruser@10.11.249.26 -p 4242
      ```
   > 💡 Replace `youruser` with the username of your virtual machine.  
   > 💡 The `10.11.249.26` is the IP of your virtual machine (the number may vary depending on your network).  
   > 💡 The `-p 4242` specifies the custom port you configured for SSH.  
     

### 8. **Monitoring Script**
* Navigate to the directory where the monitoring script will be created:
   ```bash
   cd /usr/local/bin
   ```

* Create and open the script file:
   ```bash
   sudo vim monitoring.sh
   ```

* Insert the following script:
   ```bash
   #!/bin/bash
   
   # Architecture
   arch=$(uname -a)
   
   # Physical CPUs
   cpuf=$(grep "physical id" /proc/cpuinfo | wc -l)
   
   # Virtual CPUs
   cpuv=$(grep "processor" /proc/cpuinfo | wc -l)
   
   # RAM
   ram_total=$(free --mega | awk '$1 == "Mem:" {print $2}')
   ram_use=$(free --mega | awk '$1 == "Mem:" {print $3}')
   ram_percent=$(free --mega | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}')
   
   # Disk
   disk_total=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_t += $2} END {printf ("%.1fGb\n"), disk_t/1024}')
   disk_use=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_u += $3} END {print disk_u}')
   disk_percent=$(df -m | grep "/dev/" | grep -v "/boot" | awk '{disk_u += $3} {disk_t+= $2} END {printf("%d"), disk_u/disk_t*100}')
   
   # CPU Load
   cpul=$(vmstat 1 2 | tail -1 | awk '{printf $15}')
   cpu_op=$(expr 100 - $cpul)
   cpu_fin=$(printf "%.1f" $cpu_op)
   
   # Last Boot
   lb=$(who -b | awk '$1 == "system" {print $3 " " $4}')
   
   # LVM Use
   lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)
   
   # TCP Connections
   tcpc=$(ss -ta | grep ESTAB | wc -l)
   
   # Logged-in Users
   ulog=$(users | wc -w)
   
   # Network Information
   ip=$(hostname -I)
   mac=$(ip link | grep "link/ether" | awk '{print $2}')
   
   # Sudo Commands Executed
   cmnd=$(journalctl _COMM=sudo | grep COMMAND | wc -l)
   
   # Output the information
   wall "   Architecture: $arch
       CPU physical: $cpuf
       vCPU: $cpuv
       Memory Usage: $ram_use/${ram_total}MB ($ram_percent%)
       Disk Usage: $disk_use/${disk_total} ($disk_percent%)
       CPU load: $cpu_fin%
       Last boot: $lb
       LVM use: $lvmu
       Connections TCP: $tcpc ESTABLISHED
       User log: $ulog
       Network: IP $ip ($mac)
       Sudo: $cmnd cmd"
   ```
   
   #### Configuration Explanations:
   > ✒️ **grep**:  
    Searches for a pattern in a file and displays all lines that contain that pattern.  
      `-v`: Displays all lines that do NOT contain the pattern.  
   > ✒️ **wc**:  
    Used for counting lines, words, and characters in a file.  
      `-l`: Counts the number of lines in the file.  
   > ✒️ **uname**:  
    Displays information about the operating system.  
      `-a`: Shows all available system information.    
   > ✒️ **df**:  
    Shows the amount of available disk space on mounted filesystems.  
      `-h`: Displays sizes in a human-readable format.    
      `-m`: Displays sizes in megabytes.    
   > ✒️ **vmstat**:  
    Reports information about processes, memory, paging, block I/O, and CPU activity.  
   > ✒️ **journalctl**:  
    Retrieves logs from the system, including sudo command logs.  

   > 💡 This script will monitor system architecture, CPU usage, memory, disk usage, TCP connections, and other details, and display the results every 10 minutes.  

* Save the changes and close the editor.

* Make the script executable:
   ```bash
   sudo chmod +x /usr/local/bin/monitoring.sh
   ```

* Test the script manually to verify that it works:
   ```bash
   sudo ./monitoring.sh
   ```

### 9. **Configuring Crontab**

* Set up a cron job at regular intervals (every 10 minutes)**:
   ```bash
   sudo crontab -u root -e
   ```

* Add the cron job to run the script every 10 minutes, at the end of the crontab file:
   ```bash
   */10 * * * * sleep $(who -b | awk -F: '{printf("%d"), $2%10}') && sh /home/ivbatist/monitoring.sh
   ```

   #### Configuration Explanations:
   > ✒️ **`*/10 * * * *`**:  
    Instructs the task to run every 10 minutes.  
   > ✒️ **`sleep $(who -b | awk -F: '{printf("%d"), $2%10}')`**:  
    Adds a delay based on the system's last boot time to prevent all tasks from running at the exact same time.  
   > ✒️ **`sh /home/ivbatist/monitoring.sh`**:  
    Specifies the command to execute, which in this case is the `monitoring.sh` script located at `/home/ivbatist/`.  

* Save the changes and close the editor.


* Verify if the task is registered correctly:
     ```bash
     sudo crontab -l
     ```
   > 💡 This will display all scheduled tasks for the **root** user, and you should see the line you just added.

   > 💡 Now, every 10 minutes, the `monitoring.sh` script will be executed automatically as per the crontab configuration.

### 10. **Closing UDP Port 68**

* Check if UDP Port 68 is Open**:
     ```bash
     ss -tunlp
     ```
   > 💡 This command lists all open TCP/UDP ports and their associated processes. Look for port **68/UDP** to confirm if it's open.

* Finding your IP and broadcast address:
     ```bash
     ip address
     ```
   > 💡 Look for your interface (usually **eth0** or **enp0s3**) and note the **inet** IP (e.g., `10.11.249.26/16`) and **brd** (broadcast) address.

* Check your network interface details:
     ```bash
     ip a
     ```
   > 💡 This will give you the details of all network interfaces on your system.

* Edit network configuration to set a static IP:
     ```bash
     sudo vim /etc/network/interfaces
     ```
   > 💡 In the configuration file, locate the line that configures the interface to use **DHCP** (Dynamic Host Configuration Protocol).

* **Modify DHCP to Static**:
  | BEFORE | AFTER |
  |--------|-------|
  | `iface eth0 inet DHCP` | `iface eth0 inet static` |
  | `address {your_ip_address}` | `address 10.11.249.26` |
  | `netmask {your_netmask}` | `netmask 255.255.0.0` |
  | `gateway {your_broadcast_address}` | `gateway 10.11.255.255` |

* Restart the network services:
     ```bash
     sudo systemctl restart networking
     ```

* Verify the port status, Check again whether `UDP port 68` is closed:
     ```bash
     ss -tunlp
     ```

   > 💡 By following these steps, you will close **UDP port 68**, often associated with DHCP, and configure a static IP for your machine. This is particularly useful for securing your system and preventing unwanted network configuration changes.
