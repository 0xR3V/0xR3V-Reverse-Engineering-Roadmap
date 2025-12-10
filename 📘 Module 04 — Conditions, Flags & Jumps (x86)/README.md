# Module 04 — Conditions, Flags & Jumps (x86)

## 🎯 Objectives
By the end of this module, you should be able to:
- Understand CPU flags and what sets them
- Use CMP and TEST instructions
- Read conditional jumps (JE, JNE, JG, JL…)
- Follow branches in IDA Graph View
- Predict control flow based on flags

---

# 🧠 1. CPU Flags (EFLAGS Register)

Flags are single-bit values that describe the result of an operation.

### The main flags used in reversing:

| Flag | Meaning | Triggered When |
|------|----------|----------------|
| **ZF** | Zero Flag | Result = 0 |
| **CF** | Carry Flag | Unsigned overflow / borrow |
| **SF** | Sign Flag | Result is negative |
| **OF** | Overflow Flag | Signed overflow |

You don’t set flags manually — CPU instructions modify them.

---

# 🔍 2. CMP Instruction

`cmp a, b` performs:
a - b

markdown
Copy code
But **does NOT store the result**.  
It only updates the flags.

### Example:
```asm
cmp eax, 10
Flags affected:

ZF = 1 if EAX == 10

ZF = 0 if EAX != 10

CF/SF/OF depend on signed/unsigned result

🔍 3. TEST Instruction (logical AND)
test a, b performs:

css
Copy code
a & b
Also updates flags.

Most common usage:

asm
Copy code
test eax, eax
Meaning:

Check if EAX == 0

Sets ZF = 1 if zero

🧩 4. Conditional Jumps (Branching)
Conditional jumps depend on ZF, CF, SF, OF.

▪ JZ / JE
Jump if Zero / Jump if Equal
ZF = 1

▪ JNZ / JNE
Jump if Not Zero / Not Equal
ZF = 0

▪ JG / JNLE
Jump if Greater (signed)

▪ JL / JNGE
Jump if Less (signed)

▪ JA / JNBE
Jump if Above (unsigned)

▪ JB / JNAE
Jump if Below (unsigned)

📈 5. Understanding Control Flow (Graph View)
IDA Graph View shows branches clearly.

Example:

asm
Copy code
cmp eax, 5
je correct
Graph view becomes:

csharp
Copy code
     [compare eax,5]
       /         \
   equal       not equal
   (JE)          (JNE)
Straight arrow → normal flow
Side arrow → jump path

🔁 6. Simple Validation Example
asm
Copy code
cmp eax, 1234h
jne fail

mov eax, 1
jmp end

fail:
xor eax, eax

end:
ret
Meaning:

If input != 0x1234 → go to fail

If correct → eax = 1

If incorrect → eax = 0

Classic CrackMe behavior.

🧪 7. TEST + Jumps Example
asm
Copy code
test eax, eax
jz empty
Meaning:

If eax == 0 → jump to empty

If eax != 0 → continue

Used often to check pointers, lengths, handles, etc.

🛠 8. Branching in x32dbg
How to step through branches:
F7 → Step Into

F8 → Step Over

Watch the ZF, CF, SF, OF flags in the CPU window

Follow where EIP goes based on the jump condition

📌 9. Quick Notes Summary
CMP = subtraction for flags

TEST = logical AND for flags

JZ/JE → if equal

JNZ/JNE → if not equal

JG/JL → signed comparisons

JA/JB → unsigned comparisons

Branching creates two execution paths

Graph View helps identify success/fail blocks easily

🎯 10. Exercises
✔ Q1: What does JZ do after test eax, eax?
✔ Q2: Write an assembly snippet that checks if a value is > 100.
✔ Q3: What is the difference between JL and JB?
✔ Q4: Explain how IDA Graph View shows conditional branches.
✔ Q5: Why does CMP not store the result of subtraction?
