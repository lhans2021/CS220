# CS 220 | Week 4

### C Processing

- Pre-Processing: a process by which the C compiler reads and interprets "macros" before compiling the rest of the program
    - Macros: a piece of code that can be replaced by something 
    - Any line that starts with "#" is a "pre-processing directive" / macro
    - Pre-processors consume the entire line and can replace something
        - Example: #include <stdio.h> will replace the #include... with whatever is in stdio.h file 

- #include is a macro pre-processor directive that can import contents of a file 
    1. #include <file.h> is to be used for system library files 
    2. #include "file.h" is to be used for local files 

- #define is another macro pre-processor that essentially replaces some value with another name 
    - Used to create compile time constants
        - No memory needed, not visible in debug

    - Formula: #define (NEWNAME_in_capital) oldname 

### Pointers and Arrays

- Pointers: practically a variable that houses a memory address of something else, so you can use the variable to access whatever is at that memory 
    - Declared using * 
        - Example: int *myIntPtr; says that myIntPtr has a MEMORY ADDRESS of an integer. 
    - Reference Operator "&": gets location of something 
        - Example: myIntPtr = &x; gives me the location of where x is stored and saves that location to myIntPtr 
    - Dereference Operator "*": gets the value at the pointer 
        - Example: printf("The value of myIntPtr is %d\n", *myIntPtr;) 
        - Example: (*myIntPtr) = 7; put the value 7 into whatever location myIntPtr is pointing to
    - Pointers have types. It tells what the type of data it is pointing to.
    - Pointers are NUMBERS! You can do arithmetic on them! 

- Using Pointers to Pass By Reference: 
    int counter = 0;
    void incrp(int *x) {
        (*x) = (*x) + 1;
    }
    incrp(&counter);
    printf("counter = %d\n", counter); 

    In that above example, we are modifying the DATA that x is pointing to. We passed the ADDRESS of counter in the function, which will do int *x = &counter, which gives me the ability to change the actual value of counter using *x.

