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
