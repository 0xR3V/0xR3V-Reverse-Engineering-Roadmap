🔍 Overview

Debugging is the core of practical reverse engineering.
In this module you will learn how to:

Use breakpoints (software / hardware / memory)

Control execution flow (F7 / F8 / Step Out)

Inspect registers during execution

Track memory changes in real-time

Follow CALL → RET logic

Use Trace to reveal hidden behavior

Analyze validation functions in CrackMes

x32dbg allows you to “freeze time” and watch how a program thinks.

🧩 1) Software Breakpoints (INT 3)

Software breakpoints insert the byte:

CC


When executed → debugger pauses instantly.

✔ How to set:
Right-click instruction → Breakpoint → Toggle (or press F2)

📸 Screenshot
![Software Breakpoint](./images/software_bp.png)


🧩 2) Hardware Breakpoints (DR0–DR3)

Hardware breakpoints use CPU debug registers.
They do NOT modify program code → harder to detect.

✔ Types:

On execution

On read

On write

On access

✔ Why they matter:

Bypass anti-debug tricks

Perfect for serial/password tracking

Ideal for catching “who modifies this memory?”

📸 Screenshot
![Hardware Breakpoint](./images/hardware_bp.png)


🧩 3) Memory Breakpoints (on Read / Write)

Stops execution when a specific memory address changes.

✔ Best use cases:

Tracking serial buffers

Watching XOR/add/sub transformations

Detecting corruption or hidden writes

✔ How to set:
Right-click memory → Breakpoint → Memory, on write

📸 Screenshot
![Memory Breakpoint](./images/memory_bp.png)


🧩 4) Stepping (F7 / F8 / Step Out)
🔹 F7 — Step Into

Enter inside the function being CALLed.

🔹 F8 — Step Over

Execute CALL but do not enter it.

🔹 Step Out

Return to caller instantly.

📸 Screenshot
![Stepping](./images/stepping.png)


🧩 5) CALL / RET Runtime Flow
CALL does:
push return_address
jmp function

RET does:
pop eip

✔ Useful for:

Finding validation function start

Tracing return values

Watching EAX before final decision

📸 Screenshot
![CALL RET](./images/call_ret.png)


🧩 6) Instruction Tracing (Run Trace)

Trace records every instruction executed, including:

Register changes

Memory modifications

Jumps taken

Execution path through functions

✔ Why Trace is powerful:

Reveals hidden algorithms

Shows password transformation

Uncovers obfuscation tricks

Helps understand malware behavior

✔ How to start:
Debug → Run trace

📸 Screenshot
![Instruction Trace](./images/trace.png)


🧩 7) Inspecting Registers (EAX, ECX, EIP, ESP...)

Registers change on every instruction.

✔ Most important:

EAX → return value of functions

ECX → loop counter

ESP / EBP → stack frame

ZF → jump decision accuracy

EIP → next instruction

📸 Screenshot
![Registers](./images/registers.png)


🧩 8) Memory Dump Window

Shows:

ASCII buffer

HEX bytes

Stack variables

Dynamic changes in input/serial

✔ Best use cases:

Watching input transformation

Understanding validation logic

Monitoring stack variables

📸 Screenshot
![Memory Dump](./images/memory_dump.png)


🧪 Exercises
✔ Exercise A — Software BP

Place breakpoint on CMP instruction and observe:

EAX value

ZF flag

Jump taken or not

✔ Exercise B — Memory BP

Set memory breakpoint on serial buffer:

Enter serial

Watch how buffer changes

Find validation routine

✔ Exercise C — Run Trace

Use trace to:

Find where EAX changes

Follow full validation path

Identify success/fail block

📝 Summary

In this module you learned:

Software / hardware / memory breakpoints

Stepping (F7 / F8 / Step Out)

CALL → RET flow

Trace analysis

Register inspection

Memory dump usage

This skillset transforms you into a runtime reverse engineer, ready for:

CrackMes

Malware analysis

Packed executables

Anti-debug bypass challenges
