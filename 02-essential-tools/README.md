# Essential Tools

## Objective

To learn the basic Linux skills needed to take the RHCSA exam.

## Concepts Learned

- Basic Shell Skills
- Editing Files with vim
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

