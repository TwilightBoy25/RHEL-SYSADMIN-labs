# RHEL Environment Setup

## Objective

Set up a Red Hat Enterprise Linux VM to use as my primary hands-on lab environment while developing Linux system administration skills and preparing for the RHCSA exam.

## Lab Environment

- **Host Machine:** Dell Precision
- **Hypervisor:** Microsoft Hyper-V
- **Guest OS:** Red Hat Enterprise Linux 10
- **Architecture:** x86-64

## Environment Architecture

```text
Dell Precision -> Hyper-V -> RHEL Virtual Machine
```

This environment will serve as my primary RHEL system for practicing Linux administration, configuration, troubleshooting, and RHCSA objectives.

## RHEL Installation

- **RHEL Version:** 10
- **Architecture:** x86-64
- **Memory:** 4096 MB (4 GB)
- **Network Configuration:** Default
- **Hostname:** Not yet confirmed
- **User Account:** `student`

### PXE Boot Issue

When I first started the RHEL VM in Hyper-V, the VM displayed:

```text
Start PXE over IPv4
```

This occurred because Hyper-V could not find a bootable device and attempted to boot from the network using PXE.

### Resolution

- Shut down the VM.
- Opened the VM settings in Hyper-V.
- Mounted the RHEL Boot ISO to the virtual DVD drive.
- Verified that the DVD drive was above the network adapter in the VM's boot order.
- Opened the Security settings and changed the Secure Boot template to **Microsoft UEFI Certificate Authority**.
- Restarted the VM and successfully booted into the RHEL installer.

## Installation Verification

After completing the installation, I verified the installed RHEL version with:

```bash
cat /etc/redhat-release
```

I also checked the system information using:

```bash
hostnamectl
```

These commands confirmed that the RHEL installation was running successfully inside the virtual machine.

## What I Learned

During the initial setup, I learned how Hyper-V determines which device a virtual machine attempts to boot from.

PXE (Preboot Execution Environment) allows a computer to boot using resources provided over a network. Seeing the `Start PXE over IPv4` message can indicate that the VM did not find another bootable device earlier in its boot order.

I also learned that when configuring a Linux virtual machine in Hyper-V, both the boot order and Secure Boot configuration can affect whether the installation media boots successfully.

## Next Steps

With the base RHEL installation complete, my next steps are to:

- Configure and verify networking
- Configure the system hostname
- Update installed packages
- Explore the RHEL command-line environment
- Configure SSH for remote administration
- Begin practicing RHCSA system administration tasks

