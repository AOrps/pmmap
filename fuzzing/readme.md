# fuzzing

## afl

### Workflow
```mermaid
# TODO
```
1. Compile binary with AFL
1. Find a test corpus
1. Run the fuzzer
1. Triage the findings
1. Success?


### Installation
- Debian/Ubuntu:
  - `apt install -y afl`


### Compilation
```bash
export CC=afl-clang-fast
export CXX=afl-clang-fast++
export AFL_HARDEN=1
export AFL_INST_RATIO=100
./configure
make
```
- `CC`/`CXX` : change default C/C++ compilers
- `AFL_HARDEN` : adds code hardening
- `AFL_INST_RATIO` : instrumentation ratio 

### Finding a test corpus
- Use files from unit/integration tests
  - Look for source code repo/github/sample folders

- Look at [Optimizations](#Optimizations) for optimizations on the corpus

### Run the fuzzer
```bash
# Generic Usage
afl-fuzz -i <TEST_CASES> -o <OUTPUT> <FUZZ_OPTIONS> -- <BINARY> <BINARY_OPTIONS> @@
```

```bash
# For Multi-core mode
afl-fuzz -i <TEST_CASES> -o <OUTPUT> -M fuzzer01 -- <BINARY> <BINARY_OPTIONS> @@
afl-fuzz -i <TEST_CASES> -o <OUTPUT> -S fuzzer02 -- <BINARY> <BINARY_OPTIONS> @@
afl-fuzz -i <TEST_CASES> -o <OUTPUT> -S fuzzer03 -- <BINARY> <BINARY_OPTIONS> @@
afl-fuzz -i <TEST_CASES> -o <OUTPUT> -S fuzzer04 -- <BINARY> <BINARY_OPTIONS> @@
```
- Need to use the same `<OUTPUT>` in Multi-core mode


- Fuzzer Options:
  - `-m <MEGABYTES>` : max memory usage
  - `-t <MILLISECONDS>` : timeout for each run

### Triage the findings



### Optimizations
- Minimize the list of the cases (CORPUS)
```bash
afl-cmin -i <INPUT_DIR> -o <OUTPUT_DIR> -- <BINARY> <OPTIONS TO BINARY> @@
```

-  Minimize each test file (CORPUS)
```bash
afl-tmin -i <TEST_CASE_FILE> -o <MINIMIZED_FILE> -- <BINARY> <OPTIONS TO BINARY> @@
```


### Resources
- https://youtu.be/DFQT1YxvpDo?si=XeuTfIH6wVVxtDPg