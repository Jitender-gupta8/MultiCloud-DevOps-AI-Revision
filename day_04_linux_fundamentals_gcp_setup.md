# 🐧 Day 4: Linux Fundamentals + GCP Setup

> **Learning Path:** Multi-Cloud + DevOps with AI  
> **Focus Areas:** Operating Systems, Linux Architecture, SSH, Linux Directory Structure, Essential Commands, and Google Cloud Platform (GCP) Compute Engine.

---

## 🎯 Overview & Objectives

Understanding the underlying foundation of systems, operating systems, and networking is crucial for DevOps, cloud engineering, and site reliability engineering (SRE). Tools and automation frameworks build on top of these core concepts. 

Today's milestone focuses on:
* Deconstructing the operating system architecture (Kernel vs. Shell).
* Navigating Linux distributions and why Linux dominates the cloud ecosystem.
* Setting up remote compute instances in **Google Cloud Platform (GCP)**.
* Mastering essential Linux commands and the standard filesystem hierarchy.

---

## 💻 1. Operating System Fundamentals

An **Operating System (OS)** is system software that manages computer hardware, software resources, and provides common services for computer programs. It acts as an abstraction layer between user applications and the physical hardware.

```
+-------------------------------------------------------+
|                    Applications                       |
|           (Web Browsers, Editors, Scripts)            |
+-------------------------------------------------------+
                           |
                           v
+-------------------------------------------------------+
|                       Shell                           |
|          (Command Line Interface / CLI)               |
+-------------------------------------------------------+
                           |
                           v
+-------------------------------------------------------+
|                      Kernel                           |
|      (Memory, CPU, Process & File Management)         |
+-------------------------------------------------------+
                           |
                           v
+-------------------------------------------------------+
|                     Hardware                          |
|           (CPU, RAM, Disks, Network Interfaces)       |
+-------------------------------------------------------+
```

### Key Responsibilities of an OS:
1. **Process Management:** Allocates CPU time slices to processes and handles execution, scheduling, and synchronization.
2. **Memory Management:** Manages RAM allocation and deallocation for active programs; handles virtual memory.
3. **Storage & File System Management:** Organizes physical storage blocks into readable file hierarchies.
4. **Device Management:** Communicates with hardware components using drivers.
5. **Security & Access Control:** Manages permissions, authentication, and isolation between users and processes.

---

## ⚙️ 2. Kernel vs. Shell

A classic DevOps and Linux interview topic involves explaining the precise relationship between the user, shell, kernel, and hardware:

* **Kernel:** The core, non-bypassable layer of the operating system that directly controls hardware resources. It runs in a privileged state (Kernel Mode) to ensure security and stability.
* **Shell:** An interface (Command Line Interface or Graphical User Interface) that listens to user inputs, translates commands into system calls, and passes them to the kernel for execution.

| Feature | Shell | Kernel |
| :--- | :--- | :--- |
| **Definition** | Command-line interface / Environment | Core engine of the Operating System |
| **User Interaction** | Directly interacts with the user | Indirectly interacts via system calls |
| **Memory Space** | Runs in User Space | Runs in Kernel Space |
| **Examples** | `bash`, `zsh`, `sh`, `fish` | Monolithic kernels (Linux), Microkernels |

---

## 🐧 3. Linux in Cloud & DevOps

Linux is the industry standard for cloud environments, containerization (Docker/Kubernetes), web servers, and enterprise infrastructure due to several factors:

1. **Open Source & Cost-Effective:** Fully open-source with no licensing costs, allowing rapid scaling in cloud environments.
2. **Resource Efficiency & Stability:** Runs lightweight with minimal resource overhead and uptime measured in years without requiring forced reboots.
3. **CLI-First Architecture:** Tailored for automation, remote administration, scripting, and CI/CD pipelines.
4. **Security & Permission Control:** Fine-grained access control models (`POSIX` permissions, `SELinux`, `AppArmor`).

### Overview of Key Distributions (Distros)
* **Debian / Ubuntu:** Highly popular in cloud setups and developer environments due to massive package repositories (`apt`) and community support.
* **Red Hat Enterprise Linux (RHEL) / Fedora / CentOS Stream:** Industry choice for enterprise setups prioritizing stability, long-term support, and compliance (`dnf` / `yum`).
* **Amazon Linux:** Optimized for running on AWS EC2 with tight AWS service integration and security patches.

---

## 🔐 4. Remote Access & Hands-On GCP Setup

### Secure Shell (SSH)
**SSH (Secure Shell)** is a cryptographic network protocol used for operating network services securely over an unsecured network.

```bash
# Connecting to a remote server using SSH
ssh -i /path/to/private_key username@remote_host_ip
```

### Hands-On: GCP Compute Engine Setup
1. **Cloud Environment Creation:** Set up a Google Cloud Platform (GCP) project.
2. **Provisioning VM:** Launched a lightweight **Compute Engine** virtual machine instance running **Ubuntu 22.04 LTS**.
3. **Networking & Security:** Configured firewall rules allowing inbound SSH (TCP port 22) traffic.
4. **Hands-On Practice:** Connected to the instance using GCP Cloud Shell SSH and local terminal access.

---

## 📁 5. Linux Directory Structure (FHS)

Linux follows the **Filesystem Hierarchy Standard (FHS)**, where everything is represented as a file or directory branching from a single root node `/`.

```
/ (Root)
├── bin  -> Essential user command binaries (e.g., ls, cd, cat)
├── dev  -> Device files (e.g., /dev/sda, /dev/null)
├── etc  -> Host-specific system configurations
├── home -> User home directories (e.g., /home/ubuntu)
├── lib  -> Essential shared libraries and kernel modules
├── proc -> Virtual filesystem documenting process & kernel state
├── tmp  -> Temporary files (cleared on reboot)
├── usr  -> Multi-user utilities and applications
└── var  -> Variable data files (logs, databases, spool files)
```

---

## ⌨️ 6. Essential Command Reference

Here is a summary of the fundamental commands practiced today:

```bash
# Print Working Directory: Displays the absolute path of the current directory
pwd

# List Directory Contents: Shows files and directories
ls -la        # -a: includes hidden files; -l: detailed long listing

# Change Directory: Navigate through the filesystem
cd /var/log   # Move to /var/log
cd ~          # Move to the user's home directory
cd ..         # Move up one level

# Make Directory: Create new folders
mkdir devops_practice

# Who Am I: Displays the active user name
whoami

# Unix Name: Displays system architecture and kernel information
uname -a      # Shows all system information (kernel version, architecture)
```

---

## 💡 Key Takeaway & Next Steps

> *Building expertise in DevOps starts with understanding the core operational systems underneath high-level tooling.*

**The DevOps Core Formula:**  
`Linux + Networking + Cloud + Automation = Strong DevOps Foundation 🚀`

**Next Steps:**
* Deepen command-line fluency by completing additional levels in the OverTheWire Bandit challenge.
* Practice permission management (`chmod`, `chown`) and file manipulation commands (`grep`, `find`, `sed`, `awk`).
* Automate basic Linux system checks using Bash scripts on the GCP VM.