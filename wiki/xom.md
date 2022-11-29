# eXecute Only Memory (XOM)
A rare and effective mitigation for preventing Reverse Engineering (RE) is eXecute Only Memory (XOM). The PS5 is one of the only (if not the only) x86-based system that utilizes it, as it was pioneered by [ARM](https://community.arm.com/arm-community-blogs/b/architectures-and-processors-blog/posts/what-is-execute-only-memory-xom). It effectively prevents read accesses to certain memory regions or pages via the page tables. When a memory read operation is processed by the CPU, the Page Table Entry (PTE) is checked for the accessed address range, and if the XOM-bit is set, an exception is raised. This exception is then handled by the [hypervisor](/ps5-wiki/hypervisor). On an uncompromised hypervisor, this results in a kernel panic and the system will crash.

XOM is present in both userland and kernel.

## Userland
On PS5 titles and system apps, XOM will be enforced. This means it is no longer possible to dump userland libraries and modules without a kernel exploit or some other bug. With kernel read/write, it is possible to disable XOM via flipping the bit on userland Page Table Entries (PTEs). It's worth noting you would also have to flush the [Translation Lookaside Buffers (TLBs)](https://en.wikipedia.org/wiki/Translation_lookaside_buffer) for these changes to take effect.

## Kernel
The kernel will also use XOM to protect its' own .text pages. Disabling XOM in the kernel will likely require compromising the hypervisor or cirvumenting with some form of hardware attack, as the page tables are shadowed with nested paging. This presents a chicken and egg problem, as compromising the hypervisor will be difficult without the ability to do any RE on the kernel.
