# Bomb Lab
The Bomb Lab teaches students principles of
machine-level programs, as well as general debugger and reverse
engineering skills.

A "binary bomb" is a Linux executable C program that consists of six
"phases." Each phase expects the student to enter a particular string
on stdin.  If the student enters the expected string, then that phase
is "defused."  Otherwise the bomb "explodes" by printing "BOOM!!!".
The goal for the students is to defuse as many phases as possible.

## Setup

### Get Your Own Bomb
```bash
curl -o bomb.tar https://csapp.cs.cmu.edu/3e/bomb.tar
tar -xvf bomb.tar
```

### Defuse the Bomb
#### Install GDB
```bash
sudo apt-get install gdb
```

#### Dump the Bomb
```bash
# Generate the assembly code of the bomb's symbol table
objdump -t bomb > bomb_tb.asm

# Generate the assembly code of the bomb's code
objdump -d bomb > bomb.asm

# If you want to visualize the bomb's code with jumps, you can use the following command
objdump -d --visualize-jumps bomb > bomb.asm
```

#### Examine the Bomb
```bash
cd labs/bomb/src
gdb bomb
```

## Phases
- [Phase 1](./phases/phase_1/README.md)

## Reference
- [Bomb Lab README](https://csapp.cs.cmu.edu/3e/README-bomblab)
- [Bomb Lab Instructions](https://csapp.cs.cmu.edu/3e/bomblab.pdf)
- [Bomb Lab Source Code](https://csapp.cs.cmu.edu/3e/bomb.tar)
- [x86-64 Summary of GDB Commands](https://csapp.cs.cmu.edu/2e/docs/gdbnotes-x86-64.pdf)
- [x86-64 Assembly Reference Sheet](https://web.stanford.edu/class/cs107/resources/x86-64-reference.pdf)