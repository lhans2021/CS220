# CS 220 | Week 6

## Memory and Pointers

- RAM: random access memory. It is essentially a bunch of hardware of flip flops and other logic gates that will turn on and control memory addresses and values stored

- Abstracting "Memory"
    - In computers, memory is like RAM but with words composed of 8 bit / 1 byte (char) characters! 
        - It's ASCII characters
        - Each byte/each character has its own memory address 
        - Each byte/character can be written or read independently 
    - This is modeled by a column with address 0 at the bottom (pretty much the image in the slide with 0x0000 0000 at the bottom being the first character/first byte)
    - Typically, to represent the address of the character, we will use 64 bit/8 byte addresses 
    - Initial memory is unknown 
    - WE CAN THINK OF A "CHAR" AS THE BASIS OF ALL MEMORY AND "WORDS"!! 

- Displaying Words of Memory
    - Usually, we want to display memory right next to each other in one "address" category, called a "word"
    - "Word": specific number of characters/bytes that we want to group together   
        - Example: an integer is usually 4 bytes long, so we put the 4 bytes next to each other under that one memory "address" category 
    - We will determine the size of that "word"
    - The "words" will be grouped together into one "address" category
    - In the slides, 
        At memory address category 0x0000 0000, we have the "word" (integer in this case) 0x1122 3344. 
        A byte is 2 hex digits, so "11" would be 0x0000 0000
                                    "22" would be 0x0000 0001
                                    "33" would be 0x0000 0002
                                    "44" would be 0x0000 0003 
        These will complete the "word" (integer) 

- C Values Related to Memory 
    - Every C value is somewhere in memory 
    - Every C value's "address" is the START of that location in memory 
    - C type tells us how LONG to read from that START of the location 
        - Display is BIG-ENDIAN!! 

- C Variables in Memory 
    - Compiler will reserve space for each variable
    - The variable's "address" is the START of the value's address in memory
        - Essentially, you would be storing the value at some place in memory and giving it a name, the variable 
    - The variable's name is essentially a LABEL at a specific address
        - Example: if I have a variable int x = 5; 
            The address of 5 would be the start of the location where that integer is stored. Let's say 0x0000 0004
            Essentially, the address of x would be that same thing. 0x0000 0004 is now an ALIAS for "x" 
            
- Declaring Pointers
    - "*" means that the variable "is a pointer to" 
        - Example: int *numPtr = 0x0000 0004;   
            This means to reserve space at a memory location called "numPtr" and put the value 0x0000 0004 into that place. 
    - Type: type of data being pointed to 
    - Name: name of the pointer that points to the location
    - Value: an address

- "Address Of" Operator
    - "&" in front of a variable name means to get the address (recall: the START of that memory area) of the variable
        - Example: int *numPtr = &height; 
            This will get me the address of height and put it in the data for the numPtr address 
    - We can also get the address of functions! 

- "Value At" Operator
    - "*" is the dereference operator that will get what's at the address of the pointer 
        - Example: int *numPtr = &height;
                   (*numPtr = 10);
                In this case, this means: go to the address that numPtr has, which is address of height, and change the height to 10 

- Memory Address Space
    - Address Space: all the memory from 0x0000 0000 0000 0000 to 0xFFFF FFFF FFFF FFFF
    - When program runs, your memory is divided into 4 kilobyte blocks. Different permissions:  
        - R (read): you can read any address in that block 
        - W (write): you can write to any address in that block 
        - X (execute): you can fetch and execute machine instructions from that block
    - Even if you have R W permission, you need to make sure nobody else can access that memory for other things
    - Compiler will reserve space for global and local variables that you can guarantee only you have access to them 

- Dynamic Memory 
    - Essentially, this is using libraries to request/return new memory on the heap 
    - malloc() will get me sole R/W permission to a certain piece of memory that I request. It will give me the address of it 

- VALGRIND
    - Tracks each malloc/free() and memory reference
        - Reports on unfreed malloc()
        - Reports on "orphaned pointers": malloc'd space that's been free() but still referenced
        - Reports on if you pass the space you asked for with malloc

- Structures and Pointers
    - FORMAT: 
    struct <name> {
        <members>
    } <declaring and making space for it>;

    - Example on slides

- Structure Pointers
    - Structure Pointers are pointers to a structure
    - Example: struct date *dptr = &today; // this is the pointer to a "struct date" called "today" 
    - We could access fields: 
        - Example: (*dptr.year);
    - We could use a shorthand
        - Example: (dptr -> year); 
    - Typically, structure memory is allocated with malloc 
        - struct date *newDate = (struct date\*)malloc(sizeof(struct date)); 
        newDate -> year = 2019;

- Structure Pointers and Call by Reference
    1. If you pass struct in as an argument, it will be a "call by value"! 
        - Example void getDOM(struct date now) {
                        return now.day;
                    }
            In this example, the entire struct is copied through a call by value 

    2. If you pass struct in as a pointer, it will be "call by reference"! 
        - Example void getDOM (struct date *now) {
                        return now->day;
                    }       

- C Structure in Memory
    - When you declare a structure, it will allocate enough CONTIGUOUS space for all the members in memory. 
    - Example: if i have a struct with 3 members, first is month, second is day, third is year, I will have memory reserved for: 
        0x0000 0000 (year) 
        0x0000 0004 (day) 
        0x0000 0008 (month) 
        Memory is stored from the FIRST on the bottom and the LAST on top (FILO) 

- C Array Implementation
    - Recall an array is a bunch of contiguous values in memory 
    - Example: int vec[5]; 
        In this case, compiler will make room for 5 integers CONTIGUOUS in memory! 

- How We See It vs How Memory Is Stored 
    - Arrays are stored from BOTTOM to TOP in memory (FILO) but we see it from TOP to BOTTOM.
    - Example: 
        int vec[3]; 

        We see it as 
        0x0000 0000 = vec[0] 
        ...
        0x0000 0008 = vec[2] 

        But it's stored as 
        0x0000 0008 = vec[2]
        ... 
        0x0000 0000 = vec[0]

- Matrix Pointer Arithmetic 
    - Example: 
    int mat[3][4]; int r; int c; 

    To get the address of a specific value, &mat[r][c], we can do the following: 

    &mat[r][c] == mat + (r * 4) + c 

    Essentially, what this is doing is: we have 3 rows and 4 columns. To get to row "r", we need to start the beginning, "mat", then get past the garbage elements before it to the "r"th row, and then go to the column we want 

-  Higher Dimension Matrices
    - One dimensional matrix: "array" == "&array[0]"
    - Two dimensional matrix: "matrix" == "&matrix[0][0]" 

    - In general, we can think of a multi-dimensional matrix as a MATRIX OF 1D MATRICES, meaning that each "row" is just another 1D MATRIX!
        - matrix[i] == matrix[i][0]; 
        - Allows us to think about "rows" as SUBARRAYS 

    - 3d matrix: "cube[i]" == "cube[i][0][0]" and "&cube[i][j]" == "&cube[i][j][0]". It's just a bunch of arrays in arrays in arrays in arrays ... in arrays!! 
    
    