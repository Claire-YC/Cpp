# Ch2 Variables and Basic Types

## 2.1 Built-in types

> 1. arithmetic types
>    - integral types (including character and boolean types)
>    - Floating-point types
> 2. Special type - void

### 2.1.1 Advice of using the types:

> 1. Use **int** for integer arithmetic, and if the data values are large enough using **long long**.
> 2. Use **char** or **bool** only to hold characters or truth values.
> 3. Use **double** for floating-point computations.

### 2.1.2 Type Conversions

```c++
bool b = 42;			// b is true
int i = b;				// i has value 1
i = 3.14;				// i has value 3 (直接阶段性，不会四舍五入)
double pi = i;          // pi has value 3.0 （小数位为0）
unsigned char c = -1;   // assuming 8-bit chars, c has value 255 [mod(-1, 256)]
signed char c2 = 256    // 256 is out-of-range, then c2 is undefined
```

### 2.1.3 LIteral

> Integer and Floating-Point:
>
> 1. Octal: **0**20
> 2. Hexadecimal: **0x**14
> 3. 3.14159E0 / 3.14159E3
>
> Char and String :
>
> 1. 'a', 'A'
>
> 2. "Hello World", "A" [The compiler appends a **null character '\0'** to every string literal]
>
>    ```c++
>    std::cout << "a really, really long string literal "
>                 "that spans two lines" << std::endl;
>    ```
>
> Pointer literal : nullptr

## 2.2 Variables

> It's a good habit to define an object near the point at which the object is first used.

### 2.2.1 Initialization

```c++
int units_sold = 0;
int units_sold = {0}; // This is called list initialization.
int units_sold{0};
int units_sold(0);

// warning:
long double pi = 3.1415926536;
int a{pi}, b = {pi}; // Error: list-Init cannot be used if the information is lost.
int c(pi), d = pi;   // Valid, but the value will be truncated.
```

### 2.2.2 Variable Declarations and Definitions

```c++
int j;			// defines j
extern int i;	// declares i [using "i" which is defined in other file]
extern double pi = 3.14159;	//definition
```

### 2.2.3 Identifiers

> Conventions for variable names:
>
> 1. Variables are usually lowercase: index, cnt
> 2. Classes begin with uppercase letter: Sales_item
> 3. Multiple words: student_loan, studentLoan

## 2.3 Compound types

### 2.3.1 References

> A reference defines an alternative name for an object. Itself is not an object.
>
> Attentions:
>
> 1. The type of references and variables have to match.
> 2. References cannot bind to literals.

```c++
int ival = 1024;
int &refVal1 = ival;	// refVal refers to(is another name for) ival
int &refVal2; 			// References must be initialized and cannot be changed again.
int a = refVal; 		// a = ival = 1024
```

### 2.3.2 Pointers

> Pointers are used for indirect access to other objects. They hold the address of another objects.
>
> Attentions:
>
> 1. We may not define a pointer to a reference.
> 2. It's illegal to assign an "int" variable to a pointer, even if the variable's value happens to be 0. [So with integer literal]
> 3. Define a pointer only after the object to which it should point has been defined.
> 4. Nonzero pointer evaluates as true in conditions.
> 5. Two pointers are equal if they hold the same address.

```c++
// Pointer's definition
int ival = 42;
int *p1 = &ival;	// p1 holds the address of ival;
int *p2 = p1;		// Pointers can be assigned or copied. p2 holds the address of ival.
/*
ival = 42
the address of ival is 0x7ffee7ab29c8
p1 = 0x7ffee7ab29c8
*p1 = 42
p2 = 0x7ffee7ab29c8
*p2 = 42
*/

*p2 = 10;	// We can change the value that p2 points. [ival = 10]
p2 = 0;	// p2 points no object.

// Null pointers
int *p3 = nullptr;	// "nullptr" is a literal
int *p4 = 0;
int *p5 = NULL; // Must #include <cstdlib>

// Void pointers
double obj = 3.14;
void *pv = &obj;	// void pointer holds the address of any type object.
/* We cannot retrieve the value of void pointer. */
```

### 2.3.3 Understanding Compound Type Declarations

```c++
int i = 104, *p = &i, &r = i;	
/* 
"i" is an int variable
"p" is a pointer to i
"r" is a reference to i
*/
```



# Ch3 Strings, Vectors, and Arrays

# Ch4 Expressions

# Ch5 Statements

# Ch6 Functions

# Ch7 Classes

