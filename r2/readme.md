# r2 / radare2

## 
```sh
r2 -AA -e bin.cache=true -d <exe> <arg1..n>
```
- `-AA`: aaaaa in auto-start
- `-e bin.cache=true`: fix relocations in disassembly
- `-d`: start debugger

### After Getting In
- `afl`: get list of functions in a binary
