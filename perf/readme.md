# perf
- Performance analysis tools for Linux

## For General Statistics
```sh
# Template
perf stat -o <OUT> <CMD>

# Example
perf stat -o perf-stat.data -- ./bash-script.sh
```


## For Profiling

- `-g` : To enable callgraphs

### To Record
```sh
# Template
perf record -g <CMD>

# Example
perf record -g ./bash-script.sh
```

### To Report
```sh
# Template and Example
perf report -g
```


