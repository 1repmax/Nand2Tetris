# Machine Language

* Computer can be described constructively, by laying out its hardware platform and explaining how it is built
from low level chips.
* Computer can also be described abstractly, by specifying and demonstrating its machine language capabilities.
* Machine language is agreed-upon formalism, designed to code low-level programs as series of machine instructions.
* Using these instructions, the programmer can command the processor to perform arithmetic and logic operations,
fetch and store values from and to memory, move values from one register to another, test Boolean conditions etc.
* Machine language's design is direct execution in, and total control of a given hardware platform.
* Machine language is the interface point where abstract thoughts of the programmer and symbolic instructions
are turned into physical operations performed in silicon.
* Software systems are, at bottom, long series of elementary instructions, each specifying a very simple and
primitive operation on the underlying hardware.
* A machine language can be viewed as agreed-upon formalism, designed to manipulate a memory using a processor
and a set of registers.

## Memory
* Memory loosely refers to:
  * devices that store data
  * devices that store instructions in a computer
* From developers point of view all memories have the same structure:
  * continuous array of cells of some fixed width, these fixed width cells are also called words or locations
  * each memory cell or word has a unique address
* Hence, an individual word (representing either a data item or instruction) is specified by supplying its address
* We will refer to such unique words using the notation Memory[address], RAM[address] or M[address] for brevity.

## Processor
Processor or CPU (Central Processing Unit), is a device capable of performing a fixed set of elementary operations:
* arithmetic operations
* logic operations
* memory access operations
* control or branching operations
Operands of these operations are binary values that come from registers and selected memory locations. Likewise, the
results of the operations can be stored either in registers or in selected memory locations.

## Registers
* Memory access is a relatively slow operations, requiring long instruction formats (an address may require 32 or more bits).
* For this reason most processors are equipped with several registers, each capable of holding a single value.
* Registers are located in the processors immediate proximity and registers serve as high speed local memory,
allowing the processor to manipulate data and instructions quickly.

## Languages
* Machine code (binary) is a series of coded instructions. (1011 1000 0001 0101)
* To understand what the instruction means we have to know what each of the bit means.
* Binary is hard to read, thus assembly languages have been created. Assembly language is more human readable
version of the binary instructions. For example the binary 1011 1000 0001 0101 could translate into assembly
ADD R3,R1,R9
* A text processing program can parse these symbolic commands and translate each field into its equivalent binary
representation, and assemble the resulting codes into binary machine instructions.
* The symbolic notation is called assembly language or simply _assembly_.
* The program that translates from assembly to binary is called _assembler_.

## Commands
* **Arithmetic and Logic Operations** are some basic arithmetic operations like addition and subtraction as well as
Boolean operations like bit-wise negation, bit shifting and so forth. For example:
  * `ADD R2,R1,R3` // R2 <- R1 + R3, where R1,R2,R3 are registers
  * `ADD R2,R1,foo` // foo stands for the value of the memory location pointed at by the user-defined label foo
  * `AND R1,R1,R3` // R1 <- bit wise And of R1 and R2
* **Memory access** commands fall into two categories. First, as we have just seen, arithmetic and logical commands are
allowed to operate not only on registers, but also on selected memory locations. Second, all computers feature explicit
load and store commands, designed to move data between _registers_ and _memory_. These memory access commands may use
several types of addressing _modes_ - ways of specifying the address of the required memory word.
  * _Direct addressing_ is the most common way to address the memory by expressing a specific address or by using a
  symbol that refers to a specific address:  
  `LOAD R1,67` // loads contents of memory address 67 into the R1
  `LOAD R1,bar` //loads the contents of memory address that `bar` is pointing to into the R1
  * _Immediate addressing_ is used to load constants - namely, load values that appear in the instruction code. Instead
  of treating the numeric field that appears in the instruction as an address, we simply load the values of the field
  itself into the register:  
  `LOADI R1,67` // R1 <- 67
  * _Indirect addressing_ is the addressing mode where the address of the required memory location is not hardcoded
  into the instruction. Instead, the instruction specifies a memory location that holds the required address. This
  addressing mode is used to handle pointers.  
  For example, consider the high-level command `x = foo[j]`, where foo is an array variable and `x` and `j` are integer
  variables. When the array `foo` is declared and initialized in the high-level program, the compiler allocates a memory
  segment to hold the array data and makes the symbol `foo` refer to the base address of that segment.
  Now, when the compiler later encounters references to array cells like `foo[j]`, it translates them as follows:
    * First note that the `jth` array entry should be physically located in a memory location that is at displacement
    j from the arrays base address. Hence, the address corresponding to the expression `foo[j]` can be easily calculated
    by adding the value of `j` to the value of `foo`.