- Simple Array (i.e. vector): 
    - Vector: one dimensional ordered list of values all of the same type 
    - Access each element by "index" (index starts at 0 for the first element) 
    - Vector (1D array) has a size (# of elements) 
    - Three ways to initialize: 
        1. Specify a size: 
    float areas[6] = {1.2, 3.5, 5.5, 2.3, 9.8, 6.7}; 
        2. Let C determine the size: 
    int stuff[] = {1,2,3,4,5}; // C will figure out that the size is 5
        3. Initialize to 0: 
    int default[12] = {0}; 
    - If you specify MORE than the size you allocated, compiler will give you a warning. 
        - If this happens, some random errors can happen. You might not get the correct values! 
    - If you specify LESS than the size you allocated, compiler will just put default value (0 for int, etc) 
    - If array is NOT initialized, the compiler will use WHATEVER UNKNOWN VALUE is in that memory area!! 


- C Pitfall: Array Bounds Checking 
    - There's NO run-time array bounds checking in C!!! It won't check to see if you're exceeding the bounds, so if you do, you might get into an infinite loop or some other issues like segmentation violation!!!
    - Example: 
    int vec[5]; int i;
    for (i = 0; i <= 5; i++) vec[i] = 4; // in this case, there's no vec[5] but the run-time doesn't know this, so it'll just add a 4 in whatever is after vec[4] and it keeps doing this over and over. Infinite loop.

- String: an array of ASCII characters that ends with a NULL terminator 
    - To declare a "string": 
    char str[14] = "This is a string"; has 13 characters so 12 indices, but actually has 14 characters and 13 indices because the null terminator 
    - The above example is really: {'T', 'h', 'i', 's', ' ', ..., 0x00}

- C Array Implementation: 
    - An array is nothing but a list of contiguous values in memory 
    - Array Declaration: int vec[5]; // this is a bunch of 5 integers next to each other in memory! 

- Array Name: 
    - The name of an array is actually the ADDRESS / POINTER to the first element! 
        - vec is the same as &(vec[0]) 
    - Therefore: 
    &(vec[i]) == (char *)vec + sizeof(vec[0]) * i == vec + i;
    - Remember: a pointer points to one OR MORE elements of a specific type! 

- Pointers and Memory
    - When you declare a pointer, the compiler will reserve space for that pointer to hold an address, but it WILL NOT reserve space at that address for data!!! So, we cannot assign a value to an address that's not specified yet.  
    - Example: int *x; // in this case, I reserved space for the pointer, but there's no space for the actual value at that memory address that's supposed to hold a value for x. 
                If I do *x = 7; i'd have a segmentation violation because nothing is actually allocated at the address x holds

- Initialized Pointers 
    - Sometimes, it may SEEM that we are reserving place in memory just by declaring a pointer. 
        - Example: char *name = "Hans Li"; 
            In this case, I am creating a literal value in memory. It could be READ ONLY or shared with the memory address of another "Hans Li" somewhere in memory. I don't know where it is 
    - "name" variable could cause segfault or could cause some other errors 
 
- Pointer Arithmetic: moving a pointer from value to value in memory, aka moving to the next element
    - Unit: the size of the data type pointed to by the pointer. If the pointer points to an array, it'll be the SIZE of the ENTIRE ARRAY!! 
    - If we add "1" to a pointer, that means "point to the next element" 
    - Example 1: 
    If int *iptr points to an integer, iptr + 1 points to the next integer (address + 4 because 4 bytes) 
    - Example 2: 
    If float (*aptr)[4] points to an array of 4 floats, aptr + 1 points to the next array of 4 floats (address + 16)
    - Example 3: 
    int *x; int vec[5];
    for (x = vec; x < &vec[5]; x++) {

        (*x) = 3;
    }

    DO NOT GET CONFUSED: float (*aptr)[4] would be a pointer to arrays, but float *aptr[4] would be an array OF 4 POINTERS

- Pointer/Array Ambiguity 
    - We can use pointers like arrays and arrays like pointers 
    - Example: 
    int suma(int nums[]) {
        int s = 0; int i = 0;
        while (nums[i] != 0) {
            s+=nums[i];
            i++;
        }
        return s;
    }
    int sump()

- Arrays as Arguments
    - When you pass in an array an argument, you are passing a POINTER to that array. 
        - The compiler will make a COPY of that pointer and use that pointer to MODIFY the ORIGINAL ARRAY since it has the memory address!!! 
    - Example: 
        void initArray(int vec[5], int v) {
            for (int i = 0; i < 5; i++) vec[i] = 32;
        }
        int areas[5]; initArray(areas, 32); // since I'm passing in the ADDRESS of "areas", the function will modify the original array I passed in.

- Can Functions Return Arrays?
    - No. But, you can return POINTERS to arrays. 
    - Problems: 
        1. If you return a pointer to a local array, it won't do anything. 
        2. If you return a pointer to a malloc'ed array, that's fine. But remember to free that space, else memory leak 

- Array Dimenensions
    1. 1D Array is called a vector
    2. 2D array is called a matrix
    3. 3D array is called a cube. 
        - Think of this as having "slices", "rows", and "columns". For each slice, there are rows and columns 

    - C uses Row-Major order (go col by col in each row, then next row and col by col, so forth) to organize the arrays 

- Array of Pointers (Ragged Arrays) 
    - Example: 
    int *xyz[2] // array of two pointers
    xyz[0] = (int *)malloc(3\*sizeof(int));
    xyz[1] = (int *)malloc(2\*sizeof(int));
    xyz[1][0] = 3; is really saying (xyz[1])[0], a pointer to the beginning of the second array (index 1) and first element there 

## Data in C: Characters (Under the Cover)

- Abstract View of Characters
    - Characters are anything on the keyboard, like 'a', 'b', '\t', etc. 
    - Character literals are in single quotes, like '@' and '\n' 
    - Characters are assigned to type char or int 
    - Character I/O: use putchar and getchar or printf with "%c" format 

- Abstract View of Strings
    - Strings are array of characters ending in '\0'
    - Strings use double quotes like "Hans" 
    - String I/O: use printf with "%s" format 

- ASCII Character Coding: 
    - Each character corresponds to a particular two digit hex number that can be translated to a decimal number from 0 to 127. NO NEGATIVES!!! 
    - Example: '6' is at 0x36 (which is 68 in decimal) 

- Hex to Binary 
    - 'A' = 0x41 = 0b0100 0001 = 65. So I can say represent A as 'A' or 65. 

- Is "char" a symbol or a number? 
    - Can be either or. We can mix them in expressions! 
    - Example: 
        char x = 'a'; int y; y = x + 1;  // add 1 to whatever number 'a' is 
        printf("%c\n", (char)y); // prints the number 'y' as its corresponding ASCII which is 'b' 

- Constants
    - Single quotes surround a single character: 
        - Example: char fi = 'T';
    - Using char as a number: 
        - Example: char fi = 68; 
    - Expressing it as hex
        - Example: char fi = 0x44; 
    - Expressing it as octal    
        - Example: char fi = 0104; 
    - Expressing it in binary
        - Example: char fi = 0b01000100; 
    - Double quotes 

- Notes on ASCII
    - Normal file Input/Output (I/O) is in ASCII. So, most of the stuff we see in English, like 'a', 'b', etc., are changed to their ASCII equivalent and then translated to hex/binary
        - Files we shouldn't be able to read ar "binary files" with all this binary encoding.
    - Most editors can ONLY read ASCII files (which is why we create the executable!)
    - Printers print using ASCII
        - If your ASCII code doesn't translate to a symbol, it's unprintable! 
        - Some of the ASCII code, like /t, are not symbols but are instructions (e.g. tab in that case) 
    - Keyboards translate to ASCII because they are the "input" 
    - Terminals translate ASCII to characters because they are the "output" 




