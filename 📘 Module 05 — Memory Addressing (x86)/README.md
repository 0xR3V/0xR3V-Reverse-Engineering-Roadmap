
## 🎯 Objectives
By the end of this module, you should be able to:
- Understand how memory addressing works in x86 assembly
- Access variables using `[reg]` and `[reg+offset]`
- Read arrays and buffers using ESI/EDI/ECX
- Understand scaled indexing (`[reg + reg*scale + offset]`)
- Recognize pointer dereferencing patterns in IDA and x32dbg

---

# 🧠 1. Understanding Memory Addressing

In x86 assembly, you typically access memory like this:

mov eax, [address]
mov eax, [ebx]
mov eax, [ebp+8]
mov eax, [esi+ecx*4]

markdown
Copy code

These notations refer to:
- **Pointers**
- **Offsets**
- **Arrays**
- **Structures**
- **Function arguments**
- **Local variables**

---

# 🔹 2. Basic Addressing Modes

## 2.1 Register-Only
```asm
mov eax, ebx
Just copies register values (no memory access).

2.2 Direct Memory Addressing
asm
Copy code
mov eax, [0x00405060]
Loads the data stored at that absolute memory address.

Often seen in:

Global variables

.data section

.rdata constants

2.3 Register Indirect Addressing
asm
Copy code
mov eax, [ebx]
Meaning:

Treat EBX as a pointer

Load the DWORD stored at memory address EBX

Used heavily for:

Dynamic memory

Objects/structures

Linked lists

2.4 Base + Offset
asm
Copy code
mov eax, [ebp+8]    ; function argument
mov ecx, [ebp-4]    ; local variable
Common uses:

Access arguments ([ebp+8])

Access local variables ([ebp-4])

🔹 3. Scaled Indexing (Arrays)
Pattern:

asm
Copy code
mov eax, [base + index*scale]
Where:

base = usually ESI/EDI/EBX

index = ECX, EDX

scale = 1, 2, 4, or 8

Example: Accessing int array
Each int = 4 bytes.

asm
Copy code
mov eax, [esi + ecx*4]
Meaning:

ESI = start of array

ECX = index

EAX = array[index]

🔹 4. Base + Index + Offset (full addressing mode)
Most complex form:

asm
Copy code
mov eax, [ebx + ecx*4 + 0x10]
Breakdown:

EBX → base pointer

ECX*4 → select element

+0x10 → offset inside structure

This is how compilers access:

Arrays of structures

Class fields

Function tables

🌐 5. Using ESI & EDI (String/Buffer Operations)
Typical pattern in loops:

asm
Copy code
mov esi, input_buffer
mov edi, output_buffer
mov ecx, length

rep movsb   ; copy bytes from ESI to EDI
Or manual loop:

asm
Copy code
mov esi, array
mov ecx, length

loop_start:
    mov eax, [esi]
    ; process value
    add esi, 4        ; next element
    dec ecx
    jnz loop_start
🔎 6. Reading Strings (Character-by-Character)
Strings use byte addressing:

asm
Copy code
mov al, [esi]     ; read 1 byte
inc esi           ; move to next char
Used in:

Validation loops

Key comparisons

Malware unpackers

📦 7. Structures & Offsets
Example:

c
Copy code
struct User {
    int id;             // offset 0
    int score;          // offset 4
    char name[16];      // offset 8
};
Assembly access:

asm
Copy code
mov eax, [ebx]        ; id
mov ecx, [ebx+4]      ; score
mov edx, [ebx+8]      ; name[0]
📘 8. Example: Adding elements of an array
asm
Copy code
mov esi, array
mov ecx, length
xor eax, eax       ; sum

sum_loop:
    add eax, [esi]
    add esi, 4
    dec ecx
    jnz sum_loop
📌 9. Quick Notes Summary
[reg] → pointer dereference

[reg + offset] → accessing fields/locals/args

[reg + index*scale] → arrays

[base + index*scale + offset] → arrays of structures

ESI and EDI → heavily used in loops

Strings use byte-access (al instead of eax)

🧪 10. Exercises
✔ Q1: How would you access the 5th element of an int array?
✔ Q2: Write assembly that iterates over a buffer until a zero byte.
✔ Q3: Explain what [ebx + ecx*4] means.
✔ Q4: What is the difference between [esi] and esi?
✔ Q5: Given a structure, explain how offsets map to fields.


