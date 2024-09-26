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

> 🧠 **Sudo**:  
Sudo is a program for Unix-like operating systems that allows users to run commands with the security privileges of superuser (root).  
It allows a regular user to perform tasks that typically require administrator (root) privileges without needing to log in directly as root.

> 🧠 **APT**:  
APT (Advanced Package Tool) is a free software user interface for installing and removing software on Debian-based Linux distributions. It handles package installations and dependencies.

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
* **Modify SSH Port:**
   - Locate the line:  
     `#Port 22`
   - **Uncomment** the line by removing the `#` and change it to:  
     `Port 4242`

6. **Disable Root Login via SSH:**
   - Find the line:  
     `#PermitRootLogin`
   - **Uncomment** it and change it to:  
     `PermitRootLogin no`

7. **Save the Changes** and close the editor.

8. **Edit the Client SSH Configuration** (optional):
   ```bash
   sudo vim /etc/ssh/ssh_config
   ```
   or
   ```bash
   sudo nano /etc/ssh/ssh_config
   ```

9. **Modify SSH Port for Clients:**
   - Locate the line:  
     `#Port 22`
   - **Uncomment** it and change it to:  
     `Port 4242`

10. **Restart the SSH Service** to apply the changes:
    ```bash
    sudo service ssh restart
    ```

11. **Verify SSH Service** to ensure the updates were applied:
    ```bash
    sudo service ssh status
    ```
    or:
    ```bash
    sudo grep Port /etc/ssh/ssh_config
    ```
    You should see **Port 4242** as the active port.

### Concept Explanations:

- **SSH**: A cryptographic network protocol used for secure communications over an insecure network. It's primarily used for remote login into other systems securely.
  
- **OpenSSH**: An open-source implementation of the SSH protocol. It provides secure network operations by encrypting communication.

- **ssh vs. sshd**:  
  - **SSH**: The client-side application that connects to the server.
  - **sshd**: The server-side daemon that manages incoming SSH connections.


### 4. **Installing and Configuring UFW (Uncomplicated Firewall)**

1. **Enable UFW** to start the firewall service:
   ```bash
   sudo ufw enable
   ```
   Once enabled, you’ll see a message confirming that UFW is active.

2. **Install UFW** (if not already installed) with one of the following commands:
   ```bash
   sudo apt-get install ufw
   ```
   or
   ```bash
   sudo apt install ufw
   ```
   Press **Y** to confirm the installation.

