# 0xR3V – Reverse Engineering Roadmap

This repository documents my complete journey into **Reverse Engineering** and **Malware Analysis**.

I am building this roadmap as:
- A structured learning path for myself  
- A public portfolio for future **RE / Malware Analyst** job applications  
- A reference for others who want to follow a similar path

---

## 🎯 Long-Term Goals

- Solve **95% of challenges** on [crackmes.one](https://crackmes.one)
- Become job-ready as a **Reverse Engineer / Malware Analyst**
- Build a strong portfolio of:
  - CrackMe write-ups
  - Malware analysis reports
  - Custom tools & scripts
  - RE notes & cheat sheets

---

## 🧩 Roadmap Structure (Modules)

Each topic is organized as a separate **Module**, with its own `README.md`, examples, and notes.

> The word “Module” is used instead of “Day” because some topics take more than one day of study.

Planned modules:

- `Module01_CPU_Registers` – General-purpose registers, EIP, flags  
- `Module02_Stack_and_Frames` – Prologue/Epilogue, locals, args  
- `Module03_CALL_RET_and_Flow` – Call stack, return values, control flow  
- `Module04_Conditions_and_Jumps` – CMP/TEST, flags, conditional branches  
- `Module05_Memory_Addressing` – [reg], [reg+offset], arrays, strings  
- `Module06_Calling_Conventions` – cdecl, stdcall, fastcall  
- `Module07_ASCII_and_Simple_Logic` – Input validation, loops, basic crackmes  
- `Module08_PE_Format_Basics` – PE headers, sections, RVA vs VA  
- `Module09_IDA_EntryPoint_Analysis` – EP, graph view, validation flow  
- `Module10_ImportTable_and_WinAPI` – IAT, WinAPI, behavior from imports  
- `Module11_Debugging_Internals` – x32dbg/x64dbg, breakpoints, tracing  
- `Module12_AntiDebug_Techniques` – IsDebuggerPresent, PEB checks, timing  
- `Module13_Packing_and_Unpacking` – UPX, custom stubs, OEP recovery  
- `Module14_Malware_Analysis_101` – Static & dynamic analysis, indicators  
- (more advanced modules will be added later)

---

## 📂 Repository Layout

Planned structure:

```text
0xR3V-Reverse-Engineering-Roadmap/
│
├── Module01_CPU_Registers/
│   └── README.md
├── Module02_Stack_and_Frames/
│   └── README.md
├── Module03_CALL_RET_and_Flow/
│   └── README.md
├── Module04_Conditions_and_Jumps/
│   └── README.md
├── Module05_Memory_Addressing/
│   └── README.md
├── Module06_Calling_Conventions/
│   └── README.md
├── Module07_ASCII_and_Simple_Logic/
│   └── README.md
├── Module08_PE_Format_Basics/
│   └── README.md
├── Module09_IDA_EntryPoint_Analysis/
│   └── README.md
├── Module10_ImportTable_and_WinAPI/
│   └── README.md
└── ...
Each module contains:

A detailed explanation of the topic

Assembly examples

Tool usage steps (IDA, x32dbg, CFF Explorer, etc.)

Exercises and notes

🛠 Tools Used
Disassemblers: IDA Free / IDA Pro, Ghidra (later)

Debuggers: x32dbg / x64dbg

PE Tools: CFF Explorer, PE-bear, Detect It Easy (DIE)

System Tools: Process Explorer, Process Monitor

Network (for malware): Wireshark, Fiddler (later)

✅ Current Status
✅ Modules 01–07: x86 fundamentals (registers, stack, calls, jumps, memory, calling conventions, ASCII logic) – in progress from my previous 7-days notes

✅ Module 08: PE Format Basics – notes & Word document completed

🔄 Moving content from my old repo into this structured roadmap

🔜 Next: Import Table / IAT and WinAPI analysis

👤 About 0xR3V
I am a self-taught reverse engineer & malware analyst in training.
This roadmap is both my personal study journal and a public technical portfolio.

If you want to follow along or reuse any notes, feel free – but do not use any knowledge here for illegal activities.

Educational & research use only.
