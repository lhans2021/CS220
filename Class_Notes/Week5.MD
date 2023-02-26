# CS 220 | Week 5

## Data in C: Integers 

- Abstract Numbers: 
    - Literals (decimal = base 10, octal, hex, binary) 
    - Expressions 
        - Arithmetic (+, -, *, etc) 
        - Comparison (<, >, !=, etc) 
    - Standard Rules of Math Apply 
        - Associativity 
        - Commutativity 
        - Transitivity 

- Two's Complement Binary
    - Any abstract integer is actually a TWO'S COMPLEMENT BINARY NUMBER concretely. 
    - A vector of n bits that represent a number 
    - Complement: negative of the number    
    - If leftmost bit is a ZERO, number is positive. Just perform standard conversion from binary <--> base 10
    - If leftmost bit is ONE, number is negative (complement). Do the standard conversion IF it were positive, then subtract 2^n 

- Using Leaks to Calculate 2^x After Understanding Concrete Implementation of Numbers (i.e. two's complement) 
    - 2^x is just a single 1 in the x-th bit 
    - To raise something to 2^x, just use the "shift" operator to shift x number of places to get the new value 
    - Example: 
    int x = 3;
    int y = 1 << x;
    printf("%d", y);

- Using Leaks to Calculate Strings of x 1 bits 
    - We know based on a proof by induction that (2^x)-1 is a bit string of x 1 bits 
    - We also know that 2^x is just 1<<x. 
    - So, we can combine two facts to get that (2^x) -1 is (1<<x) -1. 

- Using Leaks to Negate Values 
    - To negate a value, we can flip all of the bits (negate using ~) and then add 1 (0001). 

- Unary Minus Sign (negation) 
    - Multiplication by -1, negation, is expensive
    - Instead, we can just flip all of the bits and add 1 just as described in the 3rd leak above

- Adding Unsigned Binary Numbers
    - You know how to do this

- Adding Signed, Two's Complement Binary Numbers
    - Same as unsigned binary numbers

- Subtracting Binary Numbers
    - Add the negation of the number (e.g. 5-2 = 5+(-2) )
    - Remember, to negate, we flip the bits and add 1!! 

- Multiplying Binary Numbers
    - Check slides for example
    - The idea is, you are going to do the SAME as long muliplication on paper, but with all of the 0s and 1s instead of base 10 integers 

- C Leaky Idiom: Multiply by 2^x 
    - Instead of multiplying y by 2^x, we can just do y << x to represent y x 2^x. 
    - Informal Proof: 
        2^x is just 1<<x
        y x 2^x is just y (1<<x) which is just y << x. 
    - Example: 
        int x = 2;
        int y = atoi(argv[1]);
        int ym = y<<x // this would be the same as y x 2^x

- Binary Division
    - Similar to multiplication in that it requires a LONG process of long division. There are huge chains of logic. 

- Binary Comparison (to zero)
    - "OR" all of the bits and then "INVERT" the bits
    - Look at the signed bits to see if the binary number is positive or negative 

- Truth Value of Integers in Binary  
    - Remember that each integer can be expressed as binary. 
    1. If all of the bits are 0, the integer has a FALSE truth value 
    2. If any of the bits are 1, the integer has a TRUE truth value. 

    - So, logically, to determine this, if we "AND" all of the bits and get 1, integer is TRUE. If 0, integer is FALSE.

- Truth Value Using Logical && 
    - Each integer has a truth value obtained by "AND"ing all of the bits. 
    - We use && to see if both operands are TRUE. 
    - If we take each individual integer's truth value and "AND" them with one another, 1 is TRUE 0 is FALSE. 

- Bitwise & To Select Bits (Mask)
    - We can use bitwise & to create a mask and select bits we care about! 
    1. Create a "mask" that has 1 for the interesting bits and 0 for the ones we want to ignore
    2. Bitwise "AND" the mask and the original value I'm examining
    3. Result after "AND"ing the mask and the original value would have the original bits that I care about in the 1 positions of the mask. Everywhere else, there will just be 0s. 
    
    - Example: print binary
    COME BACK TO THIS SOON PLEASE

    - Example: print hex 
    COME BACK TO THIS SOON PLEASE 

- C Leaky Idiom: Divide by 2^x 
    - Instead of dividing by 2, simply shift to the right by 2. It would be MUCH FASTER than regular division
    - WARNING: 
        - When you MULTIPLY / DIVIDE regularly, the machine will round to 0 (-3.5 to -3) 
        - When you SHIFT, the machine will round to -infinity (-3.5 to -4). 

- "Unsigned" Integers 
    - C has an "unsigned" base 10 integer keyword to represent positive values 
    - Essentially, "unsigned" will only allow for non-negative values which would be unsigned, raw bits. 
    - This will allow more bits to store the integer, which means greater range of positive base 10 integers.
    - Example: unsigned char x; can hold TWICE as much positive base 10 integers. 

- Leaky Abstraction: Infinite Integers
    - In math, we can have infinity as a "value" because each number, n, has a successor, n+1. 
    - In C, there is no infinite numbers. When the maximum value is achieved and then passed, we will return to the first number that the data type can hold
    - Example: in a signed char can hold 127 at the highest which is 0b0111 1111. If you add 1, it will become 0b1000 0000 which is NOT 128, but rather, -128. 

- Casting in C
    - Casting in C will allow us to interpret the bits differently. Unless we explicitly cast, the interpretation is based on the type of the variable

- Mixing Integer Types
    1. Mixing Type Expressions
        - Example: int x; long y; y = y * x; 

    2. Assignment Statements
        - Example: int x; long y; x = y * 3.0;
    
    3. Argument Evaluation
        - Example: int mfn(long x); int y = mfn(3);

    4. Explicit Casting
        - Example: int x = 7; long y = ((long)x / 3)

    - C Compiler MIGHT throw errors when you are mixing stuff up
    - C Compiler MIGHT require explicit casting, so in example 1, C might ask you to change the int x into a long and then do the multiplication 
    - C Compiler MIGHT do the conversion by themselves based on certain rules. 

- C Automatic Type Conversion Rules
    - C will convert everything to the most general type (if int and long, long is more general) and then use that type to do the math 
    - C will convert the value of the expression to the type of the receiver in an assignment expression
        - Example on slides 
    - C will convert expressions with explicit casts before using the value

- Generality of Numeric Types
    - Unsigned is more general than signed 
    - Check the slides for the generality. It essentially starts like: char --> unsigned char --> short --> unsigned short --> etc 

- Converting "Unsigned" <--> Signed 
    - The bits stay the EXACT same but the sign is either IGNORED or ACKNOWLEDGED. 
    - Example: 
    char x = -22
    unsigned char y = x; 
    printf("%d", y); // prints 234 

- Changing Integer Size (Signed) 
    - Add the sign bits to the left side 
    - Example: 
    char x = -22; 
    short y = x;

    -22 is 10 1010 as a char
    -22 is simply 1111 1111 1110 1010 as a short (just add 1 because it's negative) 

- Changing Integer Size ("Unsigned"") 
    - Add enough 0s to the left side because we don't care about the sign which means that adding a 1 could add a new value to the number. Adding 0 won't change anything. 

- Conversion Errors: there will be conversion errors when: 
    1. When C tries to convert a negative SIGNED number to an UNSIGNED number (because obviously, unsigned cannot have negatives) 
    2. When C tries to convert a more general number (which would require more bits) to a less general one. 

-  "Unsigned" Problem
    - In the example in the slides, we have two variables: 
    unsigned int width = +8
    int leftX;

    Now, when we enter a negative number for "leftX" and then add that to the "unsigned width", "leftX" will be also treated as unsigned. But, if we printf the sum, C will print a signed value because printf will recognize it's signed and print it that way. 
        - A possible explanation for this is because C will convert, in an expression, to the most general type. "unsigned" is more general than "signed", so the "leftX" becomes an unsigned int! 

    - This is why "Unsigned" is dangerous in C. Let's try not to use them. 

-  Storing Bytes: "Little Endian vs Big Endian" 
    - ABSTRACTLY, we see bits as being stored most significant to least significant on the right.
    - Big Endian: storing bytes based on most significant BYTE to least significant BYTE (not bits!) 
    - Little Endian: storing bytes based on least significant BYTE to most significant BYTE (not bits!) 

    - Example: in a big endian (most machines), we would store 0x0001 86A0 with 0 being the most signficant byte. But in a little endian machine, we would store it as 0xA086 0100 with A being the least significant byte on the left. 

- Why Use Little vs Big Endian? 
    - It was efficient for casting back in the old days 
    - Example: 
        If you are trying to cast an "int" which is 32 bits (4 bytes) to a short which is 16 bites (2 bytes), you would have to chop the two least significant bytes. 
            - In a big endian machine, the first two bytes are MOST significant, so you'd have to move the address to the end. 
            - In a little endian, te first two are the LEAST, so it's easier. 

- When Does Endian-ness Leak / Become a Problem? 
    1. Only on multi-byte data types (int, long, etc) 
    2. Only when we look into the bytes and bits down below where they are not treated as a number we can read 
        - Big Endian machine: first byte is the most significant byte
            - All of our computations will work because the machine will convert to the base 10 number we know. However, when we get to looking at bits from the LITTLE endian, that's when problems happen
        - Little Endian machine: first byte is the least significant 
            - When the hardware interprets bits/bytes, it will switch to a big endian form so that we can read it in base 10
            - Only problem begins when we look deep down at the bit representation that's not as a number we can read 

- IN THIS CLASS, THE MACHINES ARE LITTLE-ENDIAN!!!! 
    (!!) So if you ever want to work with bits that are NOT represented as a BASE 10 CONVERTED NUMBER, MUST USE LITTLE-ENDIAN FORMAT!!!! 
    (!!) Otherwise, no issues 

## Data in C: Floating Point Numbers 

### In General: Abstraction vs Concrete

- Abstraction: Real Numbers
    - ABSTRACTLY, real numbers are thought of some decimal values that are between integers 

- Abstraction: Floating Point Numbers
    1. Literals (any constant we can write): anything with a decimal point. These FPN literals are actually ESTIMATIONS. 
        - We can even represent powers of 10 by inserting "e" 
        - Example: 6.4e3 is 6.4 x 10^3
    2. Expressions on Floats: we can do arithmetic with these floating point literals, like +,-,comparisons 
    3.  Standard Rules of Math Apply: commutativity, associativity, etc

- Leak 1: Floating Point Numbers are APPROXIMATIONS!!! 
    - Floating Point Numbers are not exactly precise; they are ESTIMATIONS!!!!
    
- Old Day Representing Real Numbers with Bits 
    - There are an almost infinite ways to represent these! 
    1. Implied Binary Point: using a "." to imply fractional values or negative exponents 
        - Example: to represent 54.5, I would do
        1101 10.10 in which 1101 10 = 54; .10 = 1 x 2^(-1) + 0 x 2^(-2) 

    2. Have two fields of int numerator / int denominator: using two integers expressed as binary and dividing one another
        - Example: to express 109/2, I would do
        0110 1101 / 0000 0010 

    3. Scientific notation with three fields to build the real number
        - Example: to express 54.5, I would do: 
        0000 0101 / 0111 0011 / 0000 0001 which can be interpreted as
        (Base 10) / (Binary Points) / (Exponents) 
        5 + (1/4 + 1/8 + 1/16 + 1/128 + 1/256) + (1 x 10^1)  = 54.5 

- Historial Development of Binary Representation of Real Numbers 
    - Until 1970s, machines used their own mechanisms 
    - Intel had a co-processor to their main processor to deal with floating point numbers and needed a standard
    - Intel had to get a standard to implement FPNs and found DEC VACS as the best one 
    - Intel went to IEEE to get a standardized FPN
    - NOW, WE HAVE IEEE 754 CONVENTION FOR FPN!! 

- Concrete/Under-the-hood:
    - Floats use binary and use the "binary point" system discussed above
    - Scientific Notation is used for floating point numbers 
        - The normal way of representing the FPN is the following: <number from 1-9>.<fractional value> x 10^(exponent) 
        - For 0, it will be 0.0 x 10^(Exponent)

- Scientific Notation
    - Usually approximations
    - Precision: relative accuracy of the floating point number, INDEPENDENT of the exponent 
        - Example: 1/3 = 3.3333333 x 10^(-1) is a precision of 7 because there are 7 digits after the decimal point 
    - Tolerance: absolute accuracy of the FPN, DEPENDENT on the exponent 
        - Example: 1000/3 = 3.3333333 x 10^(2) is a tolerance of +/- 10^(-5). Cannot go out of that range 

- Normalized Base 2 Scientific Notation
    - Start with a base 2 rational number (binary rational number) 
        - Example: 10000.011  = 16.375 base 10
    - Then, convert to a base 2 scientific notation as described above
        - Example: 10000.011 --> 1.0000011 x 2^4 after moving the binary point to the left 4 times to get the scientific notation form in the previous section 

- IEEE Standard (32 bit float) 
    - IEEE standard of expressing floating point numbers is essentially normalized base 2 scientific notation. How it works is: 
        value = -1^(S) x 1.<fractional value in binary> x 2^(exponent) 

        S = either 1 or 0 to make the value positive or negative 
        <fractional value in binary> is just like the one above in previous ex 
        exponent = somewhere from [-126, 127] 

    - Largest Positive Value Possible is: -1^0 x 1.11111... x 2^(127) which is about 10^38
    - Smallest Positive Value Positive is: -1^0 x 1.0 x 2^(-126) which is about 1.175 x 10^(-38)
    - Smallest Negative Value Possible is: -1^1 x 1.0 x 2^(-126) which is about -1.175 x 10 ^(-38)
    - Largest Negative Value Possible is: -1^1 x 1.1111... x 2^(127) which is about -10^(38)

- IEEE 754 Standard 
    - Binary will be represented as [+/-]1.<fraction> x 2^(exponent) 
        - Fraction will be possible 23 bits 
        - Exponents will be total 8 possible bits
        - Positive/negative will be one bit 

### Abstract to Concrete Float

- How Do We Actually Convert Abstract FPN to Concrete FPN in Bits? 
    - Example: convert -729.6 
    1. Step 1: is this number a special case (e.g. zero, infinity, irrational, NaN)? 
        - NO. 

    2. Step 2: look at the sign of this number 
        - NEGATIVE, so S = 1
        - Put the S=1 in the left most bit, bit 31 

    3. Step 3: represent the absolute value of that number as binary number with binary points using calculator 
        - 1011011001.10011001... 
    
    4. Step 4: normalize into scientific notation
        - Start with binary representation x 2^0
            - 1011011001.10011001... x 2^0 
        - Then, move the precision 
            - 1.0110110... x 2^9

    5. Step 4b: "bias" the exponent which covers 8 bits 
        - 8 bit values hold integers up to 0 to 255 at largest 
        - Since our exponents will range [-127, 126], we need to sort of make it map to something in the range [1,254]
        - We do this by adding a BIAS value of 127 
            - This works because: 
                a. Our lowest exponent is -126. -126+127 = 1, which is in [1,254]
                b. Our highest exponent is 127. 127+127 = 254, which is in [1,254] 
        - In general, if we have n bits to represent the exponent, we will have a BIAS value of: 
            2^(n-1) - 1 where n = number of bits 
    
    6. Step 5: consider special cases and then bias the exponent
        - If the exponent is LESS THAN -126, we know it's a special case of negative infinity
        - If the exponent is GREATER THAN 126, we know it's a special case of positive infinity 
        - BIAS the exponent IF we are not at a special case. 
            9 + 127 = 136
        - Express the exponent as an 8 bit unsigned binary number 
            136 = 0111 1110

    7. Step 6: write the next 23 bits AFTER the binary point into the "FRAC" part (check slides for visual of placing data) 
        - 011101100... 

    8. Step 7: convert the 32 bit binary value into hex numbers to make it easier to read 

-  IEEE 754 Summary
    - Check the slides for the summary of normalization, biasing, parsing, special cases, etc 

- IEEE 754 Special Cases: 
    - If the exponent bits are ALL zero and frac are ALL zero, we have a special case of +- 0 

    - If the exponent bits are ALL one and frac are ALL zero, we have a special case of infinity 

    - If the exponent bits are ALL one and the frac have at least one 1, we have a special case of NaN (not a number)! 

- "Denormal" and "Subnormal" Special Cases: 
    - Denormal (or subnormal) means smaller than usual. In "normal" numbers, we'd have 2^(-126) and -2^(-126) as the smallest values; but with denormal, we can get even smaller

    - If exponent bits are ALL zero, we have special numbers. In this case, assume the following: 
        1. 0.<FRAC> x 2^(-126)
        - https://www.youtube.com/watch?v=WZUPNXsusOA  
    
    - Biggest Subnormal Number: 
        - Exponent would be all zeros to assume fraction starts with 0. ...
        - Fraction bits will be all 1, so 0.1111... x 2^(-126) = 1.175... x 10^(-38)

    - Smallest Subnormal Number: 
        - Exponents would be all zero
        - Fraction bits would be all zero except right most, so 0.000...1  = 1.40129 x 10^(-45)

    - The way that we represent the denormal numbers is the SAME as with normal EXCEPT that there is an IMPLIED ZERO (0. ...)  

- Subnormal Precision
    - Normal float numbers have 24 bit precision 
        - 1.FRAC where FRAC is 23 digits 
    
    - Subnormal float numbers have less
        - Biggest Subnormal has 23 bit precision because we lost the 1. ...
        - Smallest Subnormal has 1 binary digit precision since we've lost everything else except the 1 bit on the most right

- Example of conversion again from FPN to binary 
    - Convert 3.1416
        1. Step 1: convert to general binary 
            11.00100... 
        
        2. Step 2: normalize the binary 
            1.100100... 

        3. Step 3: signed bit 
            S = 0 for positive 

        4. Step 4: determine unbiased exponent 
            1 + 127 = 128 

        5. Step 5: determine the FRAC part 
            1001001...

        6. Step 6: convert to hex to read 
            0x40490FF9

### Concrete to Abstract Float

- Example of converting from BINARY to FPN (other way around!!) 
    - Convert 0x6703ece6 
        1. Step 1: expand hex digits into bits 

        2. Step 2: check for special case (exponent = 0, exponent = 255 which means all 1s) 

        3. Step 3: look at signed bit, so we know it's positive 

        4. Step 4: convert exponent to decimal and UNBIAS it by -127 

        5. Step 5: take FRAC bits and add implicit 1. .. to the front 
            1.00001... x 2^(79)

### Floating Point Manipulations

- Floating Point Addition
    - Scientific Notation Addition 
        1. Find the largest exponent
        2. Rewrite smaller exponent so both match
        3. Add the mantissa (the FRAC part) 
        4. Re-normalize     
        - Example: 
        3.5 x 10^2 + 9.7 x 10^3 = 0.35 x 10^3 + 9.7 x 10^3 = 10.5 x 10^3 (math allows) = 1.05 x 10^4
    
- Floating Point Multiplication
    - Scientific Notation Multiplication: 
        mp x 2^p = (ma x 2^a) + (mb x 2^b) 
              mp = ma x mb
              p = a + b
        
    - Multiply signs (XOR) 
    - Add unbiased exponents and re-bias
    - Multiply 1.FRACa by 1.FRACb and re-normalize 

    HUH ???

- What Happens When Types are Mixed? 
    - Mixed Type Expressions
    - Assignment Statements
    - Argument Evaluation
    - Explicit Casting

- C Automatic Type Conversion Rules
    1. C converts an expression or all parts of an expression to the most "general" type and uses that type 
    2. In an assignment or argument evaluation, C converts the value of the expression to the type of the receiver
    3. C will convert any explicit casts if the casts are valid 

- Changing Floating Point Size
    1. Truncate the fraction (if you want smaller) or pad with 0s on the right (if you want larger, just like adding 0s to decimal point)
    2. Re-bias the exponent because bias is based on the exponent and if we add or subtract bits, we need to change exponent
        - If new exponent overflows, convert to infinity 
    3. Special case for denormalized numbers!
        - May be subnormal in float, but not in double (since we have more bits to use, but not in double because it's bigger)
        - May be subnormal in double, but 0 in float 

- Converting Integer to Float
    - Add .0 to the integer and convert to nearest floating point number
    - It may not be as accurate and may become an approximation (check slides for an example)
    
    - I don't think this is related to the representing FPN as concrete bits. When integer converts to float, that's another mechanism??? 

- Converting Float to Integer
    - Truncate everything after decimal point (rounding towards 0) 
    - Express the rest as integer value 
    - Example: float w = - 32742.74112;
                int y = w; 
                // y = -32742 

- Conversion Errors 
    - When C truncates decimals, we lose the precision 
    - When C approximates floating points, it becomes an approximation 

- Integer Division Pitfall 
    - In the example about baseball, even if I'm at the bat 600 times and hit it 500 times successfully, my average batting average is still 0 because:

        We used float battingAverage = (hits / bats) * 1000;
        In this case, hits and bats are integers, so when 500/600, we get 0.83 but C rounds towards 0, so it becomes 0. 
        0 * 1000 = 0.0000... !! 

    - So be careful!

- Associativity Leak
    - Law of Associativity: (A+B) + C = A + (B+C) 
    - Floating Point arithmetic can violate this because it is approximation 

- Multiplication is Repeated Division Leak 
    - We know that multiplication, such as 2 x 3, is just 2 + 2 + 2
    - Floating Point arithmetic can violate this idea because rounding errors compound every single time and gets worse and worse 
    - If you run the code in the slides, you can see the error gets worse and worse every time 

- The idea is: because floating points are APPROXIMATIONS, there are going to be some errors when you try to do math with them since the problems can compound with each approximation


     

