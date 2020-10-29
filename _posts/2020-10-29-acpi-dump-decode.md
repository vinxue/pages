---
layout: post
title: ACPI dump and decode on UEFI Shell
feature-img: "assets/img/pexels/computer2.jpg"
thumbnail: "assets/img/pexels/computer2.jpg"
author: vinxue
tags: [UEFI]
---

## ACPI dump and decode on UEFI Shell

ACPI can be understood as an architecture­independent power management and configuration framework that forms a subsystem within the host OS.
Fundamentally, ACPI defines two types of data structures which are shared between the system firmware and the OS: data tables and definition blocks.
This definition block byte code is compiled from the ACPI Source Language (ASL) code. ASL is the language used to define ACPI objects and to write control methods.

Usually, we need to dump ACPI table from BIOS for debugging. There is the method how to dump and decode ACPI table on UEFI Shell.

### Dump ACPI table on UEFI Shell

1. Download AcpiDump UEFI application from [ACPICA](https://acpica.org/downloads/uefi-support).
1. Copy acpidump.efi to USB drive.
1. Boot system to UEFI Shell.
1. Run: `acpidump.efi -b` to dump all ACPI tables to binary files.<br>
   AcpiDump application usage:

   ```
   FS0:\acpidump.efi -h
   Usage: acpidump [options]
   Options:
     -b                  Dump tables to binary files
     -h -?               This help message
     -o <File>           Redirect output to file
     -r <Address>        Dump tables from specified RSDP
     -s                  Print table summaries only
     -v                  Display version information
     -z                  Verbose mode
   Table Options:
     -a <Address>        Get table via a physical address
     -c <on|off>         Turning on/off customized table dumping
     -f <BinaryFile>     Get table via a binary file
     -n <Signature>      Get table via a name/signature
     -x                  Do not use but dump XSDT
     -x -x               Do not use or dump XSDT
   ```
1. Disassemble or decode binary ACPI table to file (*.dsl) by [iASL](https://acpica.org/downloads/binary-tools) tool on Windows.

   ```
   C:\ASL>iasl.exe -d dsdt.dat

   Intel ACPI Component Architecture
   ASL Optimizing Compiler version 20130117-32 [Jan 17 2013]
   Copyright (c) 2000 - 2013 Intel Corporation
   Loading Acpi table from file dsdt.dat
   Acpi table [DSDT] successfully installed and loaded
   Pass 1 parse of [DSDT]
   Pass 2 parse of [DSDT]
   Parsing Deferred Opcodes (Methods/Buffers/Packages/Regions)
   Parsing completed
   Disassembly completed
   ASL Output:    dsdt.dsl - 116334 bytes
   ```
   Get `dsdt.dsl` file for decoded ACPI table.
