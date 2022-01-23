

To understand what happens to a C++ script when fed into g++/gcc, I have written the following Makefile:

```Makefile

link: assemble
	g++ build/obj/main.o -o build/exe/main.exe

assemble: compile
	g++ -c build/ss/main.s -o build/obj/main.o

compile: pre_process
	g++ -S build/pp/main.i -o build/ss/main.s

pre_process:
	g++ -E src/main.cpp -o build/pp/main.i

```

Which describes the process ilustrated in the following diagram:

![[Flowchart of C++ compilation.png]]

I will consider several C++ scripts in the hopes of understanding how it works.

The simplest program is:

```C++
int name;
```

The result from the pre-processor is

```C++
# 1 "src/main.cpp"
# 1 "<built-in>"
# 1 "<command-line>"
# 1 "src/main.cpp"

int name;
```

Which is then compiled to 

```asm
	.file	"main.cpp"
	.globl	_name
	.bss
	.align 4
_name:
	.space 4
	.ident	"GCC: (MinGW.org GCC-6.3.0-1) 6.3.0"

```

