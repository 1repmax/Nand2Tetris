# 1. Boolean Logic
## Table of Contents
- [Terminology](#terminology)
- [Transistor](#transistor)
- [NAND Gate](#nand-gate)

### Terminology:
* _Boolean_ - a binary variable that can have one of two possible values, 0 (false) or 1 (true). The 0 and 1 in computer
science context means _absence_ and _presence_ of electrical signal respectively.
* _Function_ - in Layman's terms function operates on some input to produce an output.
* _Boolean function_ - if we combine the two statements above, then _boolean function_ is a function that operates on
binary inputs and returns binary outputs.

Computers are based on representation and manipulation of binary values thus it is important to understand how Boolean
Algebra or Boolean arithmetic works and what we can achieve with it.  

### Transistor
On a physical level computers are built using small switches called _transistors_. Transistor consists of _two input_
pins and _one output_ pin as in the image below.
![Transistor](/ch1/img/transistor.png)
Transistor acts like an electron valve. The **base** pin is like a handle you might adjust to allow more or less
electrons to flow from **emitter** to **collector**.
This is a very brief and simplistic explanation on what is the goal of each pin:
| Pin No   |                    Goal                              |
|----------|------------------------------------------------------|
| 1 | Emits the current (output)                                  |
| 2 | Controls electric current flow from collector to the emitter|
| 3 | Receiver of the current (input)                             |

I think it is worth mentioning that a NAND gate itself can be built from two transistors.

### NAND Gate
The following images were generated using [Nandgame](https://nandgame.com/) which has also been inspired by the
Nand2Tetris course.  
To understand how NAND gate is built lets look at a concept called relay or mechanical switch. Relay is not the same
thing as transistor in physical world, but both of them deliver essentially the same switching functionality although
the inner workings of them are different. Thus in any place in the future where I mention relay you can think of a
transistor.

We are given two different kinds of _relays_:
* Relay (default on)  
![Relay default on](/ch1/img/relay_default_on.PNG)  
We can observe that the circuit is _closed by default_ and electrical current will flow through from input _in_ to the
* connected output. On the other hand, when we apply electrical current to the control pin _c_, electromagnetic field is
* generated which opens the closed circuit and the electron flow to the output is not possible.  
Behaviour as explained above can be seen in these two pictures:  
![Relay default on 1](/ch1/img/default_on_sample.png)  ![Relay default on 2](/ch1/img/default_on_sample_2.png)  

* Relay (default off)  
![Relay default off](/ch1/img/relay-default-off.PNG)  
We can observe that the circuit is _open by default_ and electrical current will not flow through from input _in_ to the
* connected output. When electrical current is applied to the control pin _c_, electromagnetic field is generated which
* closes the open circuit and the electrons flow to the output. As you have guessed, this relay is basically the
* opposite of the previous one.  
![Relay default off 1](/ch1/img/default_off_sample_1.png)  ![Relay default off 2](/ch1/img/default_off_sample_2.png)

Now that we have seen the 2 kinds of relays which have analogue transistors, lets take a look at how the NAND gate can
be built from them.  
First-off lets look at truth table of the NAND gate:
| a | b | out |
|:-:|:-:|:---:|
| 0 | 0 |  1  |
| 0 | 1 |  1  |
| 1 | 0 |  1  |
| 1 | 1 |  0  |

We can observe that NAND logic gate will have signal on output pin only when either both of the inputs are off or one of
them is off. This is the place that confused me the most. Essentially, the truth table tells us that in case when both
of the input pins have no electrical current applied to them, we will have a signal on the output pin. **The question
arises, from where does the electrical current comes from?**  
The answer to the question imposed above is pretty straightforward: NAND gate is built using two relays or transistors,
where one of the transistors input pins is always connected to the power supply. The power supply makes sure that
electrical current is always flowing into one of the transistors input pins.
Now that we have covered the fact from where the electrical current comes from in NAND gate, let's look at how we can
actually build such logic gate with the help of the two relays mentioned above.  
Given truth table is shown in the following image below:
| a | b | out |
|:-:|:-:|:---:|
| 0 | 0 |  1  |

![Nand 0 0](/ch1/img/nand_0_0.PNG)  
If we dissect the picture, we can see that NAND gate is built out of one relay that is by default off and one relay
that is by default on. The relay that is by default on is permanently attached to the power supply, and current is
flowing to the _output_ pin because the electrical chain is closed.  

We continue by showing the 2nd row from the NAND gate truth table.
| a | b | out |
|:-:|:-:|:---:|
| 0 | 1 |  1  |

![Nand 0 1](/ch1/img/nand_0_1.PNG)  
In this case we have electrical current applied to the _b_ pin of the first transistor. But since the transistor we
are using is by default off, there is no current flowing to the output of the first transistor.

We continue by showing the 3rd row from the NAND gate truth table.
| a | b | out |
|:-:|:-:|:---:|
| 1 | 0 |  1  |

![Nand 0 1](/ch1/img/nand_1_0.PNG)  
In this case we have electrical current applied to the _a_ pin of the first relay. It does close the electrical chain
and theoretically electrical current could flow through relay, but there is no electrical current applied to the _b_
pin and thus there is simply no current that could flow through this closed chain.  
Now lets look at the final row of the NAND gate truth table:
| a | b | out |
|:-:|:-:|:---:|
| 1 | 1 |  0  |

![Alt text](image-1.png)  
When both of inputs _a_ and _b_ have electrical current (binary 1) applied to them, the electrical chain of the first
relay is closed and electrical current flows out of the first relays _output_ pin. Since the output of the first relay
is connected to the _c_ pin of the second relay, the second relay changes from closed chain to the open chain and
electrical current is no longer able to flow from the power supply to the output pin.  

These 4 pictures clearly demonstrate NAND gate does not generate binary 1 or electrical current out of thin air.
The NAND gate is always connected to the power supply unit with one of its input pins.  

A reader might have noticed that the truth table of NAND gate gives us 2 inputs _a_ and _b_, but we can clearly see from
the last 4 pictures that we have 3 pins where one of them is connected to the power supply. This idea introduces us to
the concept of _interface_. We as a users are able to interact only with pins that are labeled as _a_ and _b_.
The pin of the second transistor will always be connected to the power supply unit, thus it is not exposed to us as
something that we can interact with. Essentially, the NAND gate provides us with _interface_ that consists of pin _a_
and pin _b_ and we are able to manipulate only the binary signal on these pins _a_ and pin _b_ to achieve the necessary
output signal out of our _logic gate_.  

Another question of mine I had when learning these concepts was the name _logic gate_ itself. They are called _gates_
because they control the flow of the binary signal, same as regular gate controls the flow of lets say cars for example.
The _logic_ in this context means decision making. We are trying to get our logical '1' or '0', so essentially the gate
controls the flow of logic, if one might say so.