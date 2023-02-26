# CS 220 | Week 3

### Make Variables

- Make has its own variables-- it is practically its own language. 
    - You can set them in the command line or definition line 
    - Example: 
        CC = gcc
        CFLAGS = -Wall -std=c18 -ggdb 
    - CC and CFLAGS now act as variables 

- You can use these variables with ${nameOfVar}

### Make Implicit Rules

- Implicit Rules: rules that I have automatically because some recipes are used so often.

- Examples on slides 

### Typical CS220 Makefile 

- In the example on the slides, there is no recipe to compile into an executable because there is an implicit rule that already does the compile recipe for us. However, if there is more than one executable to build, we shouldn't use the implicit rule.

- Clean: removes the executable from the program just in case you want to restart.

### GDB (GNU Debugger) 
- GDB is a debugger that comes with GNU 

- To use, invoke "gdb <executable>" 

- Commands for GDB: 
    1. help: help on gdb commands
    2. break <location> if <condition>: sets a breakpoint at a location 
    3. run <command line arguments>: run the executable up to the next breakpoint (or end of program or until some other error) 
    4. continue: continue to the next break point
    5. step: go to next program instruction stepping into function invocations
    6. next: go to next program instruction but skip function invocations
    7. print <value or expression>: print something
    8. x / <options location>: print memory at location
    9. quit: quit 

### Git (Version Control Software)

- Linus Torvalds created it 

- Repository: a list of files git tracks, typically in a single directory 
    - You can add or delete stuff from each directory 

- Commit: similar to a "save" button in which you tell git there's a bunch of saved changed
    - You can also revert to a previous version, like an "undo" button

- There's a hidden ".git" directory below everything

### GitHub 

- A software owned by Microsoft that is a "cloud" for storing repositories on a website. 
    - You can have many copies of the repository in local systems
    - There is a main "master repository" in the "cloud" 

### COMPLETE NOTES LATER ON. 

### Programming Language History

### Origins of C 

- MULTICs Operating System: 
    - MIT/GE/Bell Labs collaborated in 1964 - 1970 to design an OS to run GE-645 Main Frame.
    - It was programmed in assembler and PL/I 

- BCPL (Basic Combined Programming Language) 
    - Martin Richards made this in 1966
    - Background in writing compilers 
    - First use of {}, //, and "Hello, World" culture 

- UNIX Operating System (1969-1970s) 
    - Bell Labs PD7-PDP

- "B" Language (BCPL "Lite")

### C Design Gols

- Simple Imperative Language:
    - Programmer tells the computer HOW to solve the problem, as opposed to asking the computer to do it 
    - Machine level complexity is abstracted 

- Easy to compile to machine language, so it can run on a small machine (e.g. PDP-11) 

- Fast machine language programs, so there's little or no run-time checking 

- Static Typing: 
    - Compiler will check to see that things are valid instead of during run-time 
    - Compiler doesn't overcheck, though 

- Access memory and other machine interfaces

- Platform Independence 

### OS History: Bell Labs 

- See Slides

### Origins of C 

- See Slides

### C Language Basics (OFFICAL START OF 220!!)

- Function: a body of code that can be used to perform the same task multiple times.
    - Basic building block of C -- almost everything in C is in a function. 
    - Functions create ABSTRACT items -- we don't care how the function does a task several times. We just know it does.
        - The more CONCRETE information is the function's definition. 
        - We can see the idea of ABSTRACTION vs CONCRETE. 
    - Functions allow for reusability -- you can keep doing that task over and over and over again.
        - The idea is to code the function CONCRETELY once and then use it over and over ABSTRACTLY. 
    - Example: 
    int cent_to_far(int t){
        return (t*9) / 5 + 32;
    }

- Variables: the name of some space in RAM memory that is used to store specific data. 
    - RAM will go away when your computer is off. 
    - Example: 
    float GPA = 3.97; 
    In this case, "GPA" is the name of some memory address in RAM that stores the value, 3.97

