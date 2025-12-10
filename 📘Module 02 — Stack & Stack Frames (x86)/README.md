🔍 Overview

The stack is one of the most important components in x86 reverse engineering. It stores:

Function arguments

Local variables

Return addresses

Saved registers

Understanding the stack is essential for analyzing functions, CALL/RET flow, and CrackMe validation routines.

🧠 What Is the Stack?

The stack is a LIFO (Last In, First Out) structure used for storing temporary data.

✔ Grows downwards in memory ✔ ESP → stack pointer (dynamic) ✔ EBP → base pointer (stable reference inside function)

🧩 How the Stack Works During Function Calls

When a function is called, the compiler creates a stack frame.

A typical function prologue: push ebp mov ebp, esp sub esp, 0x20

Meaning:

Save old EBP

Set new EBP

Reserve space for locals (0x20 bytes)

A typical function epilogue: mov esp, ebp pop ebp ret

Restores previous stack frame and returns to caller.

🧠 Relationship Between ESP and EBP ✔ EBP is stable

Used to access:

[ebp+8] → arg1 [ebp+0xC] → arg2

✔ ESP moves (dynamic)

Used during PUSH, POP, CALL, RET.

📌 Function Arguments Layout

Example for a function:

int sum(int a, int b);

Stack layout after CALL:

[ebp+8] = a [ebp+0xC] = b

📌 Local Variables Layout

If compiler reserves 0x10 bytes:

sub esp, 0x10

Locals are:

[ebp-4] [ebp-8] [ebp-C] [ebp-10]

Negative offsets = locals. Positive offsets = arguments.

🧠 CALL & RET Interaction with the Stack

When CALL executes:

CALL target

CPU does:

Push return address

Jump to target

When RET executes:

RET

CPU does:

Pop return address → EIP

📌 Visual Stack Diagram HIGH MEMORY
| arg2 | ← [ebp+0xC]
| arg1 | ← [ebp+8]
| return addr |
| old EBP | ← [ebp]
| local var1| ← [ebp-4]
| local var2| ← [ebp-8]
LOW MEMORY

🔍 Example in Assembly C Code: int check(int x, int y) { int z = x + y; return z; }

Assembly: check: push ebp mov ebp, esp sub esp, 4 ; reserve space for z

mov  eax, [ebp+8]  ; x
add  eax, [ebp+0xC] ; y
mov  [ebp-4], eax  ; z = x+y

mov  eax, [ebp-4]  ; return z
mov  esp, ebp
pop  ebp
ret
🔥 Stack in CrackMe Validation

In CrackMe programs, serial input is typically passed via:

push offset SerialInput call GetDlgItemTextA

Later:

cmp [ebp-4], eax jne wrong

Understanding the stack helps you follow:

where the input is stored

how the program compares it

where the validation logic branches

🧪 Exercises Exercise A

Explain what these instructions do:

push ebp mov ebp, esp sub esp, 0x30

Exercise B

Identify arguments and locals in:

mov eax, [ebp+8] mov ecx, [ebp+0xC] mov [ebp-4], eax

Exercise C

Draw the stack layout for a function with:

2 arguments

3 local variables

📝 Summary

Stack grows downward

ESP moves, EBP stays stable

Prologue/Epilogue create and destroy stack frames

[ebp+X] → arguments

[ebp-X] → locals

Understanding stack frames is essential for CALL/RET analysis and reverse engineering
