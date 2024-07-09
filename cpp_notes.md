# Basic Code syntax 
```cpp
#include<iostream>

int main(){
    std::cout << "Hello World" << std::endl;
    return 0;
}
```
---
# Commenting in Cpp

`//`  is used to make single line comments

`/*  */` is used to make multilne comments  

---
# Types of Errors in Cpp 

    1. Compile Time Errors 
    2. Run Time Errors 
    3. Warnings 

---
# Statements in Cpp

* A statement is basic unit of computation in a c++ program.
* Every c++ program is a collection of statements organized in a certain way to achieve some goal 
* Statements end with a semicolon in c++ (;)
  
---
# Data Input and Output 

|stream|purpose|
|------|-------|
|std::cout|Printing data to the console (terminal)|
|std::cin|Reading data from the terminal|
|std::cerr|Printing errors to the console|
|std::clog|Printing log messages to the console|

now we will discuss few code snippets to understand the concepts of inputting data in c++ 

<b> if we need to input data with spaces</b>
```cpp
    std::string full_name;
    int age;
    std::cout << "Please type in your full name and age " << std::endl;
    std::getline(std::cin,full_name);
    std::cin >> age;
    std::cout << "Hello " << full_name << " you are " << age << " years old!" << std::endl;
```


* As we have seen till this point to we write cout as shown below 
```cpp
std::cout<<"Message to be printed on screen"<<std::endl;
```
but insted of writing of writing std:: all the time we can at the start of the program declare 

```cpp
#include<iostream>
using namespace std;

int main(){
    cout<< "Now we don't need std:: any more infront of cout"<<endl;
}
```
so the crux of this is that in order to use cout we need to include the header file <b>iostream</b> and std is a namespace inside this header file. 

---
# Data Types and Variables 

* Primitive Data types  
  1. Integral
       * int
       * char
  2. bool
  3. floating point   
        * float 
        * double   


* User defined Data types 
  1. enum 
  2. structure 
  3. union 
  4. class 

* Derived Data types 
  1. Array
  2. Pointer 
  3. References 
   
---
# Other Important points 

  ### To use the mathametical functions you can use the header file called cmath 
```cpp
    #include <iostream>
    #include <cmath>
    int main() {
    double a, b, c;
    std::cout << "Enter coefficients a, b and c: ";
    std::cin >> a >> b >> c;
    double root1 = (-b + sqrt(discriminant)) / (2 * a);
    double root2 = (-b - sqrt(discriminant)) / (2 * a);
    return 0;
    }
```

# Compount Assignments 
Compound assignment operators in C++ combine an arithmetic or bitwise operation with an assignment. They provide a shorthand way to update the value of a variable.
| Operator | Description            | Example      | Equivalent to     |
|----------|------------------------|--------------|-------------------|
| `+=`     | Addition Assignment    | `x += 3;`    | `x = x + 3;`      |
| `-=`     | Subtraction Assignment | `x -= 2;`    | `x = x - 2;`      |
| `*=`     | Multiplication Assignment | `x *= 2;` | `x = x * 2;`      |
| `/=`     | Division Assignment    | `x /= 2;`    | `x = x / 2;`      |
| `%=`     | Modulus Assignment     | `x %= 3;`    | `x = x % 3;`      |
| `&=`     | Bitwise AND Assignment | `x &= 3;`    | `x = x & 3;`      |
| `|=`     | Bitwise OR Assignment  | `x |= 3;`    | `x = x \| 3;`     |
| `^=`     | Bitwise XOR Assignment | `x ^= 3;`    | `x = x ^ 3;`      |
| `<<=`    | Left Shift Assignment  | `x <<= 1;`   | `x = x << 1;`     |
| `>>=`    | Right Shift Assignment | `x >>= 1;`   | `x = x >> 1;`     |

### Summary 
* Compound operators improve readability and conciseness.
* They do not provide performance benefits.
* Modern compilers optimize the code, so both compound assignments and their equivalent separate operations result in the same performance.  

Thus, while compound assignment operators are useful for writing clearer and more maintainable code, they do not inherently make the code run faster.

---
# Increment and Decrement operators 
1. Pre Increment (++x) and Post Increment (x++)
2. Pre Decrement (--x) and Post Decrement (x--)

Lets talk about the two types of Increments Pre and post in terms of code and then differentiate between them 

```cpp
int x = 5,y;

// lets start with pre-increment 
y = ++x; 

/* In this case the result will be 
y = 6 
x = 6 
so the x will be incremented first and then assigned to y */

// now lets see the post-increment 
y = x++; 

/* In this case the results will be 
y = 5 
x = 6 
so in this case the assignment will take place first and then the increment */
```
lets look at one more example of the same 

```cpp 
int x = 5 , y = 10 , z ;

z = x++ * y ;
/* In this case the result will be 
z = 50 
x = 6 
so basically first the multiplication takes place and then the increment */

z = ++x * y ; 
/* In this case the result will be 
z = 60 
x = 6 
Here first the increment took place and then the multiplication */
```
---
# Overflow in C++

