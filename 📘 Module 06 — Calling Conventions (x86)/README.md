## 🎯 Objectives
By the end of this module, you should be able to:
- Understand how different calling conventions pass arguments
- Know who is responsible for cleaning the stack (caller or callee)
- Identify calling conventions from assembly patterns
- Analyze API calls and C functions in IDA and x32dbg
- Recognize RET vs RET n behavior

---

# 🧠 1. What are Calling Conventions?

A calling convention defines:
1. **How arguments are passed to a function**
2. **Where the return value is stored**
3. **Who cleans the stack (caller or callee)**

Different languages & compilers use different conventions.

---

# 📌 2. Common x86 Calling Conventions

We focus on the three main ones:

---

# 🔹 2.1 `cdecl` (C Declaration)

Used by:
- C programs
- Most user-defined functions

### ✔ Arguments passed:
Pushed right-to-left on the stack

vbnet
Copy code

Example:
```asm
push arg3
push arg2
push arg1
call function
✔ Return value:
nginx
Copy code
EAX
✔ Stack cleanup:
cpp
Copy code
Caller cleans the stack
Means after call:

asm
Copy code
add esp, 12   ; remove 3 arguments (3 * 4 bytes)
✔ RET instruction:
nginx
Copy code
ret
Identification pattern in reverse engineering:
Many pushes before call

Followed by add esp, X

🔹 2.2 stdcall (Standard Call)
Used by:

WinAPI (MessageBoxA, CreateFileA, etc.)

✔ Arguments passed:
css
Copy code
Right-to-left on stack
✔ Return value:
nginx
Copy code
EAX
✔ Stack cleanup:
cpp
Copy code
Callee cleans stack
Meaning: caller does NOT clean the stack.

✔ RET instruction:
mathematica
Copy code
ret N
Example call:

asm
Copy code
push 0
push offset caption
push offset text
push 0
call MessageBoxA
Inside function:

asm
Copy code
ret 16       ; 4 args * 4 bytes = 16
Identification pattern:
No add esp, X after call

RET has an immediate value

🔹 2.3 fastcall
Used by some compilers for performance.

✔ Arguments passed:
cpp
Copy code
First two arguments → ECX, EDX
Remaining → stack
Example:

asm
Copy code
mov ecx, arg1
mov edx, arg2
push arg4
push arg3
call fast_func
✔ Stack cleanup:
java
Copy code
Callee cleans stack (varies)
✔ RET instruction:
python
Copy code
ret N    or    ret
Identification pattern:
ECX and EDX loaded with meaningful values before CALL

🧩 3. Comparing Calling Conventions
Convention	Args	Return	Stack Cleanup	RET
cdecl	stack	EAX	caller	ret
stdcall	stack	EAX	callee	ret N
fastcall	ECX/EDX + stack	EAX	callee	ret N or ret

🔍 4. How to Identify Calling Conventions in IDA / x32dbg
✔ cdecl
Look for:

asm
Copy code
add esp, X
after the call.

✔ stdcall
Look for:

asm
Copy code
ret N
inside function.

✔ fastcall
Look for:

ECX loaded

EDX loaded

Then CALL

Example:

asm
Copy code
mov ecx, [ebp+8]
mov edx, [ebp+0xC]
call function
🎯 5. Why This Matters in Reverse Engineering
Calling conventions help you:

Identify where arguments come from

Understand function prototypes

Reconstruct C code from assembly

Reverse engineer malware routines

Understand WinAPI behavior

In IDA, you will be able to rename parameters confidently:

Copy code
arg_0, arg_4, arg_C
and reconstruct logic exactly.

🔬 6. Example: Reversing a Function Call
Caller:

asm
Copy code
push 20h
push 10h
call sum
add esp, 8
Callee:

asm
Copy code
sum:
    mov eax, [ebp+8]    ; 10h
    add eax, [ebp+0xC]  ; +20h
    ret
Because caller cleans the stack → this is cdecl.

📌 7. Quick Notes Summary
EAX always holds return value

cdecl → caller cleans stack

stdcall → callee cleans stack (WinAPI)

fastcall → ECX/EDX for first args

RET N means callee cleanup

Checking stack cleanup reveals the calling convention

Understanding this improves your C reconstruction

🧪 8. Exercises
✔ Q1: What does RET 12 tell you about the calling convention?
✔ Q2: How do you identify cdecl in assembly?
✔ Q3: Which registers are used first in fastcall?
✔ Q4: Convert a WinAPI call into its calling convention.
✔ Q5: Why is calling convention important in reversing malware?

