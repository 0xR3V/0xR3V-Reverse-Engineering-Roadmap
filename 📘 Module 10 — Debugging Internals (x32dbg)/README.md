# 📘 Module 10 — Debugging Internals (x32dbg)

---

## 🔍 Overview

Debugging is the core of practical reverse engineering.  
In this module, you learn how to:

- Control program execution  
- Understand runtime behavior  
- Inspect registers & memory  
- Use breakpoints effectively  
- Trace instructions  
- Follow validation logic live  

x32dbg allows you to *freeze time*, move line by line, and watch the program think.

---

# 🧩 1) Software Breakpoints (INT 3)

A software breakpoint inserts the byte:

```asm
CC
When the CPU executes it → the debugger pauses.

✔ How to set:
text
Copy code
Right-click instruction → Breakpoint → Toggle  (or F2)
✔ Best use cases:
Checking CMP instructions

Stopping before validation logic

Inspecting register values

📸 Example Screenshot

🧩 2) Hardware Breakpoints (DR0–DR3)
Hardware breakpoints use CPU debug registers.
They do not modify the program code.

✔ Types:
On execution

On read

On write

On access

✔ Why they are powerful:
Bypass anti-debug checks

Detect who modifies a variable

Perfect for tracking buffers

📸 Example Screenshot

🧩 3) Memory Breakpoints (on Read/Write)
Used to stop program when a specific address changes.

✔ Best use cases:
Serial buffer tracking

Password modification

Locating XOR/add/sub transformations

✔ How to set:
text
Copy code
Right-click memory → Breakpoint → Memory, on write
📸 Example Screenshot

🧩 4) Stepping (F7 / F8 / Step Out)
🔹 F7 — Step Into
Enter the function being called.

🔹 F8 — Step Over
Execute CALL without entering the function.

🔹 Step Out
Exit current function and return to caller.

📸 Example Screenshot

🧩 5) CALL / RET Runtime Flow
CALL does:
asm
Copy code
push return_address
jmp function
RET does:
asm
Copy code
pop eip
This reveals:

Start of validation function

End of validation logic

Return values in EAX

📸 Example Screenshot

🧩 6) Instruction Tracing (Run Trace)
Run Trace records every executed instruction, including:

Register changes

Memory writes

Branch decisions

✔ What it helps with:
Understanding complex serial algorithms

Detecting hidden loops

Tracking obfuscated logic

✔ How to start:
text
Copy code
Debug → Run trace
📸 Example Screenshot

🧩 7) Inspecting Registers (EAX, ECX, ESP, EIP...)
Watch registers while stepping:

EAX → return values

ECX → loop counter

ESP / EBP → stack frame

ZF → jump decisions

EIP → next instruction

📸 Example Screenshot

🧩 8) Memory Dump Window
Displays:

ASCII buffer

Hex values

Serial transformation

Dynamic data changes

✔ Useful for:
Watching how serial is processed

Understanding XOR/add/sub encoding

Inspecting strings and stack data

📸 Example Screenshot

🧪 Exercises
✔ Exercise A — Software BP
Place a breakpoint on a CMP instruction and determine:

The value in EAX

State of the Zero Flag

If jump is taken

✔ Exercise B — Memory BP
Put memory breakpoint on serial buffer:

Enter a serial

Watch who writes to the buffer

View how validation happens

✔ Exercise C — Run Trace
Use trace to:

Identify where EAX changes

Reveal hidden loops

Find the final success/fail condition

📝 Summary
In this module, you learned:

Software/hardware breakpoints

Memory breakpoints

Step Into / Step Over

CALL/RET flow

Register inspection

Memory dump analysis

Full instruction tracing

This knowledge transforms you from static analyst → runtime debugger, ready for:

Tough CrackMes

Malware analysis

Anti-debug bypass

Unpacking schemes

