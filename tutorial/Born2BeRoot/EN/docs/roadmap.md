## ⤵️ Downloading <a id="downloading"></a>

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

### Installing Debian OS
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

### 4. Starting Debian  
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
