---
title:  "Internship in CompSec 🧑‍💻"
excerpt: "My experiences in CompSec!"
toc: true
toc_sticky: true

categories:
  - Writing
---

I have been an intern at [CompSec](https://compsec.snu.ac.kr/) since last December, and I would like to share what I have learned during my time here. 

## Software Security

I first solved various problems given as assignments in the class called [Software Security](https://github.com/lifeasageek/snu-software-security-public/tree/spring-21). You can find details of the assignments and my solutions **[here](https://www.notion.so/snu-software-security-754d430013a94d2599faf34a0e19720a)**.

First, I solved three pwnable-like problems about **stack overflow** and **heap overflow**. Since it wasn't my first time solving pwnable problems, it didn't take much time for me to solve them.

---

The [second assignment](https://github.com/lifeasageek/snu-software-security-public/tree/spring-21/prog-assign-1) was to implement an **integer overflow checker** using **LLVM**.I had to **check if integer overflow occurred** in the given C code, and if the **overflowed value flowed into the argument of `malloc`** using an LLVM pass. Before I started this assignment, I had no knowledge of LLVM, so I had to first study its architecture. The documents provided in the assignment were very helpful:

- [LLVM Architecture](https://www.aosabook.org/en/llvm.html)
- [Writing an LLVM Pass](https://llvm.org/docs/WritingAnLLVMPass.html)

With this assignment, I could learn about how LLVM works, and how to write a LLVM pass. 

---

Next two assignments were to **implement a [compare coverage](https://andreafioraldi.github.io/articles/2019/07/20/aflpp-qemu-compcov.html) feature for AFL** to make it bypass strong constraints much faster.

[First assignment](https://github.com/lifeasageek/snu-software-security-public/tree/spring-21/prog-assign-2) was to implement the **LLVM pass** that transforms the target program to benefit AFL using the idea of CompareCoverage. I had to insert an additional code transformation logic using **AFL's llvm-mode**.

[Second assignment](https://github.com/lifeasageek/snu-software-security-public/tree/spring-21/prog-assign-3) was to do the same thing, but by taking **binary-based transformation**, using the **AFL's QEMU-mode**. To finish this assignment, I had to understand **how AFL works** (coverage measurements) and **what QEMU is**, and **how to modify it using TCG**. Documents below helped me a lot:

- **[How AFL works](https://afl-1.readthedocs.io/en/latest/about_afl.html#coverage-measurements)** - Coverage measurement & Detecting new behaviors
- [Documentation/TCG/frontend-ops](https://wiki.qemu.org/Documentation/TCG/frontend-ops)

## Xv6

After finishing the assignments above, I studied **how OS works** by implementing some features in **Unix-like simple OS, [Xv6](https://pdos.csail.mit.edu/6.828/2022/xv6.html)**. 

I had a general understanding of computer systems from my System Programming class, but most of the kernel's functions were not covered. Thanks to Xv6, I was able to comprehend how the kernel works and how it interacts with user space. Detailed code can be found in my [Xv6 repository](https://github.com/cw00h/xv6).

Main features that I developed in Xv6 are as follows:

- **Basic system calls**: [trace](https://github.com/cw00h/xv6/commit/ee2f0a2486864e09a6964eec3e41e5608259f44f), [sysinfo](https://github.com/cw00h/xv6/commit/b62297c310808c3135104069183d7f01982777fa) system calls
- **Page table**: [pgacess](https://github.com/cw00h/xv6/commit/ee4d06b91827a9978dcdec8d17716002980f3897) system call that prints which page has been accessed
- **Trap**: [backtrace](https://github.com/cw00h/xv6/commit/b20c93166afa1487c0479568e65503a8c33e62a8) function that shows a list of the functions that were called before the error happened, [sigalarm & sigreturn system calls](https://github.com/cw00h/xv6/commit/53673b6f9827f538dca02e729b457096951de486)
- **Copy-on-Write**: Implemented a [Copy-on-Write feature](https://github.com/cw00h/xv6/commit/36f1e31f05d7263961cd5bcbfb26bc202b774a07) in Xv6.
- **Multithreading**: Implemented **[a context switch mechanism](https://github.com/cw00h/xv6/commit/49b1e5e761e9fff2049a16f099e9948a9d61e338)** for **user-level threading system**.
- **Networking**: Implemented [functions for the network driver to transmit and receive packet](https://github.com/cw00h/xv6/commit/baf0049dbc627b9f9e6d2293fb1d328368c9a58c)s.
- **File System**: [symlink](https://github.com/cw00h/xv6/commit/ec32e20f2d422e675c0733b421227df99b28565f) system call & [Increased the maximum size of an xv6 file](https://github.com/cw00h/xv6/commit/9f1aa1972d537470750e853068a811147dd3f0aa).
- **mmap**: [mmap, munmap](https://github.com/cw00h/xv6/commit/6150bf4427c35d16fdc5443f410fdedb80828868) system call

## kvm-hello-world

I studied hypervisor by exploring [**kvm-hello-world**](https://github.com/cw00h/kvm-hello-world), a simple example program demonstrating the use of the KVM API provided by the Linux kernel. To deepen my understanding, I followed the assignments of a lecture I found on Google: **[Build your own hypervisor using the KVM API](https://www.cse.iitb.ac.in/~mythili/virtcc/pa/pa1.html)**.

First, to understand the structure of kvm-hello-world, I answered several questions in the page above. You can check the answers I wrote [here](https://github.com/cw00h/kvm-hello-world/blob/master/answers.txt).

Next, I added some **new hypercalls** according to the instructions. The hypercalls I added are:

- [printVal](https://github.com/cw00h/kvm-hello-world/commit/ab50a51d11767224cf585d1d7df2521bbc099856) printing the 32-bit value given as argument to the screen.
- [getNumExits](https://github.com/cw00h/kvm-hello-world/commit/74c32b06d0b3666517b18215f3d158d3a610f2db) returning the number of exits incurred by the guest since it started.
- [display](https://github.com/cw00h/kvm-hello-world/commit/7ca6babe5060c33aa502c1a304b3109195f53ef8) printing the string given as argument to the screen, incurring only one guest exit.
- File system hypercalls: [open](https://github.com/cw00h/kvm-hello-world/commit/67ddf8d773e2cee65509b4b2ef3c2c606989ea93), [read](https://github.com/cw00h/kvm-hello-world/commit/dd68aba29fe8ab6f292c6b35fa7db2d5cabbddfd), [write](https://github.com/cw00h/kvm-hello-world/commit/142c4f6dbf774ba34d1695c28244b2e9498efa5b)

By understanding **how the KVM API works**, I could know **how to operate KVM** - how to set up virtual machines and how to communicate with them. I also learned that KVM is an essential part of cloud computing and virtualization technologies. 

## Reading papers

After studying topics related to computer systems, such as operating systems, hypervisors, and fuzzers, I began reading papers on software security. Many papers from Compsec focus on fuzzing or confidential computing using Intel SGX, so I started there. The papers I am reading or plan to read in the future can be found in my notion [page](https://www.notion.so/cw00h/Research-Paper-2f38f4ea021848f9bdec36a48df20928?pvs=4).

## Conclusion

Through my internship at CompSec, I was able to gain a lot of knowledge and experience related to operating systems, hypervisors, fuzzing, and confidential computing. Although my internship has not yet ended, I feel that I have gained a lot of knowledge and experience that will be useful in the future. I plan to stay with CompSec until at least this summer. I'm looking forward to gaining more experiences during this internship. 😎 Also, I'd like to express my gratitude to everyone at Compsec for helping me have such a wonderful experience. ❤️