- Data Type: an attribute of data that tells the computer how to deal with the value
    - Tells compiler how many bits to use to store the data
        - Example: declaring a "float" would require 32 bits to be allocated 
    - Tells compiler how to interpret the bits 
        - Example: if I declare a "float", compiler will interpret first bit as the sign bit   
    - Enables automatic conversion from one to another
    - Enables compiler to make sure data is used correctly
        - Example: cannot add a String to an int, bits won't end up correctly.
        
    - Built in types: 
        1. Types To Represent Numbers: 
            a. Integers (binary 2's complement, whole numbers) 
                - char (8 bit or 1 byte) can store -2x10^7 to (2x10^7)-1
                - short (16 bits or 2 bytes) can store -2x10^15 to (2x10^15)-1
                - int (32 bits, 4 bytes) can store -2.15x10^9 to 2.15x10^9
                - long (64 bits, 8 bytes) can store -9x10^18 to 9x10^18
            b. Real (IEEE 754, decimal numbers, like 5.96) 
                - float (32 bit, 4 bytes)
                - double (64 bit, 8 bytes) 
        2. Type To Represent Text: 
            a. char (ASCII) 
        3. Void: 
            a. Nothing. It means there's nothing. 

- Statement: a list of tokens that end with a semi-colon
    - Tokens: things that perform certain functions or represent something. 
    - Statements can range multiple lines
        - Example: int myFunctionCalledFunctionThatCanSpanThisHugeLineOfTextThatIsAlsoFilledWithNothingThatsUsefulForThesePurposesOfTheClassCS220(int x, int y, int z) 
    - Can have multiple statements in a line
        - Example: 
        int x = 5; float z = 6.2; char myFirstLetter = 'a';    
    
- Variable Declaration Statements: 
    - type nameOfVariable = variableValue; 

    - Variables must be declared ONCE (e.g. int x;) before it is used, but may be assigned a value until later. 
    - Local Variable: variables that are accessible only inside a function. They are created with each instance of the function and destroyed after the function ends. 
   - Global Variable: variables that are created before the function starts. They are created usually before the main function runs and destroyed after main function ends
        - Reduces "reusability" 
        - "Visible" to any function in the program/file

- Integer Literals: decimal values you specify in your program
    - Decimal numbers are typically signed  literals
        - Example: int x = 93; 
        - Add "U" to suffix to make these decimal numbers unsigned
            - Example: unsigned char uy = 183U; 
    - Prefix with 0 is used to represent octal number
        - Example: int xa = 013 
    - Prefix with x, 0x, X, 0X is used to express hexadecimal: 
        - Example: int xb = 0x12; 
    - Add "L" suffix to make them a "long" data type
        - Example: long yl = 0x000011110000FFFFL; 

- Assignment/Expression Statements
    - Variable Declaration: int x;
    - Literal Assignment: x = 13; (assigning a literal to x)
    - Variable Assignment: y = -x; (assigning a variable to x)
    - Unary Operator: y = -x; (one operand only)
    - Binary Operator: y = x*3; (two operands) 
    - Parentheses: y = (x*3) + 7;
    - Function Invoaction: y = atoi(argv[2]); or printf("Hello world");
    - Assignment Operator: x = y = 7; assigns 7 to BOTH x and y
    - Compound Assignment Operator: x*=3; x = x * 3;

- Check the slides for a whole bunch of things you can include to create an expression. Most of these you know, but some are new:
    1. & is bitwise "AND" that will perform an "AND" on each of the bits. Same idea applies for |
    2. ^ is a bitwise "EXCLUSIVE OR" on the bits 
    3. ~ is a bitwise "NOT" on the bits
    4. << and >> are SHIFT operators to shift bits to the left (<<) or to the right (>>)
    5. Ternary Operator: cond?v1:v2
        - Condition before question mark, expression v1, and expression v2. 
        - First, evaluate condition. If true, return value v1. If false, return value v2. 

- More Operators on Standard Library Functions 
    1. stdlib.h
        - Has conversion functions (atoi, atol, etc) 
        - Has math functions (abs, labs, div, etc) 
    
    2. math.h
        - Trigonometry (asin, acos, tan, sin, etc) 
        - Exponents (sqrt, pow, log, etc) 
        - Rounding (fabs, floor, etc) 
        - NOTE: math.h uses FLOATING POINT, so if you want x^2, it will convert x to float x first and then raise to power

### C Functions

- Anatomy of a C Function:  
int cen_to_far(int t) {
    return (t*9)/5+32; 
}
- C Function Invocation: given this function functionName(argExpression, argExpression, ...)
    1. Argument expression evaluate from RIGHT to LEFT
    2. Function is "invokved". When this happens: 
        a. Space is reserved for new local variables and parameters
        b. Those above are initialized
        c. Function body is executed and ends whenever it should 
        d. Space for the local variables and parameters are returned
    
    - Function must be DECLARED before it can be INVOKVED. 

- Recursive Functions: functions that invoke themselves 
    - Example: factorial function 
        int factorial(int n) {
            if (n<=1) {
                return 1;
            }
            return n*factorial(n-1);
        }

- See diagram for recursion. You can see 4 different invoations all with their own local variables. 
    - It helps with the visual -- flip through the slides in order.
    - Allows us to understand that having invocations and local variables is important.

- "Upside Down Code": when all of the functions you want to use are defined above the function invocation (main function). 

- Function Definition vs Declaration: 
    - You can declare the function before defining it by including the following: 
        returnType functionName(parameters); 
    - This will allow us to write the function definition under main. 
    - You can declare the functions in a "test.h" file and then import it with #include  

- "RightSide Up Code": when all of your functions you want to use are DECLARED above function invocations in main, but are DEFINED after the main function 
    - Allows you to read the code downwards instead of upside. 

- Main Function: function that OS invokes. It's essentially the function that will cause your program to run!  
    - Arguments: 
        1. int argc - number of arguments passed into main (including .\<executable>!!)
        2. char **argv - array of Strings (argv is a pointer to an array of characters, aka String, or char *myString) 
    
### C Control Flow

- Sequential Control Flow: execute instructions exactly in the order from top to bottom

- If/Then/Else Statements: modifies the control flow. Two ways to write: 
    1. if (condition) (whatever you want to do) else (whatever else you want to do if not the previous case) 
    2. if (condition) {

    }
    else{

    }

- Switch Statement: multiple if/else in a row checking the same value against a bunch of options.
    - Potentially a glorified "if/else" statement
    switch(<whatever you want to check>) {
        case (<whatever you want to check it against>): 
            <stuff you want to do if true> 
            break; // if you don't have "break", if this case is a match, the program will continue executing every other   
                    // case down the line. 
        default: 
            <do this if no match is found>
    }

- While Statement: a loop body that will run if a condition is true
    while (condition) {

    }

- for loop: a loop that will start and do a particular body of code for a specific number of times AS LONG AS a condition is true. If it was never true to begin with, the body will not run
    - A glorified "while" loop
    for (initial; condition; iteration) {

    }

- do/while Statement: a while loop that will DO whatever is specified in the "DO" part FIRST, and then check the condition to see if we should keep doing it. 
    - It will definitely run at least once, because "DO" will run the first time BEFORE the condition is checked! 
    - Modified version of the "while" loop
    do {
        
    }
    while (condition);
    
- "break" statement: will cause the program to BREAK OUT of the IMMEIDATE LOOP that the statement is within 
    - Example: 
        for (int i = 0; i < 5; i++) {
            for (int j = 0; j <5; j++) {
                for (int k = 0; k<5; k++) {
                    break; // this will break out of the "for loop" with "k" as its iter variable
                }
            }
        }

- "continue" statement: will cause the program to go to the next iteration of the IMMEDIATE LOOP that the statement is within. Condition will be checked again! 