CSE233 Operating Systems - Assignment 2


Installation

Prerequisites

- GCC (GNU Compiler Collection): Required to compile C programs
  bash
  sudo apt install gcc
  
- Make: For building with the provided Makefile
  ```bash
  sudo apt install make
  ```
- ldd: Pre-installed on most Linux systems (used for Exercise 6)

 Building the Project

1. Clone the repository:
   ```bash
   git clone <your-repository-url>
   cd <repository-name>
   ```

2. Compile all programs:
   ```bash
   make all
   ```

 Usage

Compile All Programs

```bash
make all
```

Run All Exercises

```bash
make run
```

This will execute all three exercises and display the dynamic libraries used by the simple program.

Run Individual Exercises

```bash
make run-ex1    # Exercise 1: Fork demonstration
make run-ex5    # Exercise 5: Linker demonstration
make run-ex6    # Exercise 6: Loader demonstration
```

View Compilation Stages

```bash
make stages
```

This demonstrates the separate compilation and linking stages.

Clean Build Files

```bash
make clean
```

View Help

```bash
make help
```

Exercises Explained

Exercise 1: Using fork() in C

File: `process_creation.c`

This program demonstrates the fork() system call, which creates a new process.

How it works:
1. The program calls `fork()` which creates a child process
2. Both parent and child processes continue execution after fork()
3. The return value of fork() differs:
   - Returns **0** to the child process
   - Returns **child's PID** to the parent process
   - Returns **-1** if fork fails

Expected Output:
```
This is the parent process. PID: 1234
This is the child process. PID: 1235
```

Key Concepts:
- Process creation and duplication
- Parent-child process relationships
- Using PIDs (Process IDs) to identify processes

Exercise 2: Background Processes
Start in background:
Bash
sleep 300 &
List background jobs:

Bash

jobs
Exercise 3: Stopping Processes
Find the Process ID (PID):

Bash

ps aux | grep sleep
(Look for the number in the second column, e.g., 1234)

Kill the process:

Bash

kill <PID>
(Replace <PID> with the number you found)

Verify it is gone:

Bash

ps aux | grep sleep
Exercise 4: Pause and Resume
Pause (Suspend):

Bash

kill -STOP <PID>
Resume (Continue):

Bash

kill -CONT <PID>


  
Exercise 5: Role of the Linker

Files:`file1.c` and `file2.c`

This exercise demonstrates how the linker combines multiple object files into a single executable.

file1.c contains the implementation of the `hello()` function:
```c
void hello() {
    printf("Hello from file1!\n");
}
```

file2.c contains the main program that calls `hello()`:
```c
void hello();  // Declaration
int main() {
    hello();   // Call
    return 0;
}
```

Compilation Process:
1. `file1.c` is compiled to `file1.o` (object file)
2. `file2.c` is compiled to `file2.o` (object file)
3. Linker combines both object files into `output_program` executable
4. Linker resolves the reference to `hello()` in file2.o by finding its implementation in file1.o

Expected Output:
```
Hello from file1!
```

Exercise 6: Role of the Loader

File: `simple_program.c`

This program demonstrates what happens when an executable is loaded into memory.

Using ldd:
```bash
ldd simple_program
```

Expected Output:

This is a simple program.

What the loader does:
1. Reads the executable from disk
2. Allocates memory for the program
3. Loads program code into RAM
4. Dynamically loads required shared libraries (like libc.so)
5. Sets up the execution environment
6. Transfers control to main()

Linker and Loader

The Linker

Definition: A program that combines object files into a single executable.

Key Responsibilities:
- Symbol Resolution: Connects function calls to their definitions across multiple files
- Relocation: Assigns final memory addresses to program segments
- Library Linking: Links with static or shared libraries
- Executable Creation: Produces the final executable file in proper format (ELF on Linux)

Example in this project:

gcc file1.c file2.c -o output_program

The linker resolves the call to `hello()` in file2.c by finding its implementation in file1.c.

The Loader

Definition: Part of the operating system that loads programs from disk into memory for execution.

Key Responsibilities:
- Memory Allocation: Allocates RAM for the program
- Loading: Copies program code and data from disk to RAM
- Dynamic Linking: Loads shared libraries at runtime
- Relocation: Adjusts addresses for actual load location
- Initialization: Sets up execution environment and transfers control to entry point

Example in this project:
When you run `./simple_program`, the loader loads the program and dynamically links it with libc.so (which contains printf()).


License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

 Author: Lab-5 Assignment
Course: CSE233 - Operating Systems  
Purpose: Educational demonstration of process management and compilation

