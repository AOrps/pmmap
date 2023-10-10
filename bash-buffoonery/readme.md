# Bash Buffoonery

## bc output to sorted by second field
```bash
echo "
105*1.6
168.0
65*2.5
162.5
85*2.5
212.5
50*3
150
95*1.75
166.25
110*1.5
165.0" | grep -v '*' | cat -b | sort -n -k2 -r | cat -b
```
- `grep -v '*'` is responsible for getting all the output that is not a calculation
- `cat -b` to enumerate the numbers there
- `sort -n -k2 -r` reverse sort (highest first) at second field (`-k2`) on numeric values (`-n`)
- `cat -b` to enumerate the line there
