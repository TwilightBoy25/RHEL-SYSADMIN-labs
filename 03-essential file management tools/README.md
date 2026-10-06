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

## Managing Files

Listed below are common file management tasks that I need to be able to perform as an administrator:

1. Working with wildcards
2.  Managing and working directories
3.  Working with absolute and relative pathnames
4.  Listing files and directories
5.  Copying files and directories
6.  Moving files and directories
7.  Deleting files and directories

### Working with Wildcards

Wildcard: A shell feature that is able to let you refer to multiple files in an easy way.

| Wildcard | Use |
| --- | --- |
| * | Refers to an unlimited number of any characters. ls *, for instance shows all files in the current directory (except those that have a name starting with a dot) |
| ? | Refers to one specific character that can be any character. ls c?t would match cat as well as cut. |
| [auo] | Refers to one character that may be selected from the range that is specified between square brackets. ls c[aou]t would match cat, cut, and cot. |

### Managing and Working with Directories

To organize files, Linux works with directories (also referred to as folders). 
With me becoming an administrator, I have to be able to navigate through the directory structure. 

* -> any number of characters
? -> exactly one character
[...] -> one character from specified choices

pwd -> "Where am I?"
cd -> "Move me"
touch -> "Create an empty file"
mkdir -> "Create directory"
rmdir -> "Remove empty directory"

starts with '/' -> absolute path
doesn't start with '/' -> potentially relative to current location

### Working with Absolute and Relative Pathnames

Linux uses absolute and relative pathnames to be able to locate files and directories.

#### Absolute Pathname

An absolute pathname gives the complete path to an item starting from the root directory ('/').

Example: 

'/home/student/files/document.txt'

- Always begins with '/'
- Does not depend on the current working directory
- Refers to the same location regardless of where you currently are

#### Relative Pathname

A relative pathname describes the location of an item relative to the current working directory. 

Example: 

If the current working directory is:

'/home/student'

Then:

'files/document.txt'

refers to 

'/home/student/files/document.txt'

Relative pathnames do **not** begin with '/'.

### Special Path References

| Symbol | Meaning |
| --- | --- |
| '.' | Current directory |
| '..' | Parent directory |
| 'pwd' | Displays the current working directory |

Example: 

If the current directory is:

'/home/student/labs'

Then:

'../notes'

resolves to:

'/home/student/notes'

Each '...' moves up **one level** in the directory hierarchy.

### Mental Model

'/' at beginning -> Absolute -> Start from root

No '/' at beginning -> Relative -> Start from current directory

'.' -> Here

'..' -> Up one level

'pwd' -> Where am I?

### Listing Files and Directories

I will list in a table below of common arguments that make using ls command easier to work with 

| Command | Use |
| --- | --- |
| ls -l | Shows a long listing, which includes information about file properties, such as creation date and permissions. |
| ls -a | Shows all files, including hidden files. |
| ls -lrt | The -t option shows commands sorted based on modification date. You'll see the most recently modified files last in the list because of the -r option. This is a very useful command. |
| ls -d | Shows the names of directories, not the contents of all directories that match the wildcards that have been used with ls command. |
| ls -R | Shows the contents of the current directory, in addition to all of its subdirectories; that is, it **R**ecursively descends all subdirectories. |

A hidden file on Linux is a file that has a name that starts with a dot. 

### Copying Files and Directories

The 'cp' command is used to copy files and directories.

Basic syntax:

'cp SOURCE DESTINATION'

Example:

'cp /etc/hosts /tmp/'

This the '/etc/hosts' file into the '/tmp/' directory.

### Import 'cp' Options

| Option | Purpose |
| --- | --- |
| '-r' | Recursively copies a directory and everything inside it |
| '-a' | Archive mode: recursively copies while preserving file properties. |

Example:

'cp -r /etc /tmp/'

This copes the '/et' directory and everything beneath it into '/tmp/'.

To preserve permissions and other important file properties:

'cp -a /etc /tmp/'

### '-r' vs '-a'

'-r' -> Recursive copy

- Copies directories
- Copies files and subdirectories inside them

  '-a' -> Archive copy

  - Copies recursively
  - Preserves important file properties such as permissions and metadata
 
  Mental model:

  '-r' -> "Copy the whole directory tree"
  '-a' -> "Copy the whole directory tree while preserving its state"

  ### Trailing Slash on the Destination

  When the destination should be a directory, adding '/' makes that intention clear.

  Example:

  'cp /etc/hosts /tmp/'

  The trailing '/' tells 'cp' that '/tmp' is expected to be a directory.

  If the directory does not exist, the command will produce an error instead of accidentally creating a regular file with that name.

  ### Hidden Files

  Linux hidden files begin with a dot ('.').

  Example:

  '.bashrc'

  A normal '*' wildcard does not normally match hidden files.

  Because of this, hidden files require special attention when copying directory contents.

  Archive mode ('cp -a') is useful when copying complete directory trees, including their hidden files.

  ### Mental Model

  'cp SOURCE DESTINATION'

  'cp' -> Copy

  '-r' -> Recursive

  '-a' -> Archive + preserve properties

  '*' -> Does not normally match hidden dotfiles

  Destination ending in '/' -> Expect destination to be a directory


### Moving and Renaming Files and Directories

The 'mv' command moves files and directories from one location to another.

Syntax:

'mv SOURCE DESTINATION'

Move a file:

'mv myfile /tmp/'

Unlike 'cp', 'mv' does not require '-r' to move a directory and its contents.

'mv' can also rename files:

'mv myfile mynewfile'

This renames 'myfile' to 'mynewfile'.

### Deleting Files and Directories

The 'rm' command removes files.

'rm file1'

To recursively remove a directory and everything inside it:

'rm -r directory'

The '-f' option means force:

'rm -f file1'

Options can be combined:

'rm -rf directory;

- '-r' = recursive
- '-f' = force

## Using Links

### Understanding Hard Links and Symbolic (soft) links

| | Hard Link | Symbolic Link |
| --- | --- | --- |
| Points to | Same inode | Pathname |
| Cross filesystems? | no | yes |
| Link directories? | no | yes |
| Target filename removed? | Other hard link still works | Symlink may break |
| Command | ln | ln -s |

### Inodes and Links

Linux uses **inodes** to store administrative information about files.

An inode contains information such as:

- File permissions
- File ownership
- Timestamps
- Information needed to locate the file's data

The **filename itself is not stored in the inode**.

Mental model:

'Filename -> Inode -> File data'

A directory associates filenames with their inodes.

### Hard Links

A hard link is another filename that refers to the **same inode**

Example:

'ln file1 file2'

Mental model:

file1 --
        |--> Same Inode -> Same Data 
file2 __

Because both names reference the same inode:

- Changes made through one hard link are visible through the others.
- Removing one hard link does not remove the data if another hard link still exists.
- The file data become inaccessible once the last hard link is removed.

Hard-link restrictions:

- Must exist on the same filesystem/device
- Normally cannot be created for directories

### Symbolic Links

A symbolic link (soft link) refers to the **pathname of another file or directory** instead of sharing its inode.

Create one with:

'ls -s SOURCE LINK'

Mental model:

'Symbolic Link -> Target Pathname -> Target File'

Symbolic links:

- Can cross filesystem/device boundaries
- Can point to directories
- Become broken/dangling if the target pathname no longer exists

### Hard Link vs Symbolic Link

| Hard Link | Symbolic Link |
| --- | --- |
| Same inode as target | Refers to target pathname |
| Must remain on same filesystem | Can cross filesystems |
| Normally cannot link directories | Can link directories |
| Survives removal of another hard-link name | Can break if target disappears |
| 'ln SOURCE LINK' | 'ln -s SOURCE LINK' |

### Identifying Links

Use: 'ls -l'

A symbolic link begins with 'l' in the file type/permissions field and displays its target:

'home -> /home'

For hard-linked files, 'ls-l' displays the hard-link count.

### Mental Model

'ln' -> Hard link
'ln -s' -> Symbolic (soft) link
Hard link -> Same inode
Soft link -> Pathname to target
Hard link -> Target name removed? Other hard link still work
Soft link -> Target removed? Link becomes broken

## Removing Links

A symbolic link can be removed with 'rm'.

Example:

'rm link'

This removes the **symbolic link itself**, not the file or directory that the link points to.

When removing symbolic links to directories, avoid unnecessarily using recursive or force options.

Mental model: 

'rm symlink' -> remove the link

Do not treat a symbolic link like the directory it points to

### Hard Links After Removing a Filename 

Hard links are multiple filenames that reference the same inode. 

Example: 

'touch newfile'

'ln newfile linkedfile'

Mental model:

new file. ----
             | -> Same inode -> Same data
linkedfile ---

The hard0link count is now '2'.

If:

'rm newfile'

is executed, 'linkedfile' still works because it still references the inode.

The hard-link count decreases: 

'2->1'

The underlying data remains accessible until the last hard link is removed.

### Symbolic Links After removing the Target

Create a symbolic link:

'ln -s newfile symlinkfile'

A symbolic link refers to the target's **pathname**.

If:

'rm newfile'

is executed, the symbolic link still exists, but its target pathname no longer exists. 

'symlinkfile' -> newfile -> missing'

The symbolic link is now **broken/dangling**.

### Restoring the Target Path

If 'linkedfile' is still a hard link to the original inode:

'ln linkedfile newfile'

creates another hard link named 'newfile'.

The hard-link count returns:

'1 -> 2'

Because the pathname 'newfile' exists again, a symbolic link that points to 'newfile' can resolve again.

### Mental Model

Hard link -> references the same inode

Symbolic link -> references a pathname

Remove one hard link -> other hard links still work

Remove symlink target -> symlink becomes broken

Restore target pathname -symlink can work again

'rm link' -> remove the symbolic link itself

## Working with Archives and Compressed Files

### Archives

An archive combines multiple files and directories into a single file. 

The 'tar' command is commonly used to create and manage archives. 

> 'tar' stans for ** Tape ARchiver**

By itself, 'tar' creates an archive but does **not** compress it.

### Common 'tar' Options

| Option | Purpose |
| --- | --- |
| '-c' | Create an archive |
| 'x' | Extract an arhive |
| '-t' | List archive contents |
| '-v' | Verbose output |
| '-f' | Specify the archive file |
| '-r' | Append files to an archive |
| '-u' | Update files in an archive |
| '-C' | Change directory for the operation |
| '-z' | Use gzip compression |
| '-j' | Uses bzip2 compression |
| '-J' | Uses xz compression | 

### Creating an Archive

Structure:

'''bash
tar -cvf ARCHIVE.tar SOURCE'''