**Overflow** occurs when a calculation produces a result that exceeds the range that can be represented with a given number of bits. In C++, overflow can happen with both integer and floating-point operations, though the behavior differs.

### Integer Overflow

For signed integers, overflow is undefined behavior in C++. This means that the program's behavior is unpredictable if an overflow occurs.

For unsigned integers, overflow wraps around using modulo arithmetic. This means that if an operation results in a value larger than the maximum value, it wraps around to the beginning of the range.

#### Example

```cpp
#include <iostream>

int main() {
    unsigned int u = 4294967295; // Maximum value for 32-bit unsigned int
    u = u + 1; // Overflow: wraps around to 0
    std::cout << "Unsigned int after overflow: " << u << std::endl;

    int i = 2147483647; // Maximum value for 32-bit signed int
    i = i + 1; // Overflow: undefined behavior
    std::cout << "Signed int after overflow: " << i << std::endl;

    return 0;
}
```
---
# Bitwise Operators in C++

Bitwise operators are used to perform bit-level operations on integral data types (such as `int` and `char`). Here are the common bitwise operators in C++:

- `&` (AND): Performs a bitwise AND operation.
- `|` (OR): Performs a bitwise OR operation.
- `^` (XOR): Performs a bitwise exclusive OR operation.
- `~` (NOT): Performs a bitwise NOT operation (one's complement).
- `<<` (Left Shift): Shifts bits to the left.
- `>>` (Right Shift): Shifts bits to the right.

Here is a table summarizing these operators:

| Operator | Name        | Description                                        |
|----------|-------------|----------------------------------------------------|
| `&`      | AND         | Sets each bit to 1 if both bits are 1              |
| `(pipe)`      | OR          | Sets each bit to 1 if one of the bits is 1         |
| `^`      | XOR         | Sets each bit to 1 if only one of the bits is 1    |
| `~`      | NOT         | Inverts all the bits (one's complement)            |
| `<<`     | Left Shift  | Shifts bits to the left and fills with zeros       |
| `>>`     | Right Shift | Shifts bits to the right and may fill with sign bit|

### Examples

```cpp
int a = 5;  // 0101 in binary
int b = 3;  // 0011 in binary

int andResult = a & b;  // 0001 in binary, which is 1 in decimal
int orResult = a | b;   // 0111 in binary, which is 7 in decimal
int xorResult = a ^ b;  // 0110 in binary, which is 6 in decimal
int notResult = ~a;     // 1010 in binary (two's complement), which is -6 in decimal

int leftShift = a << 1; // 1010 in binary, which is 10 in decimal
int rightShift = a >> 1;// 0010 in binary, which is 2 in decimal

```
---
# Enum in C++

An `enum` (short for "enumeration") is a user-defined data type in C++ that consists of a set of named integral constants, known as enumerators. Enums are used to assign names to the integral constants to make a program easy to read and maintain.

### Syntax

```cpp
enum EnumName { enumerator1, enumerator2, ..., enumeratorN };
```
### Example 
```cpp
enum Color {
    RED,
    GREEN,
    BLUE
};

Color myColor = RED;
```
### Characteristics 
* By default, the first enumerator has the value 0, the second has the value 1, and so on.
* You can explicitly assign values to the enumerators.
* Enums improve code readability and maintainability.

### Example with Explicit Values 
```cpp
enum Days {
    MONDAY = 1,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY
};
```
In the above example, MONDAY is assigned the value 1, and the subsequent enumerators increment from that value.

### Benefits of Using Enums
`Readability`: Enums make the code more readable by providing meaningful names for integral values.  

`Maintainability`: Enums make it easier to update and manage the code.  

`Type Safety`: Enums provide a type-safe way to work with sets of related constants.

```cpp
#include <iostream>

enum TrafficLight {
    RED,
    YELLOW,
    GREEN
};

int main() {
    TrafficLight light = RED;
    if (light == RED) {
        std::cout << "Stop!" << std::endl;
    }
    return 0;
}
```
---
# Typedef in C++ 
In C++, typedef is used to create an alias for an existing type. This can make code more readable and easier to manage, especially when dealing with complex types.

Here's a simple example to explain how typedef works:
```cpp
#include <iostream>

// Define a new name 'Distance' for the type 'double'
typedef double Distance;

// Function to calculate the area of a rectangle
Distance calculateArea(Distance width, Distance height) {
    return width * height;
}

int main() {
    Distance width = 5.0;
    Distance height = 10.0;
    Distance area = calculateArea(width, height);

    std::cout << "Area: " << area << std::endl;

    return 0;
}
```
### Explanation 
* In this example, typedef double Distance; creates a new name Distance for the type double.
* This means you can now use Distance instead of double in your code.
* It doesn't change how the code works; it just makes it more readable and easier to understand.  

By using typedef, you can give more meaningful names to types, which can make complex code easier to understand. For example, using Distance instead of double immediately tells you that the variable is related to a measurement of distance.

---
# Conditionals ( if-else block) in C++ 

### `if-else` Statement 

```cpp 
if (condition) {
    // Code to execute if condition is true
} else {
    // Code to execute if condition is false
}
```
### `Nested if-else` Statement 
```cpp 
if (condition1) {
    // Code to execute if condition1 is true
    if (condition2) {
        // Code to execute if condition1 and condition2 are true
    } else {
        // Code to execute if condition1 is true and condition2 is false
    }
} else {
    // Code to execute if condition1 is false
    if (condition3) {
        // Code to execute if condition1 is false and condition3 is true
    } else {
        // Code to execute if condition1 and condition3 are false
    }
}
```
### `Single statement after if`
```cpp
if (condition)
    single_statement;
```
### `Single statement if-else`
```cpp
if (condition)
    single_statement_if_true;
else
    single_statement_if_false;
```

### `else-if ladder`
```cpp
if (condition1) {
    // Code to execute if condition1 is true
} else if (condition2) {
    // Code to execute if condition2 is true
} else if (condition3) {
    // Code to execute if condition3 is true
} else {
    // Code to execute if none of the above conditions are true
}
```

---
# Logical Operators in C++
Logical operators are used to perform logical operations on one or more operands. In C++, there are three primary logical operators: && (logical AND), || (logical OR), and ! (logical NOT). These operators are used to combine or invert boolean expressions.

* `&&` (Logical AND): Returns true if both operands are true.
* `||` (Logical OR): Returns true if at least one of the operands is true.
* `!` (Logical NOT): Returns true if the operand is false and vice versa.

### Example showing compound conditional statements in use
```cpp 
#include <iostream>

int main() {
    int age;
    bool hasPermission;

    std::cout << "Enter your age: ";
    std::cin >> age;
    std::cout << "Do you have permission? (1 for yes, 0 for no): ";
    std::cin >> hasPermission;

    if ((age > 18 && age < 65) || hasPermission) {
        std::cout << "You are allowed to enter." << std::endl;
    } else {
        std::cout << "You are not allowed to enter." << std::endl;
    }

    return 0;
}
```
---
# Switch Case in C++
The switch statement in C++ is a control structure that allows you to execute one block of code from multiple options based on the value of an expression. It is often used as an alternative to a series of if-else statements when you have multiple potential values for a single variable and want to execute different code for each value.

### Syntax
```cpp
switch (expression) {
    case constant1:
        // Code to execute if expression == constant1
        break;
    case constant2:
        // Code to execute if expression == constant2
        break;
    // You can have any number of case statements
    default:
        // Code to execute if none of the cases match
}
```
### Example usage 
```cpp 
#include <iostream>

int main() {
    int day;

    std::cout << "Enter a number (1-7) to get the day of the week: ";
    std::cin >> day;

    switch (day) {
        case 1:
            std::cout << "Monday" << std::endl;
            break;
        case 2:
            std::cout << "Tuesday" << std::endl;
            break;
        case 3:
            std::cout << "Wednesday" << std::endl;
            break;
        case 4:
            std::cout << "Thursday" << std::endl;
            break;
        case 5:
            std::cout << "Friday" << std::endl;
            break;
        case 6:
            std::cout << "Saturday" << std::endl;
            break;
        case 7:
            std::cout << "Sunday" << std::endl;
            break;
        default:
            std::cout << "Invalid number! Please enter a number between 1 and 7." << std::endl;
    }

    return 0;
}
```
### Important Points
* `Break Statement`: The break statement is crucial. Without it, the program continues to execute the subsequent cases (fall-through behavior), which is usually not desired.
* `Default Case`: While optional, it’s good practice to include a default case to handle unexpected values.
* `Case Constants`: The values for case must be constant expressions and of the same data type as the switch expression.  

Using switch statements can make your code more readable and efficient when dealing with multiple potential values for a single variable.

---
# While & Do-While Loop in C++ 

## While loop 
The while loop continues to execute a block of code as long as the specified condition is true. The condition is evaluated before the execution of the loop body.

### Syntax 
```cpp
while (condition) {
    // Code to execute while the condition is true
}
```
### Example 
```cpp
#include <iostream>

int main() {
    int count = 1;

    while (count <= 5) {
        std::cout << "Count is: " << count << std::endl;
        count++;
    }

    return 0;
}
```
## Do-While Loop 
The do-while loop is similar to the while loop, but the condition is evaluated after the execution of the loop body. This guarantees that the loop body is executed at least once, even if the condition is false initially.

### Syntax 
```cpp 
do {
    // Code to execute at least once, and then while the condition is true
} while (condition);
```

### Example 
```cpp
#include <iostream>

int main() {
    int count = 1;

    do {
        std::cout << "Count is: " << count << std::endl;
        count++;
    } while (count <= 5);

    return 0;
}
```
## Differences Between While and Do-While Loops
1. `Condition Check Timing:`  

    * `While Loop`: The condition is checked before the loop body executes. If the condition is false initially, the loop body does not execute at all.
    * `Do-While Loop`: The condition is checked after the loop body executes. This guarantees that the loop body executes at least once, regardless of the condition.
2. `Usage`:
    * `While Loop`: Use when you want to execute the loop body zero or more times, depending on the initial condition.
    * `Do-While Loop`: Use when you want to execute the loop body at least once and then continue based on the condition.