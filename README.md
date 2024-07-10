# Learning-Documentation

## Assembly Compiler
URL: https://godbolt.org/

**<ins>** This website displays a program from a high level prgramming language you choose (default is C++) in assembly code. **<\ins>**

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

**<ins>** This talks about, and shows a simulation of the MOS 6502 processor, one of the first mass produced CPUs **<\ins>**

The people running this project took detailed images of the processor's silicon die (what the circuit is made of) and its substrate (which is essentially the Core of the CPU)
Using the 2 images taken, they recreated a digital version of the processor using vector polygon models of each of the 20000 components (mostly transistors)
Based off of how the polygons connect, they were able to accurately recreate the entire processor model to the transistor
They also used different colors on their simulation to denote the different signals being sent through each transistor ("high" and "low" logic states as it's called)
The "high" and "low" logic states simply refer to the different exits a signal can leave through a transistor (there are 2 exits)
Using this simulation, there were able to run multiple programs that used to be able to run on the original MOS 6502 processor, including Atari games



## Feedback
Although I already know how to use GitHub Markdown long before this assignment thanks to being in the game development program
I was at least able to learn a decent amount about computer architecture, mainly about how Assembly works, something that's interested me a bit

## Reflection
I'm starting to understand just how troublesome understanding even the most basic of programs in Assembly actually is, and why it's called a "low level programming language"
