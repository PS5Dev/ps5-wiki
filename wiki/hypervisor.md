# Hypervisor
The PS5 utilizes a presumably custom hypervisor (HV) to protect the kernel. It protects the integrity of the [Control Registers (CRs)](https://en.wikipedia.org/wiki/Control_register), which by extension includes Write Protection (WP) and other protections such as [Supervisor Mode Access/Execution Prevention (SMAP/SMEP)](https://en.wikipedia.org/wiki/Supervisor_Mode_Access_Prevention). It also protects the kernel page table entries through the use of nested paging via [Second Level Address Translation (SLAT)](http://developer.amd.com/wordpress/media/2012/10/NPT-WP-1%201-final-TM.pdf). Through seeing the [hypercalls](https://playstationdev.wiki/ps5devwiki/index.php/Hypervisor) documented on the psdevwiki, it seems Sony has also moved the I/O memory management unit (IOMMU) to the hypervisor from the kernel.

## Hypercalls
The HV has very few syscalls compared to the PS3 at only 16 (as of 3.00). Little information is known about them as of yet beyond the call names via the psdevwiki.

## Importance
Since patching the kernel is the most straightforward and direct way to achieve true homebrew, bypassing or compromising the HV is necessary. Without an HV bypass/compromise, you're essentially limited to data-only attacks in kernel and userspace.
