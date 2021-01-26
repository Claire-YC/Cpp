# Chapter 4 Expressions

```  c++
	// 1. Mode - cases
(-21) % (-8) = (-5); // (-m % -n) == -(m % n)
(-21) % 8 = (-5);   // (-m % n) == -(m % n)
21 % (-5) = 1;   // (m % -n) == (m % n) 
```

## Basic Operators

> 1. ***Assignment operator is right associative***: 
>
>    ```c++
>    int ival, jval;
>    ival = jval = 0;  // Okay
>    
>    string s1, s2;
>    s1 = s2 ="OK";
>    ```
>
> 2. ***Increment and Decrement:***
>
>    ```c++
>    int i = 0;
>    j = i++;  // 'i' add 1, but (i++) returns the original value of 'i'->'j'=1
>    
>    int x = 2;
>    --x; // 'x' == (--x) ==1
>    ```
>
> 3. **Deference and increment**
>
>    ```c++
>    int main()
>    {
>    	vector<int> v = {1, 2, 3, -4, 5};
>    	auto p_beg = v.begin();
>    
>    	// print out the integer before the negative number
>    	while (p_beg != v.end() && *p_beg > 0)
>    		cout << *p_beg++ << endl;
>    	return 0;
>    }
>    /* [*p_beg] points to the next one, but print out the original one*/
>    ```

## Complex Operators

> 1. ***The Member Access Operators:***
>
>    ```c++
>    int main()
>    {
>    	string s1 = "a string", *p = &s1;
>    	auto n = (*p).size();  // size of s1 = 8
>    	auto m = p->size();   // "p->xize()" == "(*p).size()"
>        
>    	cout << m << endl;
>    }
>    ```
>
> 2. ***The Conditional Operators***
>
>    ```c++
>    string finalgrade = (grade < 60) ? "fail" : "pass";
>    // nest no more than two conditions
>    finalgrade = (grade > 90) ? "high pass"
>        					  : (grade < 60) ? "fail" : "pass";
>    
>    // "()" outside the consition is very important. Or it returns 0/1.    
>    cout << ((grade < 60) ? "fail" : "pass") << endl;                         
>    ```
>
> 3. ***The Bitwise Operators***
>
>    - `~`--not, 
>    - `<<`--left shift, `>>`--right shift
>    - `&`--AND,  `^`--XOR, `|` --Or
>
>    ```c++
>    int main()
>    {
>    	unsigned long quiz = 0;  // set 32-bits to zero
>    	quiz = quiz | (1UL << 27); 
>    	bool status = quiz & (1UL << 27); //get the value at 27 position
>    	cout << status << endl;
>    }
>    /*
>     * 1. "UL"-> means the "unsigned long" type - guarantees to have 32bits
>     * 2. "1UL << 27"-> shift "1" to the 27 position
>     * 3. "quiz | (1UL << 27)" -> change the value at the 27 position 
>     * */
>    ```
>
> 4. ***The sizeof Operator***
>
>    ```c++
>    	// 'sizeof' returns the size of an expression or variable, in byte
>    Sales_data data, *p;
>    sizeof(Sales_data); //size required to hold an object of type "Sales_data";
>    sizeof(p);  // size of a pointer
>    sizeof(*p); // size of the type to which "p" points --sizeof(Sales_data)
>    
>    int arr[3];
>    sizeof(arr);  // size of the entire arr, 3*int size
>    ```
>
> 5. ***Comma operator :*** evaluates the operands from left to right
>
>    ```c++
>    vector<int>::size_type cnt = ivec.size();
>    for(vector<int>::size_type ix = 0; ix != ivec.size(); ++ix, --cnt)
>        ivec[ix] = cnt;
>    ```



