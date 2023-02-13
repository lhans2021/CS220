# CS 220 | Week 2

### Programmer's View of a Computer (Our Typical View) 

- Imagine I am a programmer. As such, the way I view my programming of a computer is: 
    1. Very abstractly. The code that I write is just what it is-- I don't care about what happens under the hood. 
    2. All the variables are the same. 
        - Same access time, same availability, and same space 
    3. All the instructions are the same 
        - Same amount of time to execute, and same amount of resources

### Looking Under the Hood (More Advanced View)

- But, a programmer's view ABSTRACTS lots of what's happening in the hardware. 

- If we know what happens under the hood, we can write better programs! 
    - Example: in the class code example with the matrix, when traversing through COLUMNS first, we got a faster result than when traversing with ROWS first. So obviously, those variables and instructions are NOT just the same! Knowing the difference can help.

### Abstraction in CS and Filling in Gaps

- Between writing your code in a programming language, say C, and compiling it with the GNU gcc, there is a lot that's going on. 
    - Compiler, shell, loader, OS, architecture, and hardware (e.g. transistors) 

- Abstraction: shows the essence of something but hides all of the other concrete details under the object 
    - Example: Soccer ball, planets, and more are all "balls"-- they are sphererical in shape by nature. 
    - In CS, data structures, algorithms, numbers, GUIs, etc. are all abstract things. 
        - Take data structure for example. It does not tell you how exactly the data is structured; you just simply know how to use it to store stuff. The concetrate details are hidden. 

- Cache: memory that is stored really closely to the computer's CPU, so you will have quick access to it. However, it is very limited in terms of how much it can store. 


### Richard Stallman
- Developed "copyleft" 
- Caused DARPA to require passwords in MIT
- Created the first recursive acronym, GNU. GNU is a software that can be used in operating systems (OS) to do: 
    - Compiler, debugger, and so much more 

### UNIX
- Oldest "modern" operating system that has many flavors (e.g. Android, Linux, iOS, etc) 

- Most widely used.

- Operating System: software that manages your hardware and makes it work. If you delete the OS, your computer won't work

### Command Line Capabilities

- Command Line: allows us to communicate through text based interface with the OS 

- Editor (e.g. gedit, VIM, Notepad++)
- Compiler / Linker (gcc)
- Build manager (make) 
- Debugger (gdb)
- Project management (git)

### GCC (GNU C Compiler)
- To compile in our class: 
    gcc (commands) 

1. -o is for output file / command name
2. -ggdb is to include debug information to output file 
3. -Wall is to turn on all reasonable warning messages 
4. -std=c18 is to use the latest 2018 C standard 

- Example: gcc -ggdb -Wall -std=c18 -o test test.c 

### Compile / Link Process
1. Code goes through pre-processor
    - Pre-processor: deals with all of the #include and other things after "#" so that the .c file can be read 
2. The code is translated to x86 language and can produce a ".s" file for assembly, if you want it 
3. The code is translated to machine language and can produce a ".o" for those binary, if you want 
4. The linker combines the ".o" file with "libstdlib.so" to create an EXECUTABLE file, to be executed. 

### Makefile

- Make: a build manager part of GNU that will create executables

- Makefile: a file that tells "make" command what to do. 
    - THIS FILE DOES NOT HAVE ANY EXTENSION (.txt, .mk, etc)

- Makefile has a bunch of "make rules": 
    1. Target: the file that this rule produces (the executable)
    2. Dependencies: a list of files used to make the target 
    3. Recipe: Unix command(s) to produce target from the dependency files.
        - MUST HAVE TAB BEFORE RECIPE!

- Example on ppt

- To invoke "make", we need to do "make <target>". If the target is not specified, make the target the FIRST file in the Makefile

### Make Processing

1. "make" searches for the rule for the target. 
2. "make" will recursively create all dependencies that are targets of other rules 
    - Example: in the example online, "mycmd" is another target for another rule, so "make" will go to that rule and create "mycmd" 
3. "make" will invoke or ignore the recipe: 
    - If the target is a file and is NEWER than the dependency(ies), recipe will be ignored
    - If the target is a file and is OLDER than the dependency(ies), recipe will be invoked to update the target file 
    - If target is not a file, recipe will be invoked just in case

- These cascading dependencies (creating of dependency after dependency, etc) ensure everything's updated.

