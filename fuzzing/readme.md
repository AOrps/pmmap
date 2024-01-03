# fuzzing

## afl

### Tool afl Utilies
- `afl-gotcpu`: checks cpus available
- `afl-whatsup`: status checker for afl-fuzz (check processes)


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
  - BASE: `afl`
  - EXTRA: `git`,`gdb`,`llvm`,`python3`,`python3-venv`,`screen`
  - Full Command :`sudo apt install -y afl gdb git llvm python3 python3-venv screen`


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

| Binary | Environment 
| :---   | :----
| `afl-gcc`/`afl-g++` | gcc
| `afl-clang`/`afl-clang++` | Clang
| `afl-clang-fast`/`afl-clang-fast++` | LLVM


### Finding a test corpus
- Use files from unit/integration tests
  - Look for source code repo/github/sample folders

- Look at [Optimizations](#Optimizations) for optimizations on the corpus

```bash
# for a generic corpus in *nix based systems
for i in {0..4}; do dd if=/dev/urandom of=seed_$i bs=64 count=10; done
# create 5 seeds of random data
```


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


```bash
# to fully leverage and best ui for afl-multicore fuzzer,
# example:
screen -dmS fuzz01 /bin/bash -c "afl-fuzz -i ./corpus -o ./output -M fuzz01 -- ./simple @@"
screen -dmS fuzz02 /bin/bash -c "afl-fuzz -i ./corpus -o ./output -S fuzz02 -- ./simple @@"
screen -dmS fuzz03 /bin/bash -c "afl-fuzz -i ./corpus -o ./output -S fuzz03 -- ./simple @@"
screen -dmS fuzz04 /bin/bash -c "afl-fuzz -i ./corpus -o ./output -S fuzz04 -- ./simple @@"

## to get into screen: `screen -rd <screen_input>`, ex: `screen -rd fuzz01`
## to get out of screen, without killing process: `C-a d`
```

- Fuzzer Options:
  - `-m <MEGABYTES>` : max memory usage
  - `-t <MILLISECONDS>` : timeout for each run

### Triage the findings
- Compile without afl, and run test case with 'normal compile'
- GDB with [exploitable](https://github.com/jfoote/exploitable)


The best way, that I have discovered to triage is to use: [AFLTriage](https://github.com/quic/AFLTriage). It requires cargo to compile it. Here is an example of usage:

```bash
# template
./target/debug/afltriage -i <FUZZ_CRASH_DIR> -o <OUT_DIR> <TARGET_BINARY>

# example
## double-check on conventional binary
./target/debug/afltriage --stdin -i ~/project/fuzz/out/fuzzNum/crashes/id\:0000* -o project-fuzz-report ~/project/build/proj-bin

## better analyzing on the crash via afl
./target/debug/afltriage --stdin -i ~/project/fuzz/out/fuzzNum/crashes/id\:0000* -o project-fuzz-report ~/project/afl-build/proj-bin
```
1. Double check that the
1. After the double-check, run the 

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