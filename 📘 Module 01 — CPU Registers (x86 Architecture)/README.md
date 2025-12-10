
Module 01 — CPU Registers (x86 Architecture)
🎯 Objectives
By the end of this module, you should be able to:

Understand all general-purpose registers in x86
Know how each register is used during program execution
Recognize registers in disassembly (IDA/x32dbg)
Understand which registers are caller-saved vs callee-saved
🧠 1. Overview of the x86 Register Set
The x86 CPU contains several classes of registers:

🔹 General-Purpose Registers (GPR)
Register	Name	Purpose
EAX	Accumulator	Arithmetic, return values from functions
EBX	Base	Pointer for memory addressing
ECX	Counter	Loop counters, string operations
EDX	Data	Multiplication, division, extended operations
These four registers are the main workhorses in almost every assembly function.

🔹 Pointer Registers
Register	Name	Purpose
EBP	Base Pointer	Fixed reference point for the stack frame
ESP	Stack Pointer	Points to the top of the stack (moves constantly)
EBP stays stable within a function.
ESP moves up/down as values are pushed and popped.

🔹 Index Registers (used for arrays, buffers, strings)
Register	Name	Purpose
ESI	Source Index	Memory source for string operations
EDI	Destination Index	Memory destination for string operations
Useful in loops, decrypt routines, memory copying, unpackers.

🔹 Instruction Pointer
Register	Name	Purpose
EIP	Instruction Pointer	Address of the next instruction to execute
You cannot modify EIP directly — it changes through:

CALL
RET
JMP
Exceptions
🧩 2. Caller-Saved vs Callee-Saved Registers
This is important for debugging and calling conventions.

Caller-Saved (volatile)
The caller must preserve these if needed:

EAX
ECX
EDX
These will often change after calling a function.

Callee-Saved (non-volatile)
The function itself must preserve and restore:

EBX
ESI
EDI
EBP
This is why you often see:

push ebx
push esi
push edi


at the beginning of a function.

🧪 3. Example: Function Prologue Using Registers
push ebp
mov  ebp, esp
sub  esp, 20h

push ebx
push esi
push edi


Meaning:

Save old EBP

Create new stack frame

Reserve local variables

Save callee-saved registers

⚙️ 4. Example Assembly Snippets
Move values between registers
mov eax, ebx
mov ecx, 5

Using registers for memory addressing
mov eax, [ebp+8]    ; access function argument
mov ecx, [esi]      ; read from array

Using ECX as loop counter
mov ecx, 10

loop_start:
  ; ... do something ...
  dec ecx
  jnz loop_start

📌 5. Quick Notes Summary

EAX almost always stores return values.

EBP is used as a stable reference inside stack frames.

ESP changes constantly — never rely on it for fixed offsets.

ESI/EDI are critical in unpacking, encryption, memory loops.

EIP tells you “where the program is going next”.

📚 6. Exercises

✔ Q1: Which register usually holds function return values?
✔ Q2: Why does EBP stay fixed while ESP moves?
✔ Q3: Write an example where ECX is used as a loop counter.
✔ Q4: Which registers must a function save before modifying?
✔ Q5: What instructions can modify EIP?

