# Basic

## 编译

> 编译： g++ name.cpp | g++ -o a.out name.cpp
>
> 运行：./ a.out

## Main funcion

```c++
int main()
{
    return 0;	// return type has to be "int" which is compatible with "function type".
}
// The value returned from main is a status indicator.
// "0" -- success
// nonzers -- kinds of error
```

## Input / Output

> `#include<iostream>`
>
> The library has two fundamental **types**: istream & ostram.
>
> Define four **objecst**:
>
> 1. Standard input: istream object -> **cin**
> 2. Standard output: ostream object -> **cout**
> 3. Standard err: stream object -> **cerr** & **clog** 
>    (cerr: warning or error message) (clog: general information about the execution of the program) 
>
> Manipulator: **endl**
> (1. ending the current line; 2. flush the buffer in order to write all the outputs to the output stream)

### Ex1 std::cout

```c++
#include<iostream>
int main()
{
	std::cout << "Enter two numbers:" << std::endl;
	int v1 = 0, v2 = 0;
	std::cin >> v1 >> v2;
	std::cout << "The sum of " << v1 << " and " << v2
			  << " is " << (v1 + v2) << std::endl;
	return 0;
}
```

### Ex2 using std::cout

```c++
#include<iostream>
using std::cin;
using std::cout;
using std::endl;
int main()
{
	cout << "Enter two numbers:" << endl;
	int v1 = 0, v2 = 0;
	cin >> v1 >> v2;
	cout << "The product of " << v1 << " and " << v2
		 << " is " << (v1 * v2) << "." << endl;
	return 0;
}
```

### Ex3 using namespace::std

```c++
#include<iostream>
using namespace::std;

// Miles are converted to kilometers
int main()
{
	double miles = 1.0;
	while (miles != 0){
		cout << "Input distance in miles or 0 to terminate: ";
		cin >> miles;
		cout << "\nDistance is " << (miles / 1000) << " km." << endl;
	}
	return 0;
}
```

## File redirect

> Using files as the standard input/output.
>
> `./a.out < infile > outfile` : read input from infile and write its output into outfile.

## Flow of control

### While 

#### Ex1-normal

```c++
#include<iostream>
using namespace::std;

int main()
{
	int sum = 0, val = 1;
	while (val <= 10){
		sum += val;
		++val;
	}
	cout << "Sum of 1 to 10 inclusive is " << sum << endl;
	return 0;
}
```

#### Ex2-unknown number of inputs

```c++
#include<iostream>
using namespace::std;

int main()
{
	int sum = 0, val = 0;
	while (cin >> val) // Test istream is valid or not. 
		sum += val;
	cout << "Sum is " << sum << endl;
	return 0;
}
// Invalid: end-of-file (control-d) || invalid input (not int)
```



### For

```c++
#include<iostream>
using namespace::std;

int main()
{
	int sum = 0;
	for (int val = 1; val <= 10; val++) // val exists only inside the "for"
		sum += val;
	cout << "Sum of 1 to 10 is " << sum << endl;
	return 0;
}
```

### If

```c++
#include<iostream>
using namespace::std;

// Count the same input numbers
int main()
{
	int currVal = 0, val = 0;

	if (cin >> currVal){
		int cnt = 1;
		// The last number will not be printed out
		while (cin >> val){
			if (currVal == val)
				cnt++;
			else{
				cout << currVal << " occurs " << cnt << " times." << endl;
				currVal = val;
				cnt = 1;
			}
		}
		cout << currVal << " occurs " << cnt << " times." << endl;
	}
	return 0;
}
```

### Class

> A class defines a **type** along with **a collection of operations** that are related to that type.
>
> To **use a class** we need to know three things:
>
> 1. What is its name?
> 2. Where is it defined?
> 3. What operations does it support?
>
> **Member function**: a member function is defined as a part of a class

#### Ex-Bookstore

> Type "Sales_item" has following operations:
>
> 1. function isbn() -- fetch ISBN of the object
> 2. ">>" and "<<" -- read and write objects
> 3. "=" -- assign one object to another
> 4. "+" -- add two objects (same ISBN) [number sold] [total revenue]

```c++
// Add the same ISBN book assuming transactions with the same isbn grouped together.
// 命令：./a.out < book_sales
#include <iostream>
#include "Sales_item.h"

using namespace::std;

int main()
{
	Sales_item total;

	if (cin >> total){  // ">>" operation
		Sales_item trans;
		while (cin >> trans){
			if (total.isbn() == trans.isbn())
				total += trans; // "+" operation
			else{
				cout << total << endl;
				total = trans;
			}
		}
		cout << total << endl;
	}else{
		cerr << "No data?!" << endl;
		return -1;
	}
	return 0;
}
```

# Details

## Expression: operands + operator

> <u>**Operators**</u>:
>
> 1. "**<<**": output 
>    [ *std::cout* **<<** *"Hello"* ---> 1). Print out "hello" on the window; 2). Return **left-side** operand-std::cout ]
> 2. "**>>**": input
>    [std::cin **>>** v1]
> 3. "**::**" : scope 
>    [std::cout ---> using cout defined in standard library]
>
> 

## Literal

> String literal: "Hello World!"
>
> 



# 其他

## 中英对照

### 1. 符号

> 1. Parentheses: **()**
> 2. Curly brace: **{}**
> 3. Semicolon: **;**
> 4. Angle bracket: **<>**
> 5. Double quotation mark: **""**











