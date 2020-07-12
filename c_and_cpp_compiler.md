# C and C++ compiler guide
Based on [rapidtables.com](https://www.rapidtables.com/code/linux/gcc.html)
## GCC compiler
GCC is a short of GNU Compiler Collection, a C compiler for Linux.
```shell
$ gcc [options] [source files] [object files] [-o output file]
```

## GCC options
Option | Description
-|-
[`gcc -c`](#gcc--c) | Compiles source files to object files.
[`gcc -g(level)`](#gcc--g(level)) | Generate debug information to be used by GDB.
[`gcc -I(dir)`](#gcc--I(dir)) | Add include directory of header files.
[`gcc -l(lib)`](#gcc--l(lib)) | Link with a library file.
[`gcc -o output file`](#gcc--o-output-file) | Write build output to output file.
[`gcc -O(level)`](#gcc--O) | Optimize for code size and execution time.
`gcc -w` | Disabled all warning messages.
[`gcc -Wall`](#gcc--Wall) | Enabled all warning messages.
`gcc -Wextra` | Enable extra warning messages.
---
## Options' description
## `gcc -c`
Compiles source files to object files.
### Syntax
```shell
$ gcc -c [options] [source files]
```
### Example
```shell
$ gcc -c file.c
```
### Output
Generate a `file.o` file.

---
## `gcc -g(level)`
Define a preprocessor macro.



### Output flag `-o`:
Write th build output to and output file.
#### Syntax
```shell
$ gcc [options] [source files] [object files] -o 
```