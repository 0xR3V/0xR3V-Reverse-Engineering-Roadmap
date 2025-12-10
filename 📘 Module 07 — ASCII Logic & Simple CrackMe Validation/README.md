# 🎯 Objectives
By the end of this module, you should be able to:
- Understand ASCII values and character ranges
- Validate user input using CMP and TEST
- Recognize common CrackMe validation patterns
- Implement loops that process characters one-by-one
- Reverse simple serial-check routines in IDA/x32dbg

---

# 🧠 1. ASCII Basics (Important for RE)

ASCII assigns numeric codes to characters:

| Character | ASCII (hex) | ASCII (dec) |
|-----------|-------------|--------------|
| '0' | 0x30 | 48 |
| '9' | 0x39 | 57 |
| 'A' | 0x41 | 65 |
| 'Z' | 0x5A | 90 |
| 'a' | 0x61 | 97 |
| 'z' | 0x7A | 122 |

You will *always* need these in CrackMe challenges.

---

# 🔍 2. Checking Character Ranges

### 2.1 Check if a character is a digit (0–9)

```asm
cmp al, '0'
jl  fail
cmp al, '9'
jg  fail
Meaning:

If AL < '0' → invalid

If AL > '9' → invalid

2.2 Check if uppercase letter (A–Z)
asm
Copy code
cmp al, 'A'
jl  fail
cmp al, 'Z'
jg  fail
2.3 Check if lowercase letter (a–z)
asm
Copy code
cmp al, 'a'
jl  fail
cmp al, 'z'
jg  fail
🏗️ 3. Common Validation Patterns in CrackMes
Most beginner CrackMes include:

✔ Checking length
✔ Validating each character
✔ Summing ASCII values
✔ Checking XORs or simple shifts
✔ Comparing against a constant
Example (classic):

asm
Copy code
mov al, [esi]    ; get char
cmp al, 'A'
jl  bad
cmp al, 'Z'
jg  bad
🔁 4. Loops Over Input (Very Common)
Example: Loop until null byte
asm
Copy code
mov esi, user_input

loop_start:
    mov al, [esi]     ; read char
    test al, al       ; is it 0?
    jz done
    ; process char...
    inc esi
    jmp loop_start

done:
Uses:

strings

password checks

key verification

🧮 5. Simple Math-Based Serial Checks
Example: Sum of ASCII characters must equal constant
asm
Copy code
xor eax, eax          ; eax = sum
mov esi, user_input

sum_loop:
    mov bl, [esi]
    test bl, bl
    jz  compare
    add eax, ebx
    inc esi
    jmp sum_loop

compare:
    cmp eax, 0x2A5
    jne wrong
    jmp correct
🔐 6. XOR-Based Validation (Typical CrackMe)
Very common pattern:

asm
Copy code
mov al, [esi]
xor al, 0x12
cmp al, [expected + ecx]
jne fail
XOR is used because:

It’s reversible

Fast

Obfuscates the expected value

📈 7. Recognizing Validation Functions in IDA
Look for:

✔ Character checks
✔ Loops with counters
✔ Access to input buffer
✔ Final CMP/JNZ
✔ Graph View with success and fail blocks
✔ Return in EAX (1 = correct, 0 = wrong)

Common prologue:

asm
Copy code
push ebp
mov  ebp, esp
Common end:

asm
Copy code
xor eax, eax     ; wrong
; OR
mov eax, 1       ; correct
ret
🧪 8. Realistic Example (Minimal CrackMe)
asm
Copy code
validate:
    push ebp
    mov  ebp, esp

    mov esi, [ebp+8]     ; pointer to input
    mov ecx, 5           ; length must be 5

loop_chars:
    mov al, [esi]
    test al, al
    jz  fail             ; too short?
    cmp al, 'A'
    jl  fail
    cmp al, 'Z'
    jg  fail

    inc esi
    dec ecx
    jnz loop_chars

    mov eax, 1
    jmp end

fail:
    xor eax, eax

end:
    mov esp, ebp
    pop ebp
    ret
Meaning:

Input must be 5 uppercase letters

Otherwise invalid

📌 9. Quick Notes Summary
ASCII values are essential in RE

Use CMP/Test to validate characters

Loops over strings use ESI+ECX/EDI

Validation functions usually return in EAX

IDA Graph View makes spotting success/fail easy

Simple crackmes = range checks + sums + XOR + CMP

Character-based logic appears in 95% of beginner challenges

🎯 10. Exercises
✔ Q1: Write a condition that checks if a character is between '0' and 'F'.
✔ Q2: Show how to loop over 10 characters using ESI and ECX.
✔ Q3: Implement a check: input[0] XOR 0x55 must equal 'A'.
✔ Q4: How can you identify the validation function in IDA?
✔ Q5: Why is TEST AL, AL used instead of CMP AL, 0?


