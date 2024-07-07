# bpf

## BCC (bpf Compiler Collection)
- Toolkit for creating efficient kernel tracing and manipulation programs. 

## Maps
- Generic Data structure for storage of different types of data.

### Code Example
```c
BPF_HASH(counter_table)
```
- This is a macro that bpf.c allows us to use what is effectively a binary blob with an arbitrary structure. 
