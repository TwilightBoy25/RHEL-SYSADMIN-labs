# Essential File Management Tools

## Topics that are covered in this chapter

- Working with the File System Hierarchy
- Managing Files
- Using Links
- Working with Archives and Compressed Files

## RHCSA exam objectives are covered in this chapter

- Create, delete, copy, and move files and directories
- Archive, compress, unpack, and uncompress files using tar, star, gzip, and bzip2
- Create hard and soft links

## Working with the File System Hierarchy

It is good to know how to use the default directories that exist on Linux systems.

### Defining the File System Hierarchy

Filesystem Hierarchy Standard (FHS)

The table I have created below are the most significant directories that I will encounter on a RHEL system, as specified by the FHS

| Directory | Use |
| --- | --- |
| / | Specifies the root directory. This is where the file system tree starts. |
| /boot | Contains all files and directories that are needed to boot the Linux Kernel. | 
| /dev | Contains device files that are used for accessing physical devices. This directory is essential during boot. |
| /etc | Contains figuration files that are used by programs and services on your server. This directory is essential during boot. |
| /home | Used for local user home directories. |
| /media,/mnt | Contain directories that are used for mounting devices in the file system tree. |
| /opt | Used for optional packages that may be installed on your server. |
| /proc | Used by the proc file system. This is a file system structure that gives access to kernel information. |
| /root | Specifies the home directory of the root user. |
| /run | Contains process and user-specific information that has been created since the last boot. |
| /srv | May be used for data by services like NFS, FTP, and HTTP. |
| /sys | Used as an interface to different hardware devices that are managed by the Linux kernel and associated processes. |
| /tmp | Contains temporary files that may be deleted without any warning during boot. |
| /usr | Contains subdirectories with program files, libraries for these program files, and documentation about them. |
| /var | Contains files that may change in size dynamically, such as log files, mail boxes, and spool files. |

### Understanding Mounts

To be able to understand the organization of Linux files it is paramount to understand the concept of mounting. 

A mount is a connection between a device and a directory. 

Mounting devices making it possible to organize the Linux file system in a flexible way.

Below I am listing several good reasons to work with multiple mounts:

1. High activity in one area may fill up the entire file system, which will negatively impact serices running on the server.
2. If all files are on the same device, it is difficult to secure access and distinguish between different areas of the file system with different security needs. By mounting a separate file system, you can add mount options to meet specific security needs, such as the noexec option, which disallows running any executable file, which may make sense in user home directories.
3. If a one-device file system is completely filled, it may be difficult to make additional storage space available. 

To avoid these pitfalls, it is common to organize Linux file systems in different devices 

### Mental model for myself

FHS -> Defines what major Linux directories are for 
/ -> The root of the entire directory tree
Mount -> A connection between a filesystem on a device and a directory 
Mount point -> The directory where the filesystem/device becomes accessible

/ != /root
/ = root of the entire filesystem 
/root = the home directory for root user

### Common Dedicated Mounts

Certain directories are commonly placed on separate file systems for storage, security, or boot requirements.

- '/boot' - Contains files required to boot Linux. It may use a dedicated file system so boot files remain separately accessible.
- '/boot/EFI' - Used on systems that boot with UEFI/EFI. The EFI System Partition is mounted here for access to early boot files.
- '/var' - Contains variable data that can grow dynamically, such as logs under '/var/log'. A separate file system can prevent growing logs from filling storage used by the rest of the system.
- '/usr' - Contains operating system programs, libraries, and related files. It can be mounted separately and configured with restrictive options such as read-only when appropriate.

### Mount Options

Separate file systems can have different mounts options depending on their purpose.

Example:

'noexec'

The 'noexec' mount option prevents executables from being executed directly from that mounted file system. 

### Viewing Storage and Mounts

Three important commands provide different views of storage:

| Command | Purpose |
| --- | --- |
| 'df -Th' | Shows file system disk usage, type, and mount points |
| 'findmnt' | Shows mounted file systems and relationships between mounts |
| 'lsblk' | Shows block devices such as disks, partitions, and logical volumes |

For 'df -Th':

- '-T' = display the type of file system
- '-h' = display human-readable units

Important 'df' columns include:

- 'Filesystem' - Device/file system being used
- 'Type' - File system type
- 'Size' - Total size
- 'Used' - Space currently used
- 'Avail' - Space still available
- 'Use%' - Percentage of space currently used
- 'Mounted on' - Directory serving as the mount point

### Storage Mental Model

Physical/logical storage -> Block Device -> File System -> Mount -> Mount Point -> Linux Directory Tree

'df -Th' -> "How much file system space is used, and what type is it?"
'findmnt' -> "What is mounted where, and how are the mounts related?"
'lsblk' -> "What block storage devices does the system have?"
