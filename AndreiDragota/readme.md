# Andrei Dragota

## 23 June 2025
During the day I recapped most of Rust's programming language intrinsics by going through https://tourofrust.com/TOC_en.html, finished 8 chapters out of 9.'
Wrote some notes and asked questions around the office for things I didn't catch on at first. Will finish last chapter tomorrow

## 24 June 2025
Finished the last chapter on Tour of Rust, started working on a issue on GitHub project regarding x86 architecture on Tock. Wrote a basic kernel with a VGA (text) buffer and added support for simple unit tests. Installed QEMU emulator to boot the kernel on a virtual machine to test it out, and to also write via serial UART on console. Tomorrow I will move on to the next topics regarding exceptions, timeouts, etc.

## 25 June 2025
Explored everything about CPU interrupts and exceptions. Wrapped up the testing part. Updated my kernel to support handling for double/triple faults, support for GDT, TSS, IDT, from the x86_64 crate. Ready to move on to hardware interrupts based on Intel 8259 PIC.

## 26 June 2025
Finished hardware interrupts, manage to solve deadlock + race conditions issues on my testing kernel. By also implementing the hlt instruction, I managed to get keyboard support on my kernel, now I can write "Hello World" and the system won't crash. Next, I read all about paging (theory + some implementation). Toyed around with address computation, seems difficult. I'll see tomorrow!

## 27 June 2025
Started working on implementing translation between physical and virtual addresses. Fixed an issue in my kernel where I couldn't invoke a private function from memory.rs to read the 4th page table's contents in main.rs. Moved on with implemeting address maping and frame allocation, will finish it next week. Also learnt how to use helix editor and [`zellij`](https://zellij.dev) window manager.

## 30 June 2025
Wrapped up paging implementation by creating a maper and a frame allocator. Moved on with heap allocation, learnt about static and local variables, implemented an allocator interface and a heap memory stack. Finally added and debugged testing framework from last week in order to add heap memory tests, took quite a while but it's working.

## 1 July 2025
Finally finished the whole memory management chapter. I learnt how to design memory allocators by implementing bump, linked lists and fixed-size block allocator. Moved on to the final chapter, multi-tasking. Fiddled with async/await feature and multitasking, will add soon support for this in my basic kernel, then I will learn a bit about pinning in this context. Learnt the file structure/architecture for TockOS. I should start implementing x86 support for VGA on Tock real soon!!

## 2 July 2025
After a week and a half I finished implementing a basic kernel, today I added the last bits of pinning concept, coming with cooperative multitasking, wakers and constructors. Cloned the Tock repo and fiddled with its directories and code architecture. I managed to solve a small bug that prevented me from booting tock kernel on qemu. 

## 3 July 2025
Started working on my task of implementing a VGA driver. Wrote the peripherals to enter VGA mode and declared the const in configs. I wrote some code in order to test the resolution implementation, still have some bugs as it renders the correct resolution, but nothing is shown on screen, could be a crate loading issue or maybe the buffer is overwritten. However, everything works fine in text mode, I can print colored letters and it's working fine (still no keyboard support for VGA though).

## 4 July 2025
Debugged and tested my implementation from previous day. I also started adding scrolling support, will flesh it out next week. Also opened my first pull request !!!  (it's in rough shape but I can fix most of the reported issues :D ) 

## 7 July 2025
Debugged the driver, moved configs inside the crates I'm working on still could not find the issue where scrolling doesn't work, will check tomorrow.

## 8 July 2025
Debugged even further, reached a certain milestone but I don't know how to continue with it, there's an issue I can't find in my code, I require some help :( . Cargo runner is implemented and also QEMU detects and opens a VGA port. However, I can't implement the scrolling test, weirdly enough if I map some colored text directly on the exposed buffer it works but printing 200 lines doesn't.

## 9 July 2025
Finally found why it wasn't working. Basically since I wrote directly in main.rs some scrolling tests I found out why it was not reading from my vga.rs. Basically : Direct in main.rs → used read_volatile/write_volatile per cell → works . In vga.rs → I used ptr::copy (non-volatile) → compiler caches it away → no visible scroll. Next time I will switch to the per-cell volatile loop and hopefully it will act the same. But it feels good to finally know what the issue was ◝(ᵔᗜᵔ)◜!

## 11 July 2025
Fully implemented the VGA driver, had some issues with Git while making commits, opened a new PR with all the changes to keep things fresh https://github.com/WyliodrinEmbeddedIoT/tock/pull/33

## 14 July 2025
Started work on https://github.com/WyliodrinEmbeddedIoT/tock/issues/23, read all about PS/2 controllers on https://wiki.osdev.org/I8042_PS/2_Controller and implemented some code as basis, check https://github.com/WyliodrinEmbeddedIoT/tock/pull/34 commits

## 15 July 2025
Worked with @SeriouslyAndy on https://github.com/WyliodrinEmbeddedIoT/tock/pull/34, implemented most of the requirements including HIL, full initialisation for the peripheral and interrupts handling shenaningans. Should maintain it until further review changes.

## 16 July 2025
Finished up the 8042 driver and debugged it even further. LGTM. I started working on a keyboard driver over 8042. Read all about it on https://wiki.osdev.org/PS/2_Keyboard . Our final goal is to port the whole process console from UART serial to VGA... which will take a while but I think it will be fun :D. 

## 17 July 2025
Read all about process console and VGA Text implemenation on that console. I came up with a plan to swap the UART serial console with a VGA one. First, I need to make sure that the keyboard is working fine on that 8042 peripheral. Then I can start working on the text console. After I'm done with testing out the VGA console, then I can swap them out and test them further. I split a bigger issue in 2 smaller ones to keep things organized. https://github.com/WyliodrinEmbeddedIoT/tock/issues/36

## 18 July 2025
I'd say the keyboard is 50% implemented, all of the tests at the driver level seem to pass, we just need to clean up the init in the PS/2 controller to let other devices connect. Next thing would be to write a small capsule for future VGA implementation and test the keyboard even more (and ofc. to run make prepush and solve those small issues :D ) https://github.com/WyliodrinEmbeddedIoT/tock/pull/35 

## 23 July 2025
Finished up and polished the whole keyboard driver. Hopefully it works now. Next step would be to combine VGA + 8042 + Keyboard in order to add the text capsule over the keyboard.