3. **Allow Connections on Port 4242** (or any custom port you've configured for SSH):
   ```bash
   sudo ufw allow 4242
   ```
   This allows SSH connections through the specified port, ensuring you can still remotely access your server.

4. **Check UFW Status** to verify that the rules have been updated:
   ```bash
   sudo ufw status
   ```
   This will display the current firewall rules, showing that port 4242 is now allowed for connections.

### Concept Explanations:

- **UFW (Uncomplicated Firewall):** A simple command-line firewall management tool for managing iptables in Linux. It allows users to easily configure and manage their firewall rules to permit or block network traffic.

- **Firewall:** A security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules. It serves as a barrier between a trusted internal network and untrusted external networks (such as the internet).


### 5. **Configuring Sudo Password Security Policy**

1. **Create the Sudo Security Configuration File**:
   Use the following command to create a new configuration file for defining sudo password security policies:
   ```bash
   sudo touch /etc/sudoers.d/sudo_config
   ```

2. **Create a Directory for Logging Sudo Commands**:
   Create a directory to store the logs of all commands executed with sudo privileges:
   ```bash
   sudo mkdir /var/log/sudo
   ```

   <aside>
   <img src="/icons/checkmark_green.svg" alt="/icons/checkmark_green.svg" width="40px" /> **Project Rules:**
   Ensure that logging and policy enforcement adhere to your project guidelines.
   </aside>

3. **Edit the Sudo Security Configuration File**:
   Open the newly created file with your preferred text editor:
   ```bash
   sudo nano /etc/sudoers.d/sudo_config
   ```
   or
   ```bash
   sudo vim /etc/sudoers.d/sudo_config
   ```

4. **Insert the Following Code into the File**:
   Add the following configuration settings to enforce security policies for sudo access:

   ```bash
   Defaults  passwd_tries=3
   Defaults  badpass_message="Ta com dedo podre? Tenta de novo!Mensaje de error personalizadoMensaje de error personalizadoMensaje de error personalizadoMensaje de error personalizados"
   Defaults  logfile="/var/log/sudo/sudo_config"
   Defaults  log_input, log_output
   Defaults  iolog_dir="/var/log/sudo"
   Defaults  requiretty
   Defaults  secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
   ```

   ### Explanation of Configuration:

   - **passwd_tries=3**: Limits the number of incorrect password attempts to 3.
   - **badpass_message**: Displays a custom message when an incorrect password is entered.
   - **logfile**: Specifies the log file where all sudo command activity will be recorded.
   - **log_input, log_output**: Logs both input and output of sudo commands for auditing purposes.
   - **iolog_dir**: Defines the directory for storing input/output logs.
   - **requiretty**: Ensures that sudo commands are only executed from a terminal.
   - **secure_path**: Defines the path for secure access to system binaries and prevents malicious programs from overriding important commands.

5. **Save and Exit**:
   Once you've added the configuration, save the file and exit the editor. This will apply the password policy and command logging for all sudo activities.


### 6. **Configuring Non-Admin Password Security Policy**

1. **Edit the Login Configuration File**:
   Use the following command to open the `login.defs` file for editing:
   ```bash
   sudo vim /etc/login.defs
   ```

2. **Locate and Modify Password Settings**:
   Find the following lines in the file:
   - `PASS_MAX_DAYS 9999`
   - `PASS_MIN_DAYS 0`
   - `PASS_WARN_AGE 7`

   Modify the settings as follows:
   - `PASS_MAX_DAYS 30` → Maximum password age (days) before expiration is 30 days.
   - `PASS_MIN_DAYS 2` → Minimum days before a password can be changed is 2 days.
   - Keep `PASS_WARN_AGE 7` unchanged, which warns the user 7 days before password expiration.

   <aside>
   <img src="/icons/checkmark_green.svg" alt="/icons/checkmark_green.svg" width="40px" /> **Project Rules:**
   This configuration ensures compliance with the project's security policy for password expiration.
   </aside>

3. **Install the PAM Password Quality Library**:
   Use this command to install the PAM (Pluggable Authentication Module) password quality library:
   ```bash
   sudo apt-get install libpam-pwquality
   ```

4. **Confirm the Installation**:
   Type `y` when prompted to confirm the installation.

5. **Edit the PAM Password Security Configuration**:
   Open the common password file to configure password policies:
   ```bash
   sudo nano /etc/pam.d/common-password
   ```
   or
   ```bash
   sudo vim /etc/pam.d/common-password
   ```

6. **Locate the Password Configuration Line**:
   Find the line that looks like this:
   - `password  requisite  pam_deny.so` 
   - or `password  requisite  pam_deny.so retry=3`

7. **Add the Following Password Security Rules**:
   Insert the following configuration to enforce strict password requirements:

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

   ### Explanation of Configuration:
   - **minlen=10**: Minimum password length of 10 characters.
   - **ucredit=-1**: Requires at least one uppercase letter.
   - **dcredit=-1**: Requires at least one digit.
   - **lcredit=-1**: Requires at least one lowercase letter.
   - **maxrepeat=3**: Limits repeating characters to a maximum of 3.
   - **reject_username**: Prevents the username from being used in the password.
   - **difok=7**: Requires at least 7 different characters in the new password.
   - **enforce_for_root**: Enforces these rules for the root user as well.

8. **Update User Password**:
   To change the password of the current user:
   ```bash
   passwd
   ```

   Or to change another user's password:
   ```bash
   sudo passwd USER_NAME
   ```

   <aside>
   <img src="/icons/checkmark_green.svg" alt="/icons/checkmark_green.svg" width="40px" /> **Project Rules:**
   This configuration ensures strong password policies are applied to all users, including root.
   </aside>


### 7. **Conectando a máquina virtual com a máquina física via SSH**

#### 1. Configuração no VirtualBox:
   1. **Abra o VirtualBox** e selecione a máquina virtual que deseja conectar (neste caso, "Born2beroot").
   2. Vá para **Settings (Configurações)** → **Network (Rede)** → **Adapter 1 (Adaptador 1)**.
   3. **Mude o Attached to (Conectado a)** para "Bridged Adapter (Adaptador em ponte)". Isso permitirá que a VM use a mesma rede da máquina host.
   4. **Avance para "Advanced"** e clique em **Port Forwarding (Encaminhamento de porta)**.
   5. **Adicione uma nova regra**:
      - **Name:** “Rule 1”
      - **Protocol:** “TCP”
      - **Host IP:** Deixe em branco.
      - **Host Port:** “4242”
      - **Guest IP:** Deixe em branco.
      - **Guest Port:** “4242”

#### 2. Configuração na máquina real:
   1. ***OPCIONAL:*** Para garantir que o SSH está funcionando corretamente, você pode reiniciar o serviço de SSH na máquina virtual:
      ```bash
      sudo systemctl restart ssh
      sudo service sshd status
      ```
   2. **Na máquina virtual**: execute o seguinte comando para verificar o endereço IP da VM:
      ```bash
      ip address
      ```
      Anote o endereço IP que aparece após **inet**, como por exemplo: `inet 10.11.249.26`.
   
   3. **Na máquina física**:
      Abra o terminal da máquina física (host) e conecte-se à máquina virtual usando o comando `ssh`:
      ```bash
      ssh ivbatist@10.11.249.26 -p 4242
      ```
      - Substitua **ivbatist** pelo nome do usuário da sua máquina virtual.
      - O **10.11.249.26** é o IP da sua máquina virtual (o número será diferente dependendo da sua rede).
      - O **-p 4242** especifica a porta customizada que você configurou para o SSH.


### 8. **Creating and Configuring the Monitoring Script**
1. **Navigate to the directory**:
   First, navigate to the directory where the monitoring script will be created:
   ```bash
   cd /usr/local/bin
   ```

2. **Create and open the script file**:
   Create and open the monitoring script for editing. Use `vim` or `nano`:
   ```bash
   sudo vim monitoring.sh
   ```

#### 🧠 **Project Rules:**

![Project Image](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9203fb49-9a44-4181-a80d-bbc967b6f26a/WhatsApp_Image_2023-01-25_at_08.14.02.jpg)

![Another Project Image](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2f24d310-2f92-4dee-b870-63de8489e0b3/(Born2beRoot)_en.subject_page-0009.jpg)


3. **Insert the following script**:
   Copy and paste the script below into the `monitoring.sh` file:

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

---

#### 🧠 **Explanation of Commands:**

- **grep**: Searches for a pattern in a file and displays all lines that contain that pattern.
  - `-v`: Displays all lines that do NOT contain the pattern.

- **wc**: Used for counting lines, words, and characters in a file.
  - `-l`: Counts the number of lines in the file.

- **uname**: Displays information about the operating system.
  - `-a`: Shows all available system information.

- **df**: Shows the amount of available disk space on mounted filesystems.
  - `-h`: Displays sizes in a human-readable format.
  - `-m`: Displays sizes in megabytes.

- **vmstat**: Reports information about processes, memory, paging, block I/O, and CPU activity.
  
- **journalctl**: Retrieves logs from the system, including sudo command logs.

4. **Save and exit**:
   After pasting the script, save and exit the file.

5. **Make the script executable**:
   To ensure the script can be executed, run the following command to make it executable:
   ```bash
   sudo chmod +x /usr/local/bin/monitoring.sh
   ```

6. **Test the script**:
   You can run the script manually to verify that it works:
   ```bash
   sudo ./monitoring.sh
   ```

7. **Set up a cron job**:
   To run this script at regular intervals (every 10 minutes), edit the root crontab:
   ```bash
   sudo crontab -u root -e
   ```

8. **Add the cron job**:
   Add the following line to run the script every 10 minutes:
   ```bash
   */10 * * * * /usr/local/bin/monitoring.sh
   ```

This script will monitor system architecture, CPU usage, memory, disk usage, TCP connections, and other details, and display the results every 10 minutes.





### 9. **Configuring Crontab**

#### 1. **Accessing the Crontab for the Root User**:
   - In the terminal, run the following command to open the **crontab** configuration file for the **root** user:
     ```bash
     sudo crontab -u root -e
     ```
   - This will open the crontab editor where you can schedule tasks for the root user.

#### 2. **Adding a New Scheduled Task**:
   - Add the following line at the end of the crontab file:
     ```bash
     */10 * * * * sleep $(who -b | awk -F: '{printf("%d"), $2%10}') && sh /home/ivbatist/monitoring.sh
     ```
   - This line does the following:
     - **`*/10 * * * *`**: Instructs the task to run every 10 minutes.
     - **`sleep $(who -b | awk -F: '{printf("%d"), $2%10}')`**: Adds a delay based on the system's last boot time to prevent all tasks from running at the exact same time.
     - **`sh /home/ivbatist/monitoring.sh`**: Specifies the command to execute, which in this case is the `monitoring.sh` script located at `/home/ivbatist/`.

#### 3. **Saving and Exiting the Crontab**:
   - After adding the line, save the file and exit the editor (usually using `:wq` in **vim** or **Ctrl + X** in **nano**).

#### 4. **Verifying the Task is Registered Correctly**:
   - To verify that the task has been successfully added to the **crontab**, run the following command:
     ```bash
     sudo crontab -l
     ```
   - This will display all scheduled tasks for the **root** user, and you should see the line you just added.

Now, every 10 minutes, the `monitoring.sh` script will be executed automatically as per the crontab configuration.

#### 🧠 **Crontab**: A scheduling utility in Unix-based systems that allows users to run scripts or commands at specified intervals. It works by using a cron daemon to periodically check the scheduled tasks and execute them.


### 10. **Closing UDP Port 68**

#### 1. **Checking if UDP Port 68 is Open**:
   - Run the following command to check if **UDP port 68** is open on your system:
     ```bash
     ss -tunlp
     ```
   - This command lists all open TCP/UDP ports and their associated processes. Look for port **68/UDP** to confirm if it's open.

#### 2. **Finding Your IP and Broadcast Address**:
   - Use the following command to display your IP address and other network details:
     ```bash
     ip address
     ```
   - Look for your interface (usually **eth0** or **enp0s3**) and note the **inet** IP (e.g., `10.11.249.26/16`) and **brd** (broadcast) address.

#### 3. **Checking Your Network Interface Details**:
   - Run this command to confirm your network interface details:
     ```bash
     ip a
     ```
   - This will give you the details of all network interfaces on your system.

#### 4. **Editing Network Configuration to Set a Static IP**:
   - Open the network configuration file for editing:
     ```bash
     sudo vim /etc/network/interfaces
     ```
   - In the configuration file, locate the line that configures the interface to use **DHCP** (Dynamic Host Configuration Protocol).

#### 5. **Changing DHCP to Static**:
   - Replace the **DHCP** setting with **static**, like this:
     ```bash
     iface eth0 inet static
         address {your_ip_address}
         netmask {your_netmask}
         gateway {your_broadcast_address}
     ```
   - Replace `{your_ip_address}` with your actual IP address (e.g., `10.11.249.26`), `{your_netmask}` with the appropriate netmask (e.g., `255.255.0.0`), and `{your_broadcast_address}` with the broadcast address (e.g., `10.11.255.255`).

#### 6. **Restarting Network Services**:
   - After making the changes, restart the network interface or the whole system for the changes to take effect:
     ```bash
     sudo systemctl restart networking
     ```

#### 7. **Verifying the Port Status**:
   - Check again whether **UDP port 68** is closed by running:
     ```bash
     ss -tunlp
     ```

By following these steps, you will close **UDP port 68**, often associated with DHCP, and configure a static IP for your machine. This is particularly useful for securing your system and preventing unwanted network configuration changes.

#### 🧠 **UDP (User Datagram Protocol)**: A communication protocol used across the Internet that allows sending packets of data without requiring a connection, unlike TCP, making it faster but less reliable.
