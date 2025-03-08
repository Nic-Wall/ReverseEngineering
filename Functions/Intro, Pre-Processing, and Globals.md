# Intro
## `nm`
`nm` contains information about symbols (functions, variables, etc.) from object files, executable files, or object-file library. The default [command](https://linux.die.net/man/1/nm) displays three columns containing...
1. Symbol Value: The numerical value based on the base (radix) of the number system. Position in a numeral system (one can see \_\_data\_start and data\_start share the same symbol value)
2. Symbol Type: A single letter indicating the symbol's type
	1. T: Text: Function definitions
	2. D: Data: Initialized global variables
	3. B: BSS: Uninitialized global variables
	4. U: Undefined: Symbol referenced but not defined in the binary (external library functions)
	5. R: Read-Only Data: `const` variables, string literals, etc.
	6. W: Weak Symbol: Specially annotated symbol during linking of ELF object files (overridden by strong symbols of the same name)
	7. N: Debugging Symbol: Only present if compiled with a debugging flag
	8. ?: Unknown: Unrecognized or stripped symbol
3. Symbol Name: The name of the function, variable, or section
One can also use the `-A` option to show a fourth column (preceding the Symbol Value column) that indicates what file the symbol associates with.
```
$ nm ./processID

000000000000038c r __abi_tag
0000000000004010 B __bss_start
00000000000013ce T compare
00000000000013f5 T compare_two
0000000000004010 b completed.0
                 w __cxa_finalize@GLIBC_2.2.5
0000000000004000 D __data_start
0000000000004000 W data_start
0000000000001130 t deregister_tm_clones
00000000000011a0 t __do_global_dtors_aux
0000000000003d98 d __do_global_dtors_aux_fini_array_entry
0000000000004008 D __dso_handle
0000000000003da0 d _DYNAMIC
0000000000004010 D _edata
0000000000004018 B _end
00000000000014b4 T _fini
0000000000001327 T f_mess
00000000000011e0 t frame_dummy
0000000000003d90 d __frame_dummy_init_array_entry
0000000000002280 r __FRAME_END__
                 U getpid@GLIBC_2.2.5
0000000000003f90 d _GLOBAL_OFFSET_TABLE_
                 w __gmon_start__
00000000000020b0 r __GNU_EH_FRAME_HDR
0000000000001000 T _init
0000000000002000 R _IO_stdin_used
                 U __isoc99_scanf@GLIBC_2.7
                 w _ITM_deregisterTMCloneTable
                 w _ITM_registerTMCloneTable
                 U __libc_start_main@GLIBC_2.34
00000000000011e9 T main
0000000000001478 T print_asts
                 U printf@GLIBC_2.2.5
                 U putchar@GLIBC_2.2.5
                 U puts@GLIBC_2.2.5
0000000000001160 t register_tm_clones
0000000000001260 T s_mess
                 U __stack_chk_fail@GLIBC_2.4
0000000000001100 T _start
0000000000004010 D __TMC_END__
0000000000004014 B user_input
0000000000001404 T w_mess
```
Immediately eyes are drawn to those unusually named or unfamiliar symbols, like...
- compare
- compare_two
- f_mess
- print_asts
- s_mess
- user_input
- w_mess
It's relatively safe to assume (since these have the T symbol type) they are custom made functions. user_input, on the other hand, has the B symbol type, indicating it's a global variable. Some other notables include...
- main: The beginning function of the script
- getpid: Undefined, but definitely a function to... get the Process ID of the script
- printf: Function to print out a string (with custom formatting)
- putchar: Function to print out a character
- puts: Function to output a string to the standard output
The rest are functions or global variables normally found in compiled C/ C++ scripts, like...
- \_init: Initialization tasks that need to occur before any other code is executed; setting up data structures, initializing global variables, etc.
- \_\_data\_start: defined by linker. Represents the starting address of the initialized data section in memory (RAM). Holds global and static variables that have been assigned initial values
- frame\_dummy: setup arguments for \_\_register\_frame\_info for exception handling
- \_end: First address past the end of the uninitialized data segment (BSS segment)
- \_start: Entry point for a C program, preceding the `main` function. Used to setup the execution environment before calling the `main` function. Also handles program termination, including calling `exit` to cleanup the program
Those prefixed with a single or double underscore are reserved functions/ types used by the compiler and standard library. Authors of scripts are NOT allowed to prepend their global functions or variables with \_ as it may conflict with one of these functions. Similarly, a user may NOT prepend a double underscore or underscore followed by capital letter in any variable, global or otherwise. This makes tracking down custom functions much easier (although I'm sure there are tricks involved I haven't learned yet).
## `file`
The file processID can be analyzed simply with the `file` [command](https://man7.org/linux/man-pages/man1/file.1.html), like so...
```
$file processID

processID: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=a0c5e73bb72b762392a833152a69ed3e067f1bbb, for GNU/Linux 3.2.0, not stripped
```
This shows...
- The name of the file/ directory: `processID`
- Format: `ELF` (Executable and Linkable Format)
- Bit mode: `64-bit`
- Byte order: `LSB` (Least significant byte) (this is important latter, especially in [[s_mess()]] and [[f_mess()]])
- Machine code to memory address allocation: `PIE` (Position Independent Executable), allows for the executable to be run at any memory address, not required to be loaded in specific memory locations
- CPU Architecture: `x86_64` (or ARM, RISC-V, etc.)
- ABI (Application Binary Interface): `version 1 (SYSV)`, System V (the original UNIX standard for ELF binaries). The init system, starts and stop processes (probably more likely to see systemd on modern systems)
- Linking: `Dynamically linked`, shows the executable relies on shared libraries rather than being self-contained. This means the binary can be run only on systems with the same libraries (I THINK). That would mean "statically linked" binaries can run even without the libraries present on the host device
- Interpreter: `interpreter /lib64/ld-linux-x86-64.so.2`, Specifies the dynamic linker/ loader that runs before the program executes, resolving shared library dependencies
- Checksum: `BuildID \[sha1] = a0c5...1bbb`, unique identifier of the binary generated on compilation. Used to verify processID is who it says it is and not an imposter masquerading with the same filename
- Minimum required Linux Kernel Version: `for GNU/Linux 3.2.0`, minimum Linux kernel version required to run this binary
- Stripping: `not stripped`, indicates whether or not the binary contains debugging symbols (function names, variable names, etc.). This one apparently contains debugging information because it is not stripped (I'd like to see how it change if it is stripped (compiled with `gcc -g`))
Analyzing this one could deduce; this program is meant to run on Linux devices, it's doesn't require that updated of a system (minimum kernel version), it's meant to run on x86_64 machines, it requires linking to a library somewhere on the system, it doesn't require a specific memory address, it contains debugging information, and the byte order is least to greatest.
# Pre-Processors and Global(s)
```
#include <stdio.h>
#include <unistd.h>
#include <stdbool.h>

void s_mess();
void f_mess();
void w_mess();
bool compare_two();
int compare();
void print_asts();
int user_input;
```

## Pre-Processors
These are the /#include's, or (not present in the example above) \#def's and compiler logic statements (\#if, \#else, \#endif, etc.). It's my understanding Ghidra doesn't catch global variables or pre-processors because they aren't included in the binary. Since these are used before the compilation by the compiler, and they aren't part of the final binary, they don't show up in the decompiler. This means assembly is especially important because a reverse engineer may not have the fortune of seeing a direct C translation of a macro or header module, instead relying on Ghidra's decompilers best efforts of a translation or just plain assembly.
## Functions
The rest are functions (except user_input) and found automatically by Ghidra in ==Symbol Tree > Functions==. These are also found when using the `nm` command on the binary, as seen above. In the real world this may not be possible, but here one can see comparing the `nm` command to the source that all functions are accounted for.
## Global Variables
Thanks to `nm` one can also see there exists a variable called "user_input" telling the engineer this script likely requires (or records) user input (unwittingly or not). This could be a red herring variable name, but since the source code is provided one knows it is not. It's marked as an undefined symbol, so all that is known is that it exists nothing pertaining to what it holds... yet! This doesn't show up in the Functions symbol of the Symbol Tree either, but it does make an appearance in the Labels section! 