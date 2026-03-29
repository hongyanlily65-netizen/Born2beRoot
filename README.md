# 42cursus - Born2beroot
This project has been created as part of the 42 curriculum by hohu.

## Table of Contents
1. [Introduction](#introduction)
    - [What is a Virtual Machine?](#Virtual-Machine)
    - [How do Virtual Machines work?](#Virtual-Machines-work)
    - [What is LVM?](#What-is-LVM?)
    - [What is AppArmor?](#What-is-AppArmor?)
    - [What is the difference between Apt and Aptitute?](#Apt-and-Aptitute)
    - [How to use SSH?](#How-to-use-SSH?)
    - [How to implement UFW with SSH?](#UFW-with-SSH)
    - [What is cron and what is wall?](#what-is-cron)
2. [*sudo*](#sudo)
    - [Step 1: Installing *sudo*](#step-1-installing-sudo)
    - [Step 2: Adding User to *sudo* Group](#step-2-adding-user-to-sudo-group)
    - [Step 3: Running *root*-Privileged Commands](#step-3-running-root-privileged-commands)
    - [Step 4: Configuring *sudo*](#step-4-configuring-sudo)
3. [SSH](#ssh)
    - [Step 1: Installing & Configuring SSH](#step-1-installing--configuring-ssh)
    - [Step 2: Installing & Configuring UFW](#step-2-installing--configuring-ufw)
    - [Step 3: Connecting to Server via SSH](#step-3-connecting-to-server-via-ssh)
4. [User Management](#user-management)
    - [Step 1: Setting Up a Strong Password Policy](#step-1-setting-up-a-strong-password-policy)
       - [Password Age](#password-age)
       - [Password Strength](#password-strength)
    - [Step 2: Creating a New User](#step-2-creating-a-new-user)
    - [Step 3: Creating a New Group](#step-3-creating-a-new-group)
5. [*cron*](#cron)
    - [Setting Up a *cron* Job](#setting-up-a-cron-job)
6. [Monitoring](#monitoring)

7. [Submission and peer-evaluation](#peereval)

## Introduction

You will create your first machine in VirtualBox under specific instructions. At the end of this project, you should be able to set up your own operating system while following strict system administration rules.

### <a name="Virtual-Machine">What is a Virtual Machine?</a>

A virtual machine is a **software environment capable of running an operating system inside itself**, making the OS think that it is hosted on a real computer. With virtual machines, we can create virtual devices that behave like physical devices, using their own **CPU, memory, network interface, and storage**. This is possible because the virtual machine is hosted on a **physical machine**, which provides the hardware resources to the VM. The software that creates and manages virtual machines is called the **hypervisor**.<br>

The devices that provide the hardware resources are called **host machines** or **hosts**. The different virtual machines assigned to a host are called **guests** or **guest machines**. The hypervisor takes part of the host machine's resources and distributes them among the different VMs.<br>

<br>

There can be multiple virtual machines on the same host, and each of them is isolated from the rest of the system. Thanks to this, we can run different operating systems on the same physical machine. Each VM behaves as if it were installed on its own real computer.<br>

### <a name="Virtual-Machines-work">How do Virtual Machines work?</a>

Virtualization allows us to share one physical system with multiple virtual environments. The hypervisor manages the hardware and separates the physical resources from the virtual machines. **The resources are distributed from the host to the guests**, so each VM can work independently.<br>

When a user inside a virtual machine performs an action that needs hardware resources, the hypervisor manages the communication between the guest system and the physical machine. In this way, the guest operating system can use the host resources without direct access to the hardware.<br>

<br>

This system makes virtual machines useful for **learning, testing, development, and administration**, because they remain isolated and do not affect the main operating system directly.<br>

### <a name="What-is-LVM?">What is LVM?</a>

**LVM** stands for **Logical Volume Manager**. It is a method used in Linux to manage disk space in a more flexible way than traditional partitioning. Instead of depending only on fixed disk partitions, LVM allows the creation of **logical volumes** that can be resized or reorganized more easily.<br>

With LVM, storage management becomes more practical because the administrator can adapt disk space according to the system needs. This is especially useful when the machine may need future changes in storage size.<br>

<br>

In short, LVM provides **flexibility, scalability, and easier disk administration** compared with standard partition systems.<br>

### <a name="What-is-AppArmor?">What is AppArmor?</a>

**AppArmor** is a Linux security module that restricts what a program can do and what resources it can access. It works with **security profiles** that define which files, directories, and capabilities are allowed for each application.<br>

Because of these profiles, even if a program is compromised, its actions remain limited. This reduces the possible damage caused by vulnerable or malicious software and improves the global system security.<br>

<br>

AppArmor is therefore an important tool for protecting a Linux system by controlling application behavior.<br>

### <a name="Apt-and-Aptitute">What is the difference between Apt and Aptitude?</a>

**APT** is the standard package manager used in Debian-based systems. It is commonly used to **install, remove, update, and upgrade packages** from the command line. It is simple, direct, and widely used by administrators.<br>

**Aptitude** is another package manager built on top of APT. It can also manage software packages and dependencies, but it provides a more interactive interface and sometimes handles dependency conflicts differently.<br>

<br>

Today, **APT is the most commonly used tool**, while Aptitude is less common but still useful in some situations.<br>

### <a name="How-to-use-SSH?">How to use SSH?</a>

**SSH** stands for **Secure Shell**. It is a protocol that allows a user to connect securely to another machine over a network and control it remotely through the terminal.<br>

With SSH, a user can log into a server or a virtual machine with a command such as `ssh username@ip-address -p 4242`. The connection is encrypted, which means the communication is protected from unauthorized access.<br>

<br>

SSH is widely used in system administration because it offers a **secure and reliable way to manage a remote machine**.<br>

### <a name="UFW-with-SSH">How to implement UFW with SSH?</a>

**UFW** stands for **Uncomplicated Firewall**. It is a tool used to manage firewall rules in a simple way on Linux systems. When SSH is enabled, the SSH port must be explicitly allowed in UFW; otherwise, remote access will be blocked.<br>

For example, if SSH is configured to use **port 4242**, then this port must be opened in the firewall rules. Once this is done, the machine can accept SSH connections while still being protected by the firewall.<br>

<br>

Using UFW with SSH is important because it helps keep the system secure while preserving remote administrative access.<br>

### <a name="What-is-cron-and-what-is-wall?">What is cron and what is wall?</a>

**Cron** is a service that executes commands or scripts automatically at scheduled times. It is commonly used for repetitive tasks such as **monitoring, backups, updates, and maintenance**.<br>

**Wall** is a command that sends a message to **all logged-in users** on the system. It is often used by administrators to broadcast alerts or important information.<br>

<br>

In projects like Born2beroot, cron can be used to launch a monitoring script regularly, and wall can be used to display the result to every connected user.<br>


## *sudo*

### Step 1: Installing *sudo*
Switch to *root* and its environment via `su -`.
```
$ su -
Password:
#
```
Install *sudo* via `apt install sudo`.
```
# apt install sudo
```
Verify whether *sudo* was successfully installed via `dpkg -l | grep sudo`.
```
# dpkg -l | grep sudo
```

### Step 2: Adding User to *sudo* Group
Add user to *sudo* group via `adduser <username> sudo`.
```
# adduser <username> sudo
```
>Alternatively, add user to *sudo* group via `usermod -aG sudo <username>`.
>```
># usermod -aG sudo <username>
>```
Verify whether user was successfully added to *sudo* group via `getent group sudo`.
```
$ getent group sudo
```
`reboot` for changes to take effect, then log in and verify *sudopowers* via `sudo -v`.
```
# reboot
<--->
Debian GNU/Linux 10 <hostname> tty1

<hostname> login: <username>
Password: <password>
<--->
$ sudo -v
[sudo] password for <username>: <password>
```

### Step 3: Running *root*-Privileged Commands
From here on out, run *root*-privileged commands via prefix `sudo`. For instance:
```
$ sudo apt update
```

### Step 4: Configuring *sudo*
Configure *sudo* 
```
$ sudo visudo
```

To log all *sudo* commands to `/var/log/sudo/<filename>`:
```
$ sudo mkdir /var/log/sudo
$ sudo touch /var/log/sudo.log
```
```
Defaults        logfile="/var/log/sudo/sudo.log"
Defaults        log_input,log_output
Defaults        iolog_dir="/var/log/sudo"
Defaults        requiretty
```
To set *sudo* paths to `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin`:
```
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```

## SSH

### Step 1: Installing & Configuring SSH
Install *openssh-server* via `sudo apt install openssh-server`.
```
$ sudo apt install openssh-server
```
Verify whether *openssh-server* was successfully installed via `dpkg -l | grep ssh`.
```
$ dpkg -l | grep ssh
```
Configure SSH via `sudo vi /etc/ssh/sshd_config`.
```
$ sudo vi /etc/ssh/sshd_config
```
To set up SSH using Port 4242, replace below line:
```
13 #Port 22
```
with:
```
13 Port 4242
```
To disable SSH login as *root* irregardless of authentication mechanism, replace below line
```
32 #PermitRootLogin prohibit-password
```
with:
```
32 PermitRootLogin no
```
Check SSH status via `sudo service ssh status`.
```
$ sudo service ssh status
```
>Alternatively, check SSH status via `systemctl status ssh`.
>```
>$ systemctl status ssh
>```

### Step 2: Installing & Configuring UFW
Install *ufw* via `sudo apt install ufw`.
```
$ sudo apt install ufw
```
Verify whether *ufw* was successfully installed via `dpkg -l | grep ufw`.
```
$ dpkg -l | grep ufw
```
Enable Firewall via `sudo ufw enable`.
```
$ sudo ufw enable
```
Allow incoming connections using Port 4242 via `sudo ufw allow 4242`.
```
$ sudo ufw allow 4242
```
Check UFW status via `sudo ufw status`.
```
$ sudo ufw status
```

### Step 3: Connecting to Server via SSH
SSH into your virtual machine using Port 4242 via `ssh <username>@<ip-address> -p 4242`.
```
$ ssh <username>@<ip-address> -p 4242
```
Terminate SSH session at any time via `logout`.
```
$ logout
```
>Alternatively, terminate SSH session via `exit`.
>```
>$ exit
>```

## User Management

### Step 1: Setting Up a Strong Password Policy

#### Password Age
Configure password age policy via `sudo vi /etc/login.defs`.
```
$ sudo vi /etc/login.defs
```
To set password restrictions
```
160 160 PASS_MAX_DAYS   30
161 PASS_MIN_DAYS   2
162 PASS_WARN_AGE   7
```

#### Password Strength
Secondly, to set up policies in relation to password strength, install the *libpam-pwquality* package.
```
$ sudo apt install libpam-pwquality
```
Configure password strength policy via `sudo vi /etc/pam.d/common-password`, specifically the below line:
```
25 password        requisite                       pam_pwquality.so retry=3
minlen=10 ucredit=-1 dcredit=-1 lcredit=-1 maxrepeat=3 reject_username difok=7
enforce_for_root
```
### Modifying hostname
```
sudo hostnamectl set-hostname <username>
sudo nano /etc/hosts
```
### Creating a New User
Create new user via `sudo adduser <username>`.
```
$ sudo adduser <username>
```
Verify whether user was successfully created via `getent passwd <username>`.
```
$ getent passwd <username>
```
Verify newly-created user's password expiry information via `sudo chage -l <username>`.

### Creating a New Group
Create new *user42* group via `sudo addgroup user42`.
```
$ sudo addgroup user42
```
Add user to *user42* group via `sudo adduser <username> user42`.

## *cron*

### Setting Up a *cron* Job
Configure *cron* as *root* via `sudo crontab -u root -e`.
```
$ sudo crontab -u root -e
```
To schedule a shell script to run every 10 minutes, replace below line
```
23 # m h  dom mon dow   command
```
with:
```
23 */10 * * * * sh /path/to/script
```
Check *root*'s scheduled *cron* jobs via `sudo crontab -u root -l`.
```
$ sudo crontab -u root -l
```
## Monitoring

You have to create a simple script called `monitoring.sh` It must be developed in bash.
At server startup, the script will display some information (listed below) on all ter- minals every 10 minutes (take a look at wall). The banner is optional. No error must be visible.
Your script must always be able to display the following information:<br/>
• The architecture of your operating system and its kernel version.<br/>
• The number of physical processors.<br/>
• The number of virtual processors.<br/>
• The current available RAM on your server and its utilization rate as a percentage.<br/> 
• The current available memory on your server and its utilization rate as a percentage.<br/>
• The current utilization rate of your processors as a percentage.<br/>
• The date and time of the last reboot.<br/>
• Whether LVM is active or not.<br/>
• The number of active connections.<br/>
• The number of users using the server.<br/>
• The IPv4 address of your server and its MAC (Media Access Control) address.<br/>
• The number of commands executed with the sudo program.

 You can find the script `monitoring.sh` in this repository.

## <a name="peereval">Submission and peer-evaluation</a>

You only have to turn in a signature.txt file at the root of your Git repository. You must paste in it the signature of your machine’s virtual disk. To get this signature, you first have to open the default installation folder (it is the folder where your VMs are saved):
 
• Windows: `%HOMEDRIVE%%HOMEPATH%\VirtualBox VMs\`
    
• Linux: `~/VirtualBox VMs/`
    
• MacM1: `~/Library/Containers/com.utmapp.UTM/Data/Documents/ `
    
• MacOS: ` ~/VirtualBox VMs/`

Then, retrieve the signature from the ".vdi" file (or ".qcow2 for UTM’users) of your virtual machine in sha1 format. Below are 4 command examples for a centos_serv.vdi file:
    
• Windows: `certUtil -hashfile centos_serv.vdi sha1 `
    
• Linux: `sha1sum centos_serv.vdi`
    
• For Mac M1: `shasum Centos.utm/Images/disk-0.qcow2 `
    
• MacOS: `shasum centos_serv.vdi`
    
This is an example of what kind of output you will get:
    
• `6e657c4619944be17df3c31faa030c25e43e40af`

