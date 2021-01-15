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
> 2. References **cannot** bind to literals.

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

#### Pointers to Pointers

```c++
#include<iostream>
using namespace::std;

int main(){
	int ival = 1024;
	int *p = &ival;
	int **p1 = &p; 	//p1 pointes to a pointer

	cout << "ival = " << ival << "\n"
		 << "indirect value = " << *p << "\n"
		 << "double indirect value = " << **p1 << "\n" 
		 << endl;
	return 0;
}
```

#### References to Pointers

> We can define a reference to a pointer.

```c++
int i = 42;
int *p;
int *&r = p;	// "r" is a reference to pointer "p" [read the modifier <--]
r = &i;			// "r" is an alias of "p", then "r" can hold the address of "i"
*r = 0;			// *r = *p = i =0;
```

## 2.4 const Qualifier

> Define a variable whose value cannot be changed. `const int bufSize = 512;`
>
> **Attention**:  To share a ***const object*** among multiple files, you must define the variable as extern.
>
> 1. File_1.cpp :  the file defines and initializes a const that is accessible to other files.
>    `extern const int bufSize = fcn();`
> 2. File_1.h : the file can use the same ***bufSize*** as defined in file_1.cpp
>    `extern const int bufSize`

### 2.4.1 References to const

> Attention: ***const reference*** restricts only what we can do through that reference. The bound object may not be a const variable.

```c++
// Type matching
const int ci = 1024;
const int &ri = ci;

// Initialization of const references
int i = 42;
const int &r = 42; // correct
const int &r1 = i;
/*
1. "r" is a const reference to "i";
2. if "i" = 10, then "r1" = 10;
3. the value of const "r1" are unchangeable, we cannot change "i" value through "r1"
*/

const int &r2 = r1 * 2;
/*
"r2" is a reference to the value of (r1*2)-the literal, instead of the expression.
*/
```

### 2.4.2 Pointers to const

> Attention: ***Pointers to const*** can point non-const variables.

~~~c++
// Pointers to const
const double pi = 3.14;
const double *p = &pi;	// We cannot use "*p" to change the value of "pi"
double dval = 2.56;
p = &dval;

// const Pointers
int errNum  = 0;
int *const p = &errNum; // "p" will always points to errNum.

const double a = 3.45;
const double *const p1 = &a; // "p1" will always points to "a", and We cannot use "*p1" to change the value of "a"
~~~

### 2.4.3 Top-level const

> Definition:
>
> 1. Top-level: the pointer itself is a const.
> 2. Low-level: the pointer points to a const object.

### 2.4.4 constexpr and Constant expression

>  Whether an object is a ***constant expression*** or not depending on two things:
>
> 1. the expression's value cannot change 
> 2. the value is evaluated at compile time.
>
> ```c++
> const int max_files = 10;			// max_file ✅
> const int limit = max_files + 1;	// limit ✅
> const int sz = get_size();			// sz❌，the value of "get_size()" isn't know until run ti,e
> ```
>
> ***Constexpr variables***: let the compiler to verify that a variable is a constant expression or not.
>
> ```c++
> constexpr int mf = 20;
> constexpr int sz = size(); 	// correct only if "size()" is a constexpr funcion.
> /*
> C++'s new standard let us define constexpr functions which is simple enough that the compiler can evaluate them at compile time.
> */
> ```
>
> ***Pointers and constexpr***:
>
> ```c++
> const int *p = nullptr;	// "p" is a pointer to 'const int'
> constexpr int *q = &max; // "q" is a const pointer to int that is null
> 
> // !!!!Confusing!!!!
> constexpr int i = 1;
> int j = 0;
> 
> int main(){
>     constexpr const int *p = &i; // "p" is a constant pointer to the const int i;
>     constexpr int *p1 = &j;      // "p1" is a constant pointer to int j.
> }
> ```
>
> 

## 2.5 Dealing with types

### 2.5.1 Type Alias

```c++
// 1. 
typedef double wages;	// wages is a synonym for double
typedef wages base, *p;	// base is a synonym for double, p for double*

// 2.
using wages = double;
using SI = Sales_item;
```

### 2.5.2 auto type

> Let the compiler deduce the type.

