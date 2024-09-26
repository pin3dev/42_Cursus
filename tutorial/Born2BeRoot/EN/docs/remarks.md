## 🔎 Remarks

### Graphic Interface

> 🚨 Note that it is forbidden to install the chosen OS version with a graphical interface or graphics servers such as X.org.  

### System security

> 🚨 The **_Mandatory Access Control framework_** (`SELinux/AppArmor`) must be active when starting the machine.  
> 🚨 The _**SSH**_ service can only run on `port 4242`.  
> 🚨 The access to the _**root user**_ should _**not be possible**_ via the SSH.  
> 🚨 The firewall (`Firewall/UFW`) must be active when you boot up the machine.  
> 🚨 Every _**sudo user**_ action (stdin and stdout) must be written to a file in the `/var/log/sudo` directory.  
> 🚨 The TTY mode has be enabled.  
> 🚨 The PATH of possible executables by _**sudo**_ should be restricted to `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin`. 

 
#### Password policy 
> ℹ️ The rules for the strong password policy are:  

| Rule | Description | usr-sudo | usr-non-adm | Example |
|:-----|:-----------:|:--------:|:-----------:|:-------:|
| Setup and Reset |password expires after 30 days | ✅ | ✅ |-|
| Setup and Reset |min 2 days to reset password| ✅ | ✅ |-|
| Setup and Reset |password expiry alert 7 days early| ✅ | ✅ |-|
| Setup and Reset |max 3 failed access attempts| ✅ | ❌ |-|
| Setup and Reset |error message displays if password attempt fails| ✅ | ❌ |-|
| Composition |must have min 10x characters | ✅ | ✅ | `_password!` |
| Composition |must have min 1x uppercase, 1x lowercase and 1x number | ✅ | ✅ | `_P4ssw0rd!` |
| Composition |must have min 7x different characters from previous passwords| ❌ | ✅ | changed passw: `Curr3nT-#` |
| Composition |shouldn't have 3x consecutive identical characters| ✅ | ✅ | wrong passw: `P4sss_word` |
| Composition |shouldn't have the username inside| ✅ | ✅ | wrong passw: `usernameP4ssw!` |

### Monitoring

> 🚨 Note The script should be run every 10 minutes from the time the machine boots up.  
> ℹ️ The monitoring script should display the following data about the system:  

| Line | Content | Format | Example |
|:----:|:-------:|:------:|:-------:|
|1|OS Architecture and Kernel|`type and version`||
|2|Physical processors|`amount`||
|3|Virtual processors|`amount`||
|4|RAM available and in use|`amount and %`||
|5|Memory available and in use|`amount and %`||
|6|Processors in use|`%`||
|7|Last reboot|`date and time`||
|8|LVM|`status`||
|9|Connections TCP|`amount and status`||
|10|Users|`amount`||
|11|IPv4 and MAC|`addresses`||
|12|Commands executed by sudo|`amount`||
 

<p align="center">
<a href="https://github.com/pin3dev/42_Cursus/blob/main/tutorial/Born2BeRoot/EN/docs/toStudy.md"> Previous ⬅️ </a> • 
<a href=""> Top ⬆️ </a> • 
<a href="https://github.com/pin3dev/42_Cursus/blob/main/tutorial/Born2BeRoot/EN/docs/concepts.md">Next ➡️ </a>
</p>
