# OS/Unix, OSDev, binary exploitation and random shit

## Resources

[The little OS book](http://littleosbook.github.io/#about-the-book)
[Operating Systems - Andrew Tanenbaum](https://github.com/smellslikekeenspirit/an-askreddit-list-of-compsci-books/blob/master/Modern%20Operating%20Systems%204th%20Edition--Andrew%20Tanenbaum.pdf)
[Wiki - OSDEV](https://wiki.osdev.org/)
[How the Kernel manages your memory](https://manybutfinite.com/post/how-the-kernel-manages-your-memory/)
[Itanium Linux ABI - LSB](https://refspecs.linuxbase.org/)

## Memory

### Paging

>Paging is a system which allows each process to see a full virtual address space, without actually requiring the full amount of physical memory to be available or present.

>Paging is achieved through the use of the Memory Management Unit (MMU).

[Virtual Memory: How does Virtual Memory Work](https://www.youtube.com/watch?v=59rEMnKWoS4)

## Permissions

### Permission rings



## Virtualization

### Virtualization vs Hypervisors

Ring1 can be used to create an emulated real mode (ring0).
[Linux Architecture - Securing The Stack - Youtube(https://www.youtube.com/watch?v=85eINAowuMc)

## Unix
### Suid, setuid, setreuid

[SUID, SEUID, EUID](https://www.osso.nl/blog/setuid-seteuid-uid-euid/)

### LD_PRELOAD

[https://stackoverflow.com/questions/9232892/ld-preload-with-setuid-binary](LD_PRELOAD with setuid - Stack Overflow)

### Pipes

[Unix Pipe Implementatin](https://toroid.org/unix-pipe-implementation)

## Compilation

### ELF Format

[In-depth: ELF - The Extensible & Linkable Format](https://www.youtube.com/watch?v=nC1U1LJQL8o)
[Core files analysis - Stackoverflow](https://stackoverflow.com/questions/5115613/core-dump-file-analysis#:~:text=You%20just%20need%20a%20binary,the%20time%20of%20the%20crash.)

### ASLR

```sh
$ echo 1 | sudo tee /proc/sys/kernel/randomize_va_space
1
$ ./a.out
executable: 0x400677
stack: 0x7fff0561a30c
heap: 0x602010
system@plt: 0x400550
libc: 0x7ff03b6e79b0
system: 0x7ff03af64480
$ ./a.out
executable: 0x400677
stack: 0x7fffe76dd26c
heap: 0x602010
system@plt: 0x400550
libc: 0x7f063ddf79b0
system: 0x7f063d674480
```
[Memory corruption protection - ASLR](https://www.proggen.org/doku.php?id=security:memory-corruption:protection:aslr)

### PIE + ASLR

```shell
$ echo 2 | sudo tee /proc/sys/kernel/randomize_va_space
2
$ ./a.out
executable: 0x55e8208157ca
stack: 0x7ffe5d194edc
heap: 0x55e821d11010
system@plt: 0x7f2904b01480
libc: 0x7f29052849b0
system: 0x7f2904b01480
$ ./a.out
executable: 0x55716e0817ca
stack: 0x7ffd23f4e40c
heap: 0x55716ee0e010
system@plt: 0x7fe427397480
libc: 0x7fe427b1a9b0
system: 0x7fe427397480
```
[Memory corruption protection - PIE](https://www.proggen.org/doku.php?id=security:memory-corruption:protection:pie)

### GOT and PLT

[GOT and PLT for pwning - System Overlord](https://systemoverlord.com/2017/03/19/got-and-plt-for-pwning.html#:~:text=plt%20contain%20stubs%20to%20jump,sections%20as%20we%20go%20along.)

## Pwn

### Shellcoding

#### Metasploit 
```

```
[Carving shellcode using restrictive charset](https://web.archive.org/web/20190218144432/https://vellosec.net/2018/08/carving-shellcode-using-restrictive-character-sets/)
[Alphanum shellcode](https://blackcloud.me/Linux-shellcode-alphanumeric/)