* **Flow of Control** - while programs normally execute in a linear fashion, one command after the other, they also
include occasional branches to locations other than the next command. Branching serves several purposes including
repetition (jump backward to the beginning of a loop), conditional execution (if statements), and subroutine calling (
jump to the first command of some other code segment). In order to support these programming constructs, every machine
language features the means to _jump_ to selected locations in the program, both conditionally and unconditionally.
In assembly languages, locations in the program can also be given symbolic names, using some syntax for specifying labels.
  * _Unconditional jump commands_ like JMP specify only the address of a target location: `JMP beginWhile`
  * _Conditional jump commands_ like JNG must also specify a Boolean condition: `JNG R1,endWhile`

* A-instructions or addressing instructions
* C-instructions or control instructions

### A-instruction
* Symbolic syntax:  
`@value`, where `value` is non-negative decimal constant or symbol referring to such constant
* Binary syntax:  
* `0value`, where 0 at the start indicates that it is an addressing instruction. It is sometimes called the operation code
or op-code.

### C-instruction
* Symbolic syntax:  
`dest = computation ; jump`
* Binary syntax:  
`1 1 1 a  c1 c2 c3 c4 c5 c6  d1 d2 d3  j1 j2 j3`, where:
  * 1 at the start indicates op-code which is control instruction in this context
  * next 2 bits are not used and by convention are set to 1
  * the next 7 bits are computation bits
  * next 3 bits are destination bits
  * last 3 bits define jump bits

* D register is used to store data values.
* A register acts both as data and address register. So based on the instruction context, the contents of A register
can be interpreted as data value, or an address in the RAM or instruction memory.
* Looks like A stores the binary value, which is the address of where M register is pointing. For example if A = 4, then
M points to the RAM cell with address 4. Then we can assign some input to the M using the following syntax `M = 6`
* The `jump` field in the C-instruction tells what should be done next. There are 2 possibilities:
  1. fetch the next instruction in the program (default mode)
  2. fetch and execute an instruction located somewhere else in the program
To jump we have to set A register to hold an address of the next instruction we want to jump to. Whether jump should
be performed depends on the 3 `j` bits of the jump field and on the ALU output value. For example step by step explanation
of this example:
```
@3    // Load 3 in the A(ddressing) register -> 0011
D=M   // Since M(emory) register now points to the M[3], we fetch that value and load it into D(ata) register
@5    // Load 5 in the A(ddressing) register -> 0101
D=D-A // Subtract the value that is currently in A register from the value that is currently in D register and load the result into the D register
@100  // Load the value of next instruction into the A register
D;JEQ // Take the value from D register and perform comparison with 0. If the result evaluates to true, we jump and execute the instruction that is currently loaded in A register. If the value is false, we proceed with the next instruction in the program.
@200  // Load the next instruction in the A register
0;JMP
```
### Symbols
Assembly commands can refer to memory locations (addresses) using either constants or symbols. Symbols are introduced
into assembly programs in the following three ways:
1. _Predefined symbols_: a special subset of RAM addresses can be referred to by any assembly program using the
predefined symbols:
   * _Virtual registers_: to simplify assembly programming, the symbols `R0` to `R15` are predefined to refer to RAM
   addresses 0 to 15 (M[0..15])
   * _Predefined pointers_: The symbols `SP`, `LCL`, `ARG`, `THIS` and `THAT` are predefined to refer to RAM addresses 0 to 4
   respectively. Note that each of these memory locations has two labels. For example M[2] can be referred either using
   `R2` or `ARG`.
   * _I/O pointers_: the symbols `SCREEN` and `KBD` are predefined to refer to RAM addresses 16384(0x4000) and
   24576(0x6000). These are the base addresses of the screen and keyboard memory maps. They are manipulated using
   binary calculations.
2. _Label symbols_: these are user-defined symbols, which server to label destinations of goto commands, are declared
by the pseudo command "(Xxx)". This directive defines the symbol Xxx to refer to the instruction memory location holding
the next command in the program. A label can be defined only once and be used anywhere in the assembly program, **even
before the line in which it is defined**.
3. _Variable symbols_: any user-defined symbol Xxx appearing in an assembly program that is not predefined and is not
defined elsewhere using the "(Xxx)" command is treated as a variable, and is assigned a unique memory address by the
assembler, starting at RAM address 16