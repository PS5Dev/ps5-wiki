# Hypervisor
The PS5 utilizes a presumably custom hypervisor (HV) to protect the kernel. The hypervisor is a virtual machine monitor (VMM), where the kernel and userland applications (such as games) run in a guest OS. Hardware as well as the x86 kernel talk to the hypervisor through hypercalls and [memory-mapped I/O (MMIO)](https://en.wikipedia.org/wiki/Memory-mapped_I/O). It can be considered the highest privilege level for x86 on the system.

The more conventional use of a hypervisor is to run separate virtual machines on a host machine that are isolated from each other and can run their own guest operating systems. In the PS5s case, it's used primarily for Virtualization Based Security (VBS) to protect the kernel integrity.

It protects the integrity of the [Control Registers (CRs)](https://en.wikipedia.org/wiki/Control_register), which by extension includes Write Protection (WP) and other protections such as [Supervisor Mode Access/Execution Prevention (SMAP/SMEP)](https://en.wikipedia.org/wiki/Supervisor_Mode_Access_Prevention). It also protects the kernel page table entries through the use of nested paging via [Second Level Address Translation (SLAT)](http://developer.amd.com/wordpress/media/2012/10/NPT-WP-1%201-final-TM.pdf). By looking at the [hypercalls](https://playstationdev.wiki/ps5devwiki/index.php/Hypervisor) documented on the psdevwiki, it seems Sony has also moved the I/O memory management unit (IOMMU) to the hypervisor from the kernel.

## Hypercalls
The HV has very few syscalls compared to the PS3's at only 16 (as of 3.00). Little information is known about them as of yet beyond the call names.

## Importance
Since patching the kernel is the most straightforward and direct way to achieve true homebrew, bypassing or compromising the HV is necessary. Without an HV bypass/compromise, you're essentially limited to data-only attacks in kernel and userspace.
