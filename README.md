# Big List of ABI Resources

I am interested in how Application Binary Interfaces (ABIs) are designed. Since
I got involved in helping to define the RISC-V psABI (linked below), I've tried
to collect together a lot of different and disparate resources on the ABIs I
know of, for future reference.

The main part of this repository is this README, which contains links out to the
canonical references for each ABI specification. There is also an `archive`
directory in the repository which contains copies of any publicly-available
resources which I deem to be at risk of disappearing.

**Contributing:** I am happy to accept pull requests to this repository to add
any resources or sections which are missing or incomplete.

## Introduction

### What is an ABI?

An ABI is an agreement for how software on a given platform will interoperate.
The three main parts of this agreement are:

*   The representation of values;
*   The names of values and procedures (symbols); and
*   How procedures encode arguments and return values (the Calling Convention).

These are of fundamental importance to Instruction Set, Compiler, Linker,
Operating System, and Library authors, as these are the central place where
choices can be made about software compatibility.

Most application authors will almost never have to care about defining an ABI,
but understanding the ABI of their platform might allow them to extract the
maximum performance available for their usecase.

### ABI Platforms

There are three main groups of ABI platforms in common usage in 2020:

*   The System V ABIs (Linux, most BSDs)
*   The Windows ABIs
*   The Darwin ABIs (Apple's macOS, iOS and variants)

## The System V ABIs

The System V ABI is made up of two parts:

*   The Generic ABI (gABI), which is extended per-processor by:
*   The Processor-Specific ABIs (psABIs).

The System V gABI is the specification that defines the ELF file format.

Bare-metal systems which also use ELF often follow the System-V ABI for their
processor family.

### System V gABI

The System V gABI is available here: http://www.sco.com/developers/gabi/

Older versions of the gABI, not listed on that page, are available here: http://www.sco.com/developers/devspecs/

Some operating systems have their own extensions to the System V gABI, which are
also linked below.

Several of the psABIs also reference two other ABIs, for historical reasons (usually because it's easier to take someone else's implementation and adapt it for your processor than come up with your own).

#### Intel Itanium C++ ABI

Intel went to great lengths to define how C++ should work on their Itanium
architecture. Rather than go through the process of producing
new definitions that are compatible with System V and C++'s intented semantics, most System V platforms use this ABI for C++.

In particular, this contains the definition of how exception handling (including
frame unwinding) usually works in the System V ABI.

The Itanium C++ ABI is available here: https://itanium-cxx-abi.github.io/cxx-abi/

#### ELF Handling of Thread-Local Storage

The following document describes how ELF handles thread-local storage (TLS).

The current version is 0.21: https://akkadia.org/drepper/tls.pdf

This document contains processor-specific information about TLS for IA-32 (i386), IA-64 (Itanium), SPARC (32- and 64-bit), SH, Alpha, x86-64, and S390.

Older versions are available as well:

*   (v0.20 2005-12-21) https://www.uclibc.org/docs/tls.pdf

Android has its own TLS variant, documented here: https://android.googlesource.com/platform/bionic/+/HEAD/docs/elf-tls.md

#### DWARF

ELF commonly uses a format called DWARF for representing debugging information.

The current version is DWARF 5: http://www.dwarfstd.org/doc/DWARF5.pdf

Previous versions are available here: http://www.dwarfstd.org/Download.php

The DWARF standard source is available here: http://git.dwarfstd.org/?p=dwarf-doc.git;a=summary

Thre is a discussion forum for this standard: http://lists.dwarfstd.org/pipermail/dwarf-discuss-dwarfstd.org/

### Intel x86-64 psABI

The primary 64-bit psABI is for Intel's x86-64 architecture. Other psABIs often
choose to match this psABI, unless there is a good reason not to.

This processor architecture is also called "amd64" by some vendors. Do not
confuse this with "IA-64", which denotes Intel's Itanium Architecture. Windows,
to add to the confusion, calls this architecture "x64".

The current version is 1.0: https://github.com/hjl-tools/x86-psABI/wiki/x86-64-psABI-1.0.pdf

The x86-64 psABI source is available here: https://gitlab.com/x86-psABIs/x86-64-ABI

This repository is under active development, and there are new changes every few months.

There is a discussion forum for this ABI: https://groups.google.com/forum/#!forum/x86-64-abi

### Intel i386 and IA MCU psABI

This is the psABI for Intel's 32-bit i386 architecture. This architecture is
also called "IA-32" or "x86" (without the "-64" suffix).

The current version is 1.1: https://github.com/hjl-tools/x86-psABI/wiki/intel386-psABI-1.1.pdf

The i386 psABI source is available here: https://gitlab.com/x86-psABIs/i386-ABI

There is a discussion forum for this ABI: https://groups.google.com/g/ia32-abi

#### Misc Intel ABIs:

*   IA-MCU psABI (Pentium without x87): https://github.com/hjl-tools/x86-psABI/wiki/iamcu-psABI-0.7.pdf
*   IA-64 psABI (Itanium): https://refspecs.linuxfoundation.org/elf/IA64-SysV-psABI.pdf
*   ? A 16-bit i386 ABI: https://github.com/hjl-tools/x86-psABI/wiki/intel386-psABI-16bit.pdf


### ARM Architectures

ARM have collected the psABIs for their 32-bit (AArch32) and 64-bit (AArch64) Architectures together.

ARM used to have their psABIs available as PDFs on their website, but they
redesigned it, and the specifications have became very hard to find and obtain
PDF copies of.

The ARM psABI sources are available here: https://github.com/ARM-software/abi-aa (the README contains an overview of the available documents, and links to the parts that have not yet migrated).

#### Additional ARM psABIs

*   "Function-Descriptor Position Independent Code" (FDPIC) specification: https://github.com/mickael-guene/fdpic_doc/blob/master/abi.txt (v1.0 is available in this repo as well).

    This is one solution for running GNU/Linux on platforms where processes
    share a common address space.

*   

### RISC-V psABI

The RISC-V ELF psABI is available here: https://github.com/riscv/riscv-elf-psabi-doc/blob/master/riscv-elf.md

There is a discussion forum for this ABI: https://groups.google.com/a/groups.riscv.org/g/sw-dev























### GNU/Linux gABI Extensions

There are linux-OS specific additions to the System V gABI. These are mandated as part of the "Linux System Base".

The specifications referenced from the Linux System Base are available here: https://refspecs.linuxfoundation.org

The current version is available here: https://github.com/hjl-tools/linux-abi/wiki/linux-abi-draft.pdf

These are partially documented in: https://gitlab.com/x86-psABIs/Linux-ABI

There is a discussion forum for this gABI: https://sourceware.org/pipermail/gnu-gabi/

## Further Resources

*   Agner Fog's Optimization Pages: https://www.agner.org/optimize/

*   μClibc's psABI page: https://uclibc.org/specs.html
