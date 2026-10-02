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
