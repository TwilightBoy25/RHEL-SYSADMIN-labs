
# RHCSA 10 — Chapter 5: Working with Local Consoles

> **Study resource:** Red Hat RHCSA 10 Cert Guide (EX200)  
> **Environment:** Red Hat Enterprise Linux 10  
> **Topics:** Consoles, terminals, root access, virtual terminals, and pseudo terminals

---

## 1. Understanding Consoles and Terminals

### Console
A console is the environment through which a user interacts with the Linux system.

- Can provide a graphical or text-based interface.
- A graphical console can have multiple terminal windows.
- A text console typically provides direct access to a shell.

### Terminal
A terminal provides an interface for interacting with a shell, typically Bash.

- Accepts commands from the user.
- Can run inside a graphical environment.
- Can also be accessed remotely through SSH.

### Shell
A shell is a command interpreter that executes commands.

**Example:** Bash is the default shell for many RHEL users.

**Key distinction:**
- Console = Interaction environment
- Terminal = Command-line interface
- Shell = Command interpreter

---

## 2. Logging In to a Local Console

Linux systems can provide two common login environments:

**Graphical login**
- Uses a graphical display manager, such as GDM.
- Allows users to access a desktop environment.

**Text-based login**
- Presents a login prompt without a graphical desktop.
- Common on servers without a GUI.

### Best Practice: Avoid Direct Root Login

The root account has unrestricted administrative privileges.

Working as root unnecessarily increases the risk of accidental changes.

Instead:
1. Log in using a regular account.
2. Elevate privileges when necessary.
3. Return to your regular shell when finished.

---

## 3. Root Access: sudo
