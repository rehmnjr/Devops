# 🗂️ Linux Filesystem

> Learn how Linux organizes files and directories using the **Filesystem Hierarchy Standard (FHS)**. Understanding the filesystem is essential for navigating Linux, managing servers, troubleshooting applications, and working efficiently in DevOps.

---

# 📖 Overview

A **filesystem** is the way an operating system stores and organizes files and directories.

Unlike Windows, which uses multiple drives like `C:\`, `D:\`, and `E:\`, Linux organizes everything under a **single directory tree** that starts from the **root directory (`/`)**.

Everything in Linux is treated as a file, including:

- Regular files
- Directories
- Hard disks
- USB devices
- Network sockets
- Running processes
- System information

This unified structure makes Linux simple, consistent, and powerful.

---

# 🎯 Learning Objectives

After completing this chapter, you will understand:

- What is a filesystem?
- What is the root directory?
- Linux directory hierarchy
- Important system directories
- Absolute and Relative paths
- Hidden files
- Inodes
- Hard Links
- Symbolic Links
- Filesystem Hierarchy Standard (FHS)

---

# 🌳 Linux Filesystem Structure

```text
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

Unlike Windows, Linux has only **one root directory (`/`)**.

Every file and directory exists somewhere under this root.

---

# 📌 What is the Root Directory (`/`)?

The **root directory** is the top-most directory in Linux.

Every other directory is a child of the root directory.

```text
/
├── home
├── etc
├── usr
└── var
```

Think of it as the **starting point** of the entire filesystem.

> **Note:** The root directory (`/`) is different from the **root user**. The root directory is a location in the filesystem, while the root user is the system administrator account.

---

# 📂 Important Linux Directories

## `/bin`

Stores essential user commands required for basic system operation.

Examples:

- `ls`
- `cp`
- `mv`
- `cat`
- `pwd`

**DevOps Use Case**

Even if the system is in recovery mode, many basic commands remain available from this directory.

---

## `/sbin`

Stores essential system administration commands.

Examples:

- `shutdown`
- `reboot`
- `fsck`

These commands are primarily used for system maintenance.

---

## `/boot`

Contains files required during system startup.

Examples:

- Linux Kernel
- Bootloader configuration
- Initial RAM filesystem (initramfs)

---

## `/dev`

Contains device files.

Examples include:

- Hard disks
- USB drives
- Terminal devices

In Linux, hardware devices are represented as files.

---

## `/etc`

Contains system-wide configuration files.

Examples:

- Network configuration
- User configuration
- Service configuration

**DevOps Use Case**

Configuration files for services like SSH, NGINX, Apache, and many others are commonly stored here.

---

## `/home`

Contains personal directories for regular users.

Example structure:

```text
/home/
├── developer1
├── developer2
└── developer3
```

Each user has their own workspace.

---

## `/root`

Home directory of the **root user**.

Do not confuse:

| Directory | Purpose |
|-----------|---------|
| `/` | Root directory |
| `/root` | Home directory of the root user |

---

## `/lib`

Contains shared libraries required by system programs.

These libraries work similarly to reusable code modules used by applications.

---

## `/media`

Automatically mounts removable storage devices.

Examples:

- USB Drives
- Memory Cards
- External Hard Drives

---

## `/mnt`

Used for manually mounting storage devices or network filesystems.

---

## `/opt`

Stores optional third-party software.

Examples:

- Custom applications
- Commercial software
- Vendor packages

---

## `/proc`

A virtual filesystem that provides information about the running system.

Examples include information about:

- CPU
- Memory
- Running processes
- Kernel

The files in `/proc` are generated dynamically while the system is running.

---

## `/run`

Stores temporary runtime information used by running services and processes.

---

## `/srv`

Contains data served by system services.

Example:

- FTP server data
- Web server content

---

## `/sys`

Provides information about hardware devices and the Linux kernel.

Used primarily by the kernel and system utilities.

---

## `/tmp`

Stores temporary files.

Important points:

- Used for temporary data
- Files may be deleted automatically after reboot
- Safe for temporary scripts and testing

---

## `/usr`

Contains user applications and utilities.

Examples include:

- Installed software
- Documentation
- Libraries

Most applications installed on the system are located under `/usr`.

---

## `/var`

Stores files that change frequently.

Examples:

- Log files
- Cache
- Mail
- Databases
- Print queues

**DevOps Use Case**

Application and system logs are commonly stored under `/var/log`.

---

# 🗺️ Filesystem Hierarchy Standard (FHS)

The **Filesystem Hierarchy Standard (FHS)** defines a common directory structure for Linux systems.

Benefits include:

- Consistency across Linux distributions
- Easier administration
- Predictable file locations
- Improved software compatibility

