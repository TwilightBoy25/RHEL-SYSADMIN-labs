# Essential Tools

## Objective

To learn the basic Linux skills needed to take the RHCSA exam.

## Concepts Learned

- Basic Shell Skills
- Editing Files with vim
- Editing Files with nano
- Understanding the Shell Environment

## Understanding Commands

### ls

List the files of a directory

To modify the behavior of a command you can use options. 

Example: Using "-l" with ls a long listing of filenames and properties will be displayed.

Anything you put after the command is considered an argument (including options). 

Example: Using "ls -l/etc" 

So using this command, you have two arguments (anything after the command), but specifically an option with an argument. The option being "-l" and the argument being "etc"

So the first argument "-1" is modifying the behavior of the command. The second part of the argument "etc" tells the command specifically where to work. 


## Executing Commands

The purpose of Linux shell is to provide an environment to execute commands. 

The shells takes care of interpretiung the proper command that a user inputs.

How the shells does that, interprets the command in three distinct ways.
1. Aliases
2. Internal Commands
3. External Commands

Alias is a command that a user can define as needed. Typing "alias" in the command line will show an overview of it. 
![Typing alias RHEL](screenshots/alias_overview.png)

Internal command, also known as/referred to a shell builtin. It is apart of the shell itself, so it doesn't have to be loaded from disk separately. 

External command is a command that exist as an executable file on the disk of a computer

To find out if a command is an internal command or an external command you can use the type command

![Typing type pwd in the terminal](screenshots/type_pwd.png)

To change how the shell finds an external command, use "$PATH" variable. It defines for a list of directories for the matching filename when a user enters a command. 

To find EXACTLY which command the shell will use, use the "which" command. 

![Typing which ls in the terminal](screenshots/which_ls.png)

A stronger command is "type". Which will also work on internal commands and aliases. 

echo $PATH types out the contents of the $PATH variable

## I/O Redirection

The computer monitor is used as the standard destination for output = STDOUT 
The shell also has default standard destinations to send errors messages to (STDERR) and to accept input (STDIN)

| Name | Default Destination | Use in Redirection | File Descriptor Number
| STDIN| Computer keyboard | <(same as 0<) | 0
| STDOUT| Computer monitor | >(same as 1>) | 1
| STDERR | Computer monitor | 2> | 2

