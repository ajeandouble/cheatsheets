# Memory

## Pages

**_...TODO_**

## Fixed page allocator

### Bump allocator

```
- Allocate a page
- Keep a pointer to the top of used memory
- Bump it at each bump alloc call
```

Sucks because you can't free parts of the memory.
Although you could wipe out the memory and reset the whole data when it's invalidated.
**Saves time from syscall**!

### Arena Allocator

It's a **_bump allocator with expandable memory_**!
The operating system provides a mechanism? With pages that it allocates and an interface. It wil lfree everything for once and for all (all the pages).
