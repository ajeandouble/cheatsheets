# OS/Unix, OSDev, binary exploitation and random shit

## Resources

[The little OS book](http://littleosbook.github.io/#about-the-book)
[Operating Systems - Andrew Tanenbaum](https://github.com/smellslikekeenspirit/an-askreddit-list-of-compsci-books/blob/master/Modern%20Operating%20Systems%204th%20Edition--Andrew%20Tanenbaum.pdf)
[Wiki - OSDEV](https://wiki.osdev.org/)
[How the Kernel manages your memory](https://manybutfinite.com/post/how-the-kernel-manages-your-memory/)

## Memory

### Paging

>Paging is a system which allows each process to see a full virtual address space, without actually requiring the full amount of physical memory to be available or present.

>Paging is achieved through the use of the Memory Management Unit (MMU).

[Virtual Memory: How does Virtual Memory Work](https://www.youtube.com/watch?v=59rEMnKWoS4)

## Permission rings
### Permission rings

### Suid, setuid, setreuid

[SUID, SEUID, EUID](https://www.osso.nl/blog/setuid-seteuid-uid-euid/)

## Virtualization

### Virtualization vs Hypervisors

Ring1 can be used to create an emulated real mode (ring0).
[Linux Architecture - Securing The Stack - Youtube(https://www.youtube.com/watch?v=85eINAowuMc)

## Unix

### LD_PRELOAD

[https://stackoverflow.com/questions/9232892/ld-preload-with-setuid-binary](LD_PRELOAD with setuid - Stack Overflow)

### Pipes

[Unix Pipe Implementatin](https://toroid.org/unix-pipe-implementation)
