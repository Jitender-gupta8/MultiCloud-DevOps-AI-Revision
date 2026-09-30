# 🐧 Day 9 | Linux Administration, Patching & File Permissions

Continuing my **DevOps learning journey**, today I focused on some practical Linux concepts that are directly relevant to **server administration, troubleshooting, security and automation**.

## 📂 Linux Directory Structure

Understanding where things live in Linux is essential for troubleshooting.

- 🔹 `/` → Root of the filesystem
- 🔹 `/etc` → Configuration files
- 🔹 `/bin` → Essential executable commands
- 🔹 `/root` → Root user's home directory
- 🔹 `/home` → Regular users' home directories
- 🔹 `/tmp` → Temporary files
- 🔹 `/dev` → Device files

## 📝 Vi/Vim Basics

I also revised the fundamentals of the **vi/vim** editor:

- `i` → Insert mode
- `Esc` → Command mode
- `:w` → Save
- `:wq` → Save & exit
- `:q!` → Exit without saving
- `dd` → Delete a line
- `u` → Undo

These commands are especially useful when working directly on Linux servers.

## 🔄 OS Patching

Patching is an important part of maintaining secure and stable servers.

**Basic flow:**

- `apt update` → Update package information
- `apt upgrade -y` → Install available updates
- `reboot` → Restart when required after critical updates

In production environments, patches should be tested in lower environments before production deployment.

## 🌐 Nginx + systemctl

I also learned how a web server can be installed, tested and managed using Linux:

- `systemctl status nginx`
- `systemctl start nginx`
- `systemctl stop nginx`
- `systemctl restart nginx`
- `systemctl enable nginx`

The same `systemctl` concept applies to services such as **Docker, Jenkins and Apache**.

## 🔐 File Permissions

One important troubleshooting scenario:

**Permission denied ❌**

A newly created script doesn't automatically have execute permission.

- `chmod +x script.sh` → Add execute permission
- `chmod 755 script.sh` → Owner: `rwx`, Group: `r-x`, Others: `r-x`

And an important production lesson:

**Avoid `chmod 777` unless there is a very specific, justified requirement.**

## 🚀 Key Takeaway

DevOps isn't just about learning tools.

It starts with understanding the **operating system, services, permissions, patching and troubleshooting** behind those tools.

**Linux → Administration → Security → Automation → DevOps 🚀**

**Day 9 ✅ | Learn → Practice → Troubleshoot → Apply**

#Day9 #Linux #DevOps #LinuxAdministration #LinuxCommands #SystemAdministration #LinuxSecurity #Nginx #ShellScripting #CloudComputing #DevOpsLearning #CloudEngineering #LearningInPublic #DevOpsJourney
