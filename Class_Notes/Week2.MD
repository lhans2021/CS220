# CS 220 | Week 2

## Jan. 25, 2023

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

## Jan. 27, 2023
