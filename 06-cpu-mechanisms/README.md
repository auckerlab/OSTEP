# CPU mechanisms⚙️

In order to virtualize the CPU, the OS needs to somehow share the physical CPU among many jobs running seemingly at the same time.

Basic idea: run one process for a litt wle while, then run another one, so forth.

*Challenges*:

* performance
* control

| OS | Program |
|--- | ---     |
|Create entry for process list | |
|Allocate memory for program |  |
|Load program into memory |  |
|Set up stack with argc/argv | |
|Clear registers | |
|Execute **call** main() | |
| | Run main() |
| | Execute **return** from main |
|Free memory of process | |
|Remove from process list | |

Figure 1: **Direct Execution Protocol (Without Limits)**

in **user mode**, code is restricted in what it can do, e.g., a process can't issue I/O requests; doing so would result in the processor raising an exception; the OS would then likely kill the process.

In contrast to user mode is **kernel mode**, which the OS (or kernel) runs in. Code that runs can do what it likes, including privileged operations such as issuing I/O requests and executing all types of restricted instructions.

Special instructions to **trap** into the kernel and **return-from-trap** back to user-mode programs are also provided, as well as instructions that allow the OS to tell the hardware where the **trap table** resides in memory.
