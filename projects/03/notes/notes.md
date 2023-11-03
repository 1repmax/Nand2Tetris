# Sequential Logic
* Flip-flops:
  * DFF (data flip-flop) outputs the input value from the previous clock cycle
  * out(t) = in(t - 1)
  * this elementary behaviour forms the basis of all hardware devices that computers use to maintain state

* Registers:
  * used to store a value over time
  * out(t) = out(t - 1)
  * multiplexer is used to allow `loading` of new values:
    * if load = 0, we start storing new value
    * if load = 1, we take the value from previous clock cycle

* Memories:
  * RAM has 3 inputs:
    * data input
    * address input
    * load bit

* Counters:
  * Counter is a sequential chip whose state is an integer number that increments every time unit
  * Typical CPU includes a program counter whose output is interpreted as the address of the instruction that
    should be executed next in the current program.
* In sequential chips the output at time _t_ does not depend on itself, but rather on the output at time _t - 1_.
* The above property guards against uncontrolled _data races_ that would occur in combinatorial chips with 
feedback loops.

* _Clocked Data Flip-Flop_ moves one bit of information from time _t - 1_ to time _t_. Essentially it shifts the input signal
by one time unit or clock cycle.

* Single-bit register, which can also be called bit or binary cell, is designed to store a single bit of information
over the time. Registers are implemented combining multiplexer with the DFF chip. DFF chips expose input as interface,
but the chip itself internally is connected to the clock.

* Number of registers is referred to as memory's size
* Width of each register is referred to as memory's width
* _k_ or memory access bit count can be calculated from formula log2(n)
  * We need _address_ input of 3 bits to control access to a memory of size 8
  * We need _address_ input of 6 bits to control access to a memory of size 64
  * We need _address_ input of 9 bits to control access to a memory of size 512

* RAM8 gate gives us memory with 8 memory cells, where each cell is 16 bits wide.