```c++
// 1.
auto i = 0, *p =&i;

// 2.
int i = 0, &r = i;
auto a = r;	// "a" is an int [not a reference]

// 3. auto-deduced will ignore top-level const.
int i = 0;
const int ci = i, &cr = ci;
auto b = ci;	// "b" is an 'int'(top-level const in "ci" is dropped)
auto c = cr;

auto d = &i;	// "d" is an 'int*'(& of an 'int' is 'int*')
auto e = &ci;	// "e" is 'const int*' (& of a const object is low-level const)

const auto f = ci; // deduced type of "ci" is 'int', "f" has type 'const int'
const auto &g = 42; // we can bind a const reference to a literal

// 4. reference to an auto-deduced will not ignore top-level const.
int i = 0;
const int ci = i;
auto k = ci, &l = i;	// "k" is int; "l" is 'int&'
auto &m = ci, *p = &ci;	// "m" is 'const int&'; "p" is a pointer to 'const int'
```

### 2.5.3 The *decltype* Type Specifier

> 1. `decltype(f()) sum = x; // sum has whatever type f return ` Using the type of the expression returned to define a variable.
> 2. ***decltype*** keeps top-level const and references
>
> ```c++
> // 1. decltype(reference variable) gives reference type
> const int ci = 0, &cj = ci;
> decltype(ci) x = 0;		// x has type const Int
> decltype(cj) y = x;		// y is a const_int Reference and bound to x
> 
> // 2. decltype(reference + integer) gives int/float type
> int i = 42, &r = i, *p = &i;
> int a = 100;
> decltype(r + 0) b; 		// b has type int
> decltype(*p) c = a;		// 'c' is a reference, which is an alias to 'a'
> 
> // 3. decltype((i)) gives a reference type!!
> int i = 0, j = 1;
> decltype((i)) a = j;	// 'a' is a reference, which is an alias to 'j'
> decltype(i) b = 0;		// 'b' is an int.
> ```

## 2.6 Defining Our Own Data Strutures

> In C++, we define our own data types by defining a class.

### 2.6.1 Exp-defining a new type

```c++
// The data type defining below supports no operations
struct Sales_data{
    std::string bookNo;
    unsigned units_sold = 0;
    double revenue = 0.0;
};	 
/*
1. 'bookNo', 'units_sold' and 'revenue' are called data member.
2. Don't forget ";" at the end.
*/

// We can use the 'Sales_data' type to define variables.
Sales_data accum, trans, *salesptr;
```

### 2.6.2 Using the *Exp-struct* class 

```c++
#include <iostream>
#include <string>
#include "Sales_data.h"
int main()
{
    Sales_data data1, data2; // Define two objects in 'Sales_data' type
    
    double price = 0;  // price per book
    
    // read the first transaction
    std::cin >> data1.bookNo >> data1.units_sold >> price;
    data1.revenue = data1.units_sold * price;
    
    // read the second transaction
    std::cin >> data2.bookNo >> data2.units_sold >> price;
    data2.revenue = data2.units_sold * price;
    
    if (data1.bookNo == data2.bookNo){
        unsigned totalCnt = data1.units_sold + data2.units_sold;
        double totalRevenue = data1.revenue + data2.revenue;
        std::cout << data1.bookNo << " " << totalCnt << " "
                  << totalRevenue << " ";
        if (totalCnt != 0)
            std::cout << totalRevenue / totalCnt << std::endl;
        else
            std::cout << "(No sales)" << std::endl;
        return 0;
    }else{
        std::cerr << "Data must refer to the same ISBN" << std::endl;
        return -1;
    }  
}
```

### 2.6.3 Writing Header Files

> 1. Classes are usually defined in header files. [Header's name == Class'name.]
>
> 2. **Preprocessor**: a program runs before the compiler.
>
>    - `#include`
>
>    - Header guards: *avoiding include headers multiple time*
>
>      ```c++
>      #ifndef SALES_DATA_H // 'SALES_DATA_H' is called preprocessor variable
>      #define SALES_DATA_H
>      
>      #include <string>
>      struct Sales_data{
>          std::string bookNo;
>          unsigned units_sold = 0;
>          double revenue = 0.0;
>      };	
>      
>      #endif
>      ```

