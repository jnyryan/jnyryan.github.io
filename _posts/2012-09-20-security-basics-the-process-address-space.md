---
layout: post
title:  "Security Basics: The Process Address Space"
date:   2012-09-20 00:00:00
categories: forensics-and-security
tags: [security, processes]

---

To understand the security aspects of software, it’s important to know how the operating system treats software and how it’s shored and accessed during execution. This article is aimed at refreshing engineers memories who have already touched this subject even though it may have been many years ago.
<linebreak>

The Process address space is the environment set up by the operating system in which the process can execute. The program is just a collection of instructions and data sitting on the disk and do needs a structure that is defined and usable to run its instructions. When code is compiled, the instructions are stored in the .text segment, the execution engine then knows where to begin execution and it steps over the instructions in this space. If the program had global data then this would be stored in the data segment and local variables to functions are stored in the stack or heap. A diagrammatic representation of this could be a box separated into areas that represent different logical segments of the address space.

###High Level look at the address space

|Address Space Segments|Description|
|------------------------------------|----|
|kernel|	Top 1/4 of process address space is reserved for the kernel.|
|environment|	Set of environment variables that program inherits from the context in which it was launched. e.g.path|
|command line parameters|	all arguments passed to the process are stored in the process address space|
|stack|	Stores all data to do with executing functions, local variables, return addresses, frame pointers etc.|
|heap|	This is used for dynamic memory allocation, when an executing function requires dynamic memory it mus allocate it manually on the heap and then free it once it’s finished.|
|dlls|	All shared objects will be stored here e.g. standard c lib
|rodata|	read only data associated with the process|
|data|	initialized global data (r/w)|
|bss|	all uninitialized global variables are stored here (e.g. char buffer[4096];)|
|text|	This contains the instructions that make up the executable.The instruction pointer moves over this area executing each entry and jumping around it according to the specific instructions. This section is read only and attempting to write to it results in an segmentation error|

So what does all this look like outside of friendly dumbed down diagrams? Well to answer that we’re going to write a small amount of c code and compile it in debugger mode so that we can use the GNU Debugger to have a look at it in a bit more detail.
	
{% highlight c %}
//hello.c
#include <stdio.h>
int main(int argc, char **argv)
{
printf("Hello");
return 0;
}
{% endhighlight %}
 
Compile the c code below in the shell using
{% highlight bash %}
> gcc -g -o hello hello.c
{% endhighlight %}
	
You can now view the process space information uning the GNU Debugger.

{% highlight bash %}
> gdb hello
(gdb) info file
{% endhighlight %}


	Process Space Information
	/home/john/hello’, file type elf32-i386.
	Entry point: 0×8048340
	0×08048154 – 0×08048167 is .interp
	0×08048168 – 0×08048188 is .note.ABI-tag
	0×08048188 – 0x080481a0 is .note.SuSE
	0x080481a0 – 0x080481c8 is .hash
	0x080481c8 – 0x080481e8 is .gnu.hash
	0x080481e8 – 0×08048238 is .dynsym
	0×08048238 – 0×08048284 is .dynstr
	0×08048284 – 0x0804828e is .gnu.version
	0×08048290 – 0x080482b0 is .gnu.version_r
	0x080482b0 – 0x080482b8 is .rel.dyn
	0x080482b8 – 0x080482d0 is .rel.plt
	0x080482d0 – 0×08048300 is .init
	0×08048300 – 0×08048340 is .plt
	0×08048340 – 0x080484a4 is .text
	0x080484a4 – 0x080484c0 is .fini
	0x080484c0 – 0x080484ce is .rodata
	0x080484d0 – 0x080484d4 is .eh_frame
	0x08049f0c – 0x08049f14 is .ctors
	0x08049f14 – 0x08049f1c is .dtors
	0x08049f1c – 0x08049f20 is .jcr
	0x08049f20 – 0x08049ff0 is .dynamic
	0x08049ff0 – 0x08049ff4 is .got
	0x08049ff4 – 0x0804a00c is .got.plt
	0x0804a00c – 0x0804a018 is .data
	0x0804a018 – 0x0804a01c is .bss
 

What have we done here? It’s easy, we compiled the code using the GNU compiler gcc and then inspected the process address space using the GNU Debugger gdb.  The result is a representation of what a process address space looks like on a Linux box. You can clearly see the address space ranges of each section of the compiled code. What you may not see are the heap and stack as they are allocated at run time. e.g. the text section, which holds the code is located between 0×08048340 and 0x080484a4.

###Treading

What happens when we fork of a thread in a process, well here the data and heap segments are shared, but text is not. Each thread gets it’s own stack and own copy of any local variables.

###Virtual Address Space

You may ask, how does a 32 bit machine allocate 4GB of memory for the address space for each process it launches? Well, too do this the system uses a system called Virtual Memory and a process of paging to create a virtual address space, in which the executing process can still “see” the full 4GB and address is as if it were physically laid out in a block of contiguous memory. The Paging system maintains  a mapping of virtual memory to physical memory in the form of Page Directories and Page Tables. These in turn contain pointers to 4KB page frames which are created as needed to store the data.  These pages are either stored in physical memory or swapped out to disk. The CR3 register always points to the current processes page directory. It’s updated on a process context change.

 

	-> Page Table	->Page
	->Page
	->Page
	CR3 Register	-> Page Directory (1024 capacity)		-> Page Table
	(1024 Capacity)	->Page(4KB)
	-> Page Table	->Page
	->Page
	->Page
 

Total capacity on 32bit system = 1024*1024*4KB = 4GB

System Calls

System calls run inside the Kernel and run in kernel mode with elevated privileges. To invoke a system call we place in registers the parameters we want to send to the system call and then place in the EAX resister the number of the system call that we want to call. Then a software interrupt, this switches to kernel mode and the system call dispatcher takes over and executes that system call on behalf of the programming.