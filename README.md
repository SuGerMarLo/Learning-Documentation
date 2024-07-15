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

**This is a CPU simulator that outlines different steps of a given program, and how the processor would go about executing them.**

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
In this case, 00000000 (0) + 00000020 (32) = 00000020 (32)

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
The third command follows the same process until it reaches the instruction register.
we take the data in "x1" (marked by "rs1" in the instruction register) and add the currently value to it: 0 + 32 = 32

![image](https://github.com/user-attachments/assets/a482a16d-6952-4545-9573-354ea97ea90e)
![image](https://github.com/user-attachments/assets/61db60b5-56cf-452b-8970-a5dfadc32ce8)

Next, as per this specific command, instead of storing the new value into "x3", we instead use it as an address, plugging it back into the bus.
00000020 matches on the addresses, therefore it will take a data set from there, "48" (which is the value at the address pointer stored in "x1"), and store that into "x3"

![image](https://github.com/user-attachments/assets/35e5b08c-f105-4a6f-b231-49c31d6f4722)
![image](https://github.com/user-attachments/assets/3bf51907-3ee4-4a88-a4f1-66cc0a99e1c0)
![image](https://github.com/user-attachments/assets/bcc5e259-1d61-4810-ab29-97fe487201a2)

Program counter goes up again, and onto the next step.
Same process towards the instruction register...

![image](https://github.com/user-attachments/assets/0e90841a-51c5-4c4c-837c-f56baf5da46d)

First off, this instruction took the program counter value, 0000001c (12), and the current instruction's immediate value, 00000010 (16), and added them together (28)
Next, the program is checking if the 2 selected registers, in this case "x3" and "x0" (marked by "rs1" and "rs2"), are equal to each other.
They aren't, so the program returned "false".
The "beq" instruction compares "rs1" and "rs2", if they are equal, the program counter would have changed to the new value calculated in this instruction, skipping ahead to a further instruction.
Since it wasn't equal, that part is ignored and the program counter goes up by another 4, leading us to the next step.

![image](https://github.com/user-attachments/assets/6560c502-ed8a-4997-a44d-f0175f89634d)
![image](https://github.com/user-attachments/assets/6fd06c48-213d-4eba-9628-cd067a84acad)

Same process as usual...
We take the information stored in "x2" (the empty ASCII string) and the data stored in "x3" (48) and bring them both over to the bus.

![image](https://github.com/user-attachments/assets/9f2f74ec-7e54-4961-b091-02189ae8b5bc)
![image](https://github.com/user-attachments/assets/dca82e4b-193f-49c0-81da-5c4a9202cf02)
![image](https://github.com/user-attachments/assets/1645ce95-3850-4a03-a500-e97d7a89cffe)
![image](https://github.com/user-attachments/assets/c0cebad7-20a3-4470-851e-86a816978ec0)

The empty ASCII string and the 48 is then brought over to the TEXT I/O section to assign it's value.
Since this program is meant to write "Hello", the first letter should in theory be "H".
If we check an ASCII table, we can see that the ASCII character that matches the hexadecimal value of 48 is, in fact, an "H", meaning that we now have our first letter.

![image](https://github.com/user-attachments/assets/aa055ab0-ca82-45a6-9593-e09cf4dfa3e7)
![image](https://github.com/user-attachments/assets/82d46ea9-8ad5-4a54-92f9-0944e38b8fda)

The program counter goes up by 4, and onto the next instruction.
As seen before, the "addi" instruction signifies a simple addition, in this case, between "x1", 00000020 (32), and "imm" (1), giving a value of 33 which will replace 32 in "x1" (since "rd" is 1)

![image](https://github.com/user-attachments/assets/f98ec39e-0eee-4819-823a-e4e8546afdba)
![image](https://github.com/user-attachments/assets/6437a1ab-526e-43b2-9e29-4e3cf29ab167)
![image](https://github.com/user-attachments/assets/df766ca9-62b2-4746-9180-fc83b6cebbda)
![image](https://github.com/user-attachments/assets/ee542620-f73f-457b-bd91-1e93e840a3cd)
![image](https://github.com/user-attachments/assets/f4dff7f8-d5dc-42da-a5e6-dd186fed5346)

Program counter goes up again, and onto the next instruction...
This next instruction is essentially a "goto" function that substracts "imm" from the program counter.
00000018 (24) - fffffff0 = 00000008 (8)

![image](https://github.com/user-attachments/assets/2ffdf6f1-187b-40c1-a2d7-15fe8e73dec6)
![image](https://github.com/user-attachments/assets/87aa1e36-b3eb-430c-afce-cd4637d5e60f)
![image](https://github.com/user-attachments/assets/62762a04-e53e-4c6b-a1c4-88c079da9452)
![image](https://github.com/user-attachments/assets/5adff890-ceec-4d49-87fb-35f74afc5968)
![image](https://github.com/user-attachments/assets/b3a6225c-31fd-433b-b031-f00731e9468b)

The program counter then gets set to the calculated value (8), bringing us back to a previous instruction, but now with different stored values

![image](https://github.com/user-attachments/assets/fefe51b6-83ad-4b17-88ca-3f63af85602f)

These next 5 instructions will be repeated over and over again until the word "Hello" is created, looping back every time until a new letter gets added.

![image](https://github.com/user-attachments/assets/441acfda-2c75-447c-812e-e35bf748e56f)

As we previously saw, 48 was already taken, next comes 65 and so on until the word is completed.
The reason that the stored ASCII values are able to be found is because of the below addition instruction which we earlier saw adds "1" to value stored in "x1".
The value stored in "x1" is an address pointer, and every time that it's referenced, it will take the data set at that specific location in the computer's storage.
This means that adding 1 to the address pointer every time just means that the next time this pointer is referenced, it will take the data value in the next cell over, which is why 48 (H), 65 (e), 6c (l), 6c (l) and 6f (o) are all next to each other.

![image](https://github.com/user-attachments/assets/8c0e0081-6829-4f56-bf4c-489ec048bc1e)
![image](https://github.com/user-attachments/assets/205e06aa-7588-4739-9579-8e746f3fcb74)
![image](https://github.com/user-attachments/assets/132a02b3-5d16-4617-9d26-b8cd42815bb1)

The word "Hello" is finished, but the "addi" instruction will still end up running one more time.
The next cell in the list however is just 0.
This will be important once the program loops again...

![image](https://github.com/user-attachments/assets/14de6934-5e79-466d-b76a-cdba31f6e9e1)
![image](https://github.com/user-attachments/assets/331cbc6b-1570-4053-a476-659110d81cee)

Back at this step, the value taken into "x3" became 0 for the reason mentioned above.

![image](https://github.com/user-attachments/assets/35862dbe-a9b5-4e48-98bb-64f283cc723b)
![image](https://github.com/user-attachments/assets/1f040fd2-042a-41a7-9285-64a9853f307f)

This is where the "beq" instruction comes into play, comparing the values of "x0" and "x3".
Since this time, they are both equal, the addition done onto the program counter will take effect, making it skip all the way to 0000001c.

![image](https://github.com/user-attachments/assets/59fd9af1-6d5a-4aec-b850-09dab2053b9b)
![image](https://github.com/user-attachments/assets/43d33707-80ac-40c3-8f22-adbdbc65ee93)
![image](https://github.com/user-attachments/assets/085a6ce6-c658-40a5-be5d-1668d3f85ce9)
![image](https://github.com/user-attachments/assets/c8215117-9d39-4cb4-8d84-4f0a8d28f70b)
![image](https://github.com/user-attachments/assets/1cf2cecb-ccec-4000-a9a8-05aba7a8c996)

This instruction however... is just an infinite loop, meaning that the program will never exit this instruction since the desired outcome of writing "Hello" has already been accomplished.

![image](https://github.com/user-attachments/assets/f9f83d92-d214-4b04-9ee5-393eaf604b55)


## Feedback
Although I already know how to use GitHub Markdown long before this assignment thanks to being in the game development program
I was at least able to learn a decent amount about computer architecture, mainly about how Assembly works, something that's interested me a bit

## Reflection
I'm starting to understand just how troublesome understanding even the most basic of programs in Assembly actually is, and why it's called a "low level programming language"
