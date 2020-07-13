# C and C++ compiler guide
Based on [rapidtables.com](https://www.rapidtables.com/code/linux/gcc.html)
## GCC compiler
GCC is a short of GNU Compiler Collection, a C compiler for Linux.
```shell
gcc [options] [source files] [object files] [-o outfile]
```

## GCC options
Option | Description
-|-
[`gcc -c`](#compile-source-gcc--c) | Compiles source files to object files.
[`gcc -g(level)`](#generate-debug-information-gcc--glevel) | Generate debug information to be used by GDB.
[`gcc -I(dir)`](#include-directory-of-header-files-gcc--Idir) | Add include directory of header files.
[`gcc -l(lib)`](#link-with-library-gcc--llib) | Link with a library file.
[`gcc -o output file`](#output-flag-gcc--o-output-file) | Write build output to output file.
[`gcc -O(level)`](#set-compilers-optimization-gcc--O) | Optimize for code size and execution time.
`gcc -w` | Disabled all warning messages.
[`gcc -Wall`](#gcc--Wall) | Enabled all warning messages.
`gcc -Wextra` | Enable extra warning messages.

---

## Compile source: `gcc -c`
Compiles source files to object files.
#### Syntax
```shell
gcc -c [options] [source files]
```
#### Example
```shell
gcc -c file.c
```
#### Output
Generate a `file.o` file.


## Generate debug information: `gcc -g(level)`
Generates debug information to be used by GDB debugger.

Option | Description
-|-
`-g0` | No debug information
`-g1` | Minimal debug information.
`-g` | Default debug information.
`-g3` | Maximal debug information.

> Compiling without `-g` at all and compiling with `-g0` are equivalent.

#### Syntax
```shell
gcc -g(level) [options] [source files] [object files] [-o outfile]
```
#### Example
```cpp
// hello.cpp
#include <iostream>

auto main(void) -> int {
    std::cout << "Hello world!\n";

    return 0;
}
```

Building and using `gdb`:
```shell
g++ -g hello.cpp -o hello
gdb hello
...
(gdb) run
Starting program: /home/.../hello
Hello world!
[Inferior 1 (process 15094) exited normally]
(gdb) quit
```
More information about debug levels int the [official documentation](https://gcc.gnu.org/onlinedocs/gcc/Debugging-Options.html).


## Include directory of header files: `gcc -I(dir)`
Adds include directory of header files.
#### Syntax
```shell
gcc -Idir [options] [source files] [object files] [-o outfile]
```
#### Example
`header/main.h`
```cpp
auto greetings() { std::cout << "Hello world!"; }
```

`main.cpp`
```cpp
#include <iostream>
#include "main.h"

auto main(void) -> int {
    greetings();

    return 0;
}
```

Building `main.cpp` without include `header/`:
```shell
g++ main.cpp -o main
main.cpp:2:10: fatal error: main.h: No such file or directory
    2 | #include "main.h"
      |          ^~~~~~~~
compilation terminated.
```

Building `main.cpp` with `header/`:
```shell
g++ -Iheader main.cpp -o main
./main                           
Hello world!
```

## Link with library: `gcc -l(lib)`
Links with a library file.
> `gcc -L(dir)`: Adds custom library directory
#### Syntax
```shell
gcc [options] [source files] [object files] -l(libname) [-o outfile]
```
#### Example
Linking static library file `libmath.a`:
```shell
gcc -static file.c -lmath -o file
```
Linking shared library file `libmath.so`:
```shell
gcc file.c -lmath -o file
```
> Note: static library is included in the final binary, shared library is loaded in run-time (external dependency), [more information here](https://stackoverflow.com/questions/2649334/difference-between-static-and-shared-libraries).


## Output flag: `gcc -o output file`
Write the build output to and output file.
#### Syntax
```shell
gcc [options] [source files] [object files] -o output
```

## Set compiler's optimization: `gcc -O`
Set the compiler's optimization level. (Average performance *)
Option | Optimization level | Execution time | Code size | Memory usage | Compile time
-|-|-|-|-|-
`-O0` | Optimization for compilation time (default) | + | + | - | -
`-O1` or `-O` | Optimization for code size and execution time | - | - | + | +
`-O2` | Optimization more for code size and execution time | -- || + | ++
`-O3` | Optimization more for code size and execution time :fire: || -- || +++
`-Os` | Optimization for code size || -- || ++
`-Ofast` | O3 with fast none accurate math calculations | --- || + | +++

> +increase, ++increase more, +++increase even more

> -reduce, --reduce more, ---reduce even more

Strange behavior [here](https://stackoverflow.com/questions/28875325/gcc-optimization-flag-o3-makes-code-slower-than-o2) :exclamation:.