Whether you're using Ubuntu, Debian, Rocky Linux, or Fedora, the major directories remain largely consistent because they follow the FHS.

---

# 📍 Absolute Path

An **absolute path** starts from the root directory (`/`).

Example:

```text
/etc/ssh/sshd_config
```

Characteristics:

- Always starts with `/`
- Works regardless of the current directory

---

# 📍 Relative Path

A **relative path** starts from the current working directory.

Example:

```text
documents/report.txt
```

Characteristics:

- Does not start with `/`
- Depends on your current location

---

# 🔒 Hidden Files

Files beginning with a dot (`.`) are hidden by default.

Examples:

```text
.bashrc
.profile
.gitignore
```

Use the following command to view hidden files:

```bash
ls -a
```

---

# 📄 Inodes

An **inode** is a data structure that stores metadata about a file.

It contains information such as:

- File size
- Permissions
- Owner
- Group
- Creation and modification times
- Disk block locations

An inode **does not store the filename**.

---

# 🔗 Hard Link

A hard link is another directory entry pointing to the **same inode**.

Characteristics:

- Shares the same data
- Shares the same inode
- Deleting one link does not remove the data until all hard links are deleted

---

# 🔗 Symbolic Link (Soft Link)

A symbolic link is a special file that points to another file or directory.

Characteristics:

- Has a different inode
- Can point across filesystems
- Can point to directories
- Becomes broken if the original file is deleted

---

# 🔄 Hard Link vs Symbolic Link

| Feature | Hard Link | Symbolic Link |
|----------|-----------|---------------|
| Same inode | ✅ | ❌ |
| Can cross filesystems | ❌ | ✅ |
| Can link directories | ❌ | ✅ |
| Breaks if original is deleted | ❌ | ✅ |

---

# 🌍 Real-World DevOps Usage

A DevOps engineer works with the filesystem every day.

Examples include:

- Editing configuration files under `/etc`
- Reading application logs from `/var/log`
- Deploying applications under `/opt`
- Managing user directories under `/home`
- Monitoring system information from `/proc`
- Storing temporary deployment artifacts in `/tmp`

Understanding where files are stored makes troubleshooting much easier.

---

# ⚠️ Common Beginner Mistakes

- Confusing `/` with `/root`
- Assuming Linux uses drive letters like Windows
- Storing important files inside `/tmp`
- Deleting files from system directories without understanding their purpose
- Ignoring hidden configuration files

---

# 🛠️ Troubleshooting

### "I can't find my configuration file."

Check the `/etc` directory.

---

### "Where are my application logs?"

Many applications store logs under:

```text
/var/log
```

---

### "Where should I install my own software?"

Third-party applications are commonly installed under:

```text
/opt
```

---

# 💡 Best Practices

- Learn the purpose of each top-level directory.
- Avoid modifying system directories unless necessary.
- Use absolute paths in automation scripts whenever possible.
- Store temporary data in `/tmp`.
- Keep custom applications organized under `/opt` when appropriate.

---

# ❓ Interview Questions

### 1. What is the Linux Filesystem Hierarchy Standard (FHS)?

**Answer:** It is a standard that defines the directory structure and directory contents on Linux systems, ensuring consistency across distributions.

---

### 2. What is the difference between `/` and `/root`?

**Answer:** `/` is the root directory of the filesystem, while `/root` is the home directory of the root (administrator) user.

---

### 3. What is an inode?

**Answer:** An inode stores metadata about a file, such as permissions, ownership, timestamps, and disk block locations, but not the filename.

---

### 4. What is the difference between an absolute path and a relative path?

**Answer:** An absolute path starts from the root directory (`/`), whereas a relative path starts from the current working directory.

---

### 5. Where are configuration files typically stored?

**Answer:** Most system-wide configuration files are stored under `/etc`.

---

# 📝 Practice Tasks

1. Draw the Linux filesystem hierarchy on paper.
2. Identify the purpose of each top-level directory.
3. Explore the contents of `/etc`, `/var`, and `/usr`.
4. Find three hidden files in your home directory.
5. Compare a hard link and a symbolic link using sample files.

---

# 📚 Summary

- Linux organizes everything under a single root directory (`/`).
- The Filesystem Hierarchy Standard (FHS) provides a consistent directory structure.
- Each top-level directory has a specific purpose.
- Absolute paths always begin with `/`.
- Relative paths depend on the current directory.
- Hidden files begin with a dot (`.`).
- Inodes store file metadata.
- Hard links and symbolic links behave differently and serve different purposes.

---

# ➡️ Next Chapter

**📄 03-linux-navigation.md**

In the next chapter, you'll learn how to navigate the Linux filesystem using commands such as `pwd`, `ls`, `cd`, `tree`, and `stat`.
