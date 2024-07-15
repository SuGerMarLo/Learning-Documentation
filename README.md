# Learning-Documentation

## Assembly Compiler
URL: https://godbolt.org/

**This website displays a program from a high level prgramming language you choose (default is C++) in assembly code.**

`
int square(int num) 
{
    return 9 * num;
}
`

When inputting the above code in the compiler (which is the defautl code provided but a "num" has been switched to a "9"), it gets converted to the below code in assembly

```
push    rbp
mov     rbp, rsp
mov     DWORD PTR [rbp-4], edi
mov     edx, DWORD PTR [rbp-4]
mov     eax, edx
sal     eax, 3
add     eax, edx
pop     rbp
ret
```

What I understood is the following
the program starts of by pushing the value of `rbp` (Register Base Pointer) into a stack
`DWORD PTR [rbp-4]` tells the program that the info is in 32 bits
`mov     DWORD PTR [rbp-4], edi` is telling the program to take the first argument (in this case `num`) into `[rbp-4]` (which stores the entirety of `num`, an integer, into 4 bytes `-4`)
Now in the function, it's loading the `num` value in `edx` which is another register that is 32 bits wide (the "e" stands for "extended"), then copying that value over to `eax` which itself is another register
`sal     eax, 3` is shifting the value in `eax` over by 3 bits, which multiplies the value by 8 (because bit positions a to the power of 2: 1, 2, 4, 8)
`add     eax, edx` adds the value of edx to `eax`, which is `edx * 8`
since `edx` is 1, `(edx * 8) + 1 = edx * 9`
we now have the `9 * num` function ready
`pop     rbp` removes `rbp` from the stacks and restores it to its default value
and finally, `ret` returns the value of `eax` which is `edx * 9`, also known as `9 * sum`, which is the function we wanted



## Visual Transistor-level Simulation of the 6502 CPU
URL: http://www.visual6502.org/

**This talks about, and shows a simulation of the MOS 6502 processor, one of the first mass produced CPUs**

The people running this project took detailed images of the processor's silicon die (what the circuit is made of) and its substrate (which is essentially the Core of the CPU)
Using the 2 images taken, they recreated a digital version of the processor using vector polygon models of each of the 20000 components (mostly transistors)
Based off of how the polygons connect, they were able to accurately recreate the entire processor model to the transistor
They also used different colors on their simulation to denote the different signals being sent through each transistor ("high" and "low" logic states as it's called)
The "high" and "low" logic states simply refer to the different exits a signal can leave through a transistor (there are 2 exits)
Using this simulation, there were able to run multiple programs that used to be able to run on the original MOS 6502 processor, including Atari games



## CPU Simulation
https://eseo-tech.github.io/emulsiV/

**<ins>** This is a CPU simulator that outlines different steps of a given program, and how the processor would go about executing them. **<\ins>**

![image](https://github.com/user-attachments/assets/8582a895-efac-405b-974a-459268e0d3e1)

The first step is a simple addition (addi); the "x1" after said instruction denotes which GPR the processed information will be stored in.

![image](https://github.com/user-attachments/assets/9b98b632-7d3b-4ae3-bd46-d14f344dcd4f)

The program counter, which is currently at 00000000, calls over the instruction at the 00000000 address.

![image](https://github.com/user-attachments/assets/4fe50718-79a9-4839-accd-3fa89ebc490b)
![image](https://github.com/user-attachments/assets/a5d01c5d-146e-4a70-969b-12f5e7c6037a)

The data in that address (which are 4 sets of 2 bit hexadecimal integers) gets called over to the bus, then moves over to the instruction register to be processed.
The instruction register determines that the process to be executed is to take the value at "x0" (which is why rs1 is 0), 00000000, and add 00000020 to that value, then store it into the "x1" register (which is why "rd" is 1).

![image](https://github.com/user-attachments/assets/0e25020a-049d-4c73-98f9-0f0581ee06c2)
![image](https://github.com/user-attachments/assets/7cbb4773-b203-4c7a-9a4e-e681d92caa76)
![image](https://github.com/user-attachments/assets/71438bdf-6d5b-43ef-be68-d46d76032ae6)

The value from "x0" then goes over to the "a" section of the ALU, and the value from the instruction register gets brought over to the "b" section.
One simple addition later, the answer is displayed in the "r" section.
In this case, 00000000 (0) + 00000020 (20) = 00000020 (20)

![image](https://github.com/user-attachments/assets/e9cac0cf-2a40-47d4-8d82-58215cbc7366)

The response then gets stored into the predetermined "x1" register for later use

![image](https://github.com/user-attachments/assets/c3149269-0b25-47dc-8184-6d0c3f65cdf2)

To conclude the first step, the program counter gets 4 added to it (from 00000000 to 00000004), which also happens to be the address of the next instruction.

![image](https://github.com/user-attachments/assets/3aebf556-8742-45b7-9c3d-693071e87c74)
![image](https://github.com/user-attachments/assets/c7fd2dbb-4694-495f-9971-b8db5b142cc0)

The next step is meant to use ASCII text to type something out.

![image](https://github.com/user-attachments/assets/7789c61e-86a6-4eb3-88f0-be8490a0ec07)

We follow the same process as the first instruction, referencing the address, taking the associated 2 bit sets and bringing them through the bus over to the instruction register.
This specific instruction is meant to use ASCII text (which is what c0000000 is referencing).
The ASCII value gets brought over to the ALU, where no calculations need to be done, meaning that the value can now be stored in "x2" (which is why rd in the instruction register is 2).

![image](https://github.com/user-attachments/assets/ac438b10-d2ad-46b4-8f5b-118f38a40310)
![image](https://github.com/user-attachments/assets/090db2d0-34aa-4365-b2c8-5ece5ac7b93b)

Again, the program counter gets 4 added to it, which is the address for the third command.
The third command follows the same process until it reaches the instruction register

![image](https://github.com/user-attachments/assets/a482a16d-6952-4545-9573-354ea97ea90e)
![image](https://github.com/user-attachments/assets/61db60b5-56cf-452b-8970-a5dfadc32ce8)



## Feedback
Although I already know how to use GitHub Markdown long before this assignment thanks to being in the game development program
I was at least able to learn a decent amount about computer architecture, mainly about how Assembly works, something that's interested me a bit

## Reflection
I'm starting to understand just how troublesome understanding even the most basic of programs in Assembly actually is, and why it's called a "low level programming language"
