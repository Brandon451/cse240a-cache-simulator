# Project 2:  The Cache Simulator

In the second edition of our project, we are now going to simulate the behaviour of the cache in a processor. This cache will be somewhat similar to the cache present in a real processor. You will simulate an Instruction cache, a Data Cache and a Level 2 cache which is common for both instructions and data. 

## The Assignment:
We have given a framework for running the cache functions in `main.c`. You will create required data structures for the 3 caches, and functions to access these caches. Each cache will have 3 configuration settings - number of sets, associativity and hit time. You will need to calculate the statistics based on your understanding of the cache.


## Get Started
Download the code from this repository `https://github.com/Brandon451/cse240a-cache-simulator`. Once you have checked out this repository, start adding your code into this. To compile, run the following command from within the src directory: make all or make. This will compile your code and generate output files. You will also get a executable binary called "cache". 

## Testing
Once you have created the binary, you can run it with the following command:
`bunzip2 -kc trace.bz2 | ./cache <options>`
The options are as follows:
```
  --help                     Print this message
  --icache=sets:assoc:hit    I-cache Parameters
  --dcache=sets:assoc:hit    D-cache Parameters
  --l2cache=sets:assoc:hit   L2-cache Parameters
  --inclusive                Makes L2-cache be inclusive
  --blocksize=size           Block/Line size
  --memspeed=latency         Latency to Main Memory
```

The testing can be done using the traces given to you in the repository. There are 2 correct outputs given for 2 configurations as follows:
1. **MIPS R10K** - [Reference Manual](https://ieeexplore.ieee.org/abstract/document/491460?casa_token=xRyemPMXCU4AAAAA:qMm86PcKveY_y6TAegQChllzSccO4b6ILZRKKEeO_ml4HjQfav6hBbHDJeHR0TeXZCUPyjOpFQ):
   * I$: 32KB, 2-way, 2 cycles hit latency
   * D$: 32KB, 4-way, 2 cycles hit latency
   * L2: 128KB, 8-way, off-chip, 50 cycles hit latency, inclusive(we are not testing inclusivity)
   * 128B block size
   * `./cache --icache=128:2:2 --dcache=64:4:2 --l2cache=128:8:50 --blocksize=128 --memspeed=100`
2. **Alpha A21264** - [Reference Manual](https://course.ece.cmu.edu/~ece447/s15/lib/exe/fetch.php?media=21264hrm.pdf):
   * I$: 64KB, 2-way, 2 cycles hit latency
   * D$: 64KB, 4-way, 2 cycles hit latency
   * L2: 8MB, direct-mapped, off-chip, 50 cycles hit latency, inclusive(we are not testing inclusivity)
   * 64B block size
   * `./cache --icache=512:2:2 --dcache=256:4:2 --l2cache=16384:8:50 --blocksize=64 --memspeed=100`


You need to make sure that your output matches this configuration output with 2% of error margin. There will be some more hidden test cases which will test the simulator against some other configurations. 

You can test using the same docker image as Project 1, the image name is `gandhardesh13/240a_base:v2` The commands to run this would be the same as before: `docker pull gandhardesh13/240a_base:v2` to pull the image, `docker run --rm -it -v <path on local machine>/<path on ubuntu> gandhardesh13/240a_base:v2` to run it on your local machine.

## Traces

Your simulator will model a cache hierarchy based on traces of real programs.
Each line in the trace file contains the address of a memory access in hex as
well as where the access should be directed, either to the I$ (I) or D$ (D).


```
<Address> <I or D>

Sample Trace from tsman.bz2:
0x648 I
0x64c I
0x650 I
0x654 I
0x658 I
0x40868 D
0x65c I
0x660 I
0x664 I
0x668 I
```


## Academic Integrity
This assignment is to be done individually by every student. Please make sure you do not copy a single line of code from any source. Not from other students, not from the web, not from anywhere. We have very sophisticated tools to discover if you did. This is a graduate class and we have the very highest expectations for integrity. You should expect that if you do so, even in very small amounts, you will be caught, you will be asked to leave the program, and if an international student, required to leave the country. 

## Turning it in
We will be taking only your predictor.c and predictor.h files. You can add the entire repository, but you need to have a folder structure like the following at least:

```
├── 📂 src
|   ├── 📄 cache.c
|   ├── 📄 cache.h
```

You can, of course, submit the entire repository, but we will look for only these files, and all the remaining files used will be our own. We will run the following commands for grading: `make clean` followed by `make`
