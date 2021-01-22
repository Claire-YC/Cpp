# Chapter 3. String, Vectors, and Arrays

> ***Library*** types: String and Vector
>
> ***Buit-in*** type: Array

## 3.1 Namespace *using* Declarations

> 1. `using namespace::name` Using the *names* from *namespace*.
> 2. Headers should not include *using Declarations*.

```c++
#include <iostream>
using std::cin; 
using std::cout;
using std::endl; // Or using namespace::std
int main()
{
    int i;
    cin >> i;
    cout << i << endl;
    return 0;
}
```

## 3.2 Library *string* Type

> ***String*** : a variable-length sequence of characters.
>
> ```c++
> // Using "strings"
> #include <string>
> using std::string
> ```

### 3.2.1 Defining and Initializing *strings*

```c++
string s1; 			// empty string
string s2 = s1; 	// copy initialization from variable 's1'
string s3 = "hiya"; // copy initialization from string literal "hiya"
string s4(10, 'c')  // s4 is "cccccccccc"
```

### 3.2.2 Operations on *strings*

```c++
#include <iostream>
#include <string>
using std::cin; using std::cout; using std::endl;
using std::string;

// 1. Read and Write 
int main()
{
    string s;
    cin >> s;
    cout << s << endl; // whitespace-separated string
    return 0;
}
/*x
in : hello world
out: hello
*/

// 2. read a line at a time
int main()
{
	string line;
	// unitl end-of-file
	while (getline(cin, line))
		cout << line << endl;
	return 0;
}

// 3. ".empty()" 判断string是否为空 || ".size()"返回字符串长度
int main()
{
	string line;
	while (getline(cin, line))
		if (!line.empty()) // "!!line.empty()!!"
			cout << line << " " <<line.size() << endl;
		else
			cout << "empty" << endl;
	return 0;
}
/*注：".size()"返回的值的类型为：string::size_type(是一种特殊的无符号类型)*/

// 4. 字符串合并
nt main()
{
	string h = "hello", w = "world";
    
    // "hello world"
    string hw = h + " " + w; 
	cout << hw << endl; 
    
    //!!!!在加号的两边，至少有一遍是string类型的变量
    string s = h + " " + "world"; // Right: (h + " ") + "world"
	return 0;
}
```

### 3.2.3 Dealing with the *characters* in a *string*

#### 1. 字符操作 < cctype > 

```c++
char c;
isalnum(c);	// true: letter/number
isalpha(c);	// true: letter 
isdigit(c); // true: number
isxdigit(c); //true: hexadecimal-16 digit

islower(c); // true: lowercase letter
tolower(c); // A -> a
isupper(c); // true: uppercase letter
toupper(c); // a -> A

ispunct(c); // true: c is a punctuation
lsspace(c); // true: c is a whitespace
```

#### 2. Processing every characters - *range-for*

```c++
int main()
{
	string s = "Hello World!!!";
	decltype(s.size()) punct_cnt = 0;  // The type of "punct_cnt" is "string::size_type"

	for (auto c : s)
		if (ispunct(c))
			++punct_cnt;

	cout << punct_cnt << " punctuation character in " << s << endl;
	return 0;
}

	// 通过reference改变字符串中的字符
int main()
{
	string s = "hello world!!!";
	for (auto &c : s)
		c = toupper(c); // 'c' is a reference of each character

	cout << s << endl;
	return 0;
}
```

#### 3. Processing some characters - *$0 \leq$ s[index] $<$ s.size()*

```c++
// 只将第一个词大写
int main()
{
	string s = "hello world!!!";
    
	for (decltype(s.size()) index = 0;  // "&&"先查左边，保证在字符串内后，再查右边
				  index != s.size() && !isspace(s[index]);
				  ++index)
		s[index] = toupper(s[index]);
	cout << s << endl;
	return 0;
}

// Using an index for "random access"
int main()
{
	const string hexdigits = "0123456789ABCDEF";
	cout << "Enter a series of numbers between 0 and 15 separated by spaces. " << endl;

	string result;
	string::size_type n; //hold the numbers from input

	while (cin >> n)
		if (n < hexdigits.size())
			result += hexdigits[n];
	cout << "Your hex number is: " << result << endl;
	return 0;
}
```



## 3.3 Library *vector* - class template

> - A ***vector*** is a collection of objects, all of which have the ***same type*** and each object has an associated index. e,g. [a vector of int `vector<int>`] [a vector of class `vector<Sales_item>`]
>
> - To use a ***vector*** ： 
>
>   ```c++
>   #include <vector>
>   using std::vector;
>   
>   vector<int> ivec;  // 'ivec' holds objects of type 'int'
>   vector<Sales_item> Sales_vec; 
>   vector<vector<string>> file; // 'file' holds vector objects and each object is a vector of string
>   ```
>
> - C++ has both class and function templates. ***Vector*** is a ***class templates*** not. The compiler creates classes from templates. 

### 3.3.1 Define and Initialization

```c++
	// 1. 
vector<int> ivec;	// The most common way: define an empty vector and added values later
vector<int> ivec2(ivec);  //copy elements of ivec into ivec2
vector<int> ivec3 = ivec2;

vector<int>::size_type; // string::size_type

	// 2.
vector<string> articles = {"a", "an", "the"};

	// 3.
vector<int> ivec(10, -1);	// ten int-elements, each initialized to 1
vector<string> svec(10, "hi");
	// 4.
vector<int> ivec(10);	// ten elements, default initlization
vector<string> svec(10);
```

### 3.3.2 Add elements to a *vector*

```c++
// "push_back()" add a new element at the end of the vector 
	// 1.
vector<int> v2;
for (int i = 0; i != 100; i++)
    v2.push_back(i);
	// 2.
string word;
vector<string> text;
while (cin >> word)
    text.push_back(word);
/*[cannot use range-for function to add an element]*/

	// 3. other operations
v.empty();
v.size();
v[n];	// return a reference to the element at 'position-'n in 'v'
```

### 3.3.3 Subscripting(index)

> v[index] returns a **reference**.

```c++
int main()
{
	vector<unsigned> scores(11, 0);
	unsigned grade;
	while (cin >> grade)
		if (grade <= 100)
			++scores[grade/10];

	for (auto s : scores)
		cout << s << " ";
	cout << endl;
	return 0;
}
```



## 3.4 Introduction Iterators

> Access *characters in string* and *elements in vector* has two ways:
>
> 1. str[index] & vec[index];
> 2. iterators - indirect access to an object.

### 3.4.1 Using iterators

```c++
vector<int> v{1, 2, 3};
auto b = v.begin(); // ".begin()" returns an iterator that denotes the first element
auto e = v.end();   // ".end()" denotes a nonexistent element-"off the end" 
/*
1. if the container(vector) is empty, then ".begin()==.end()"
2. we don't care about the type that an iterator has, using "auto"
*/ 

/* Iterator operations */ 
*iter;	// return the element denoted by iterator-iter
iter->mem; // dereference iter and fetches the member-"mem" == (*iter).mem
++iter;	  // refer to next element
--iter;   // refer to previous element

/* Exp1 */
int main()
{
	string s("some string");  // C++ use "!=" instead of "<".
	for (auto it = s.begin(); it != s.end() && !isspace(*it); ++it)
		*it = toupper(*it); 
	cout << s << endl;  // Output: Some string
}

/*Exp2*/
int main()
{
	vector<int> text{1, 2, 3, 4, 5, 6, 7, 8, 9};
	int sought;
	cin >> sought;

	auto beg = text.begin(), end = text.end();
	// (end-begin) gives the distance between two iterators (+-)
	auto mid = text.begin() + (end - beg) / 2;
	
	// Binary Search - the text must be sorted
	while ((mid != end) && (*mid != sought)){
		if (sought < *mid)
			end = mid;
		else
			beg = mid + 1;
		mid = beg + (end - beg) / 2;
	}
	cout <<  "mid = " << *mid << endl;
}
```



## 3.5 Arrays

> 1. Array has fixed size. (Unlike *vector*) 
> 2. Cannot assign one array to another "=" ; 
> 3. There is **no** array of references.

### 3.5.1 Define and Initialize 

```c++
constexpr unsigned sz = 42; // variable[size] : size must be "constant expression" 
int *parr[sz];  // parr is an array of 42 pointers to int

int arr[5] = {0, 1, 2, 3, 4}; //array of 5 ints
int a1 = {1, 3, 1};      //a1 = {1, 3, 1, 0, 0}
string a2[] = {"Hello", "Wrold"};

char a3 = {'a', 'b', 'c'};
char a4 = "c++";   //a4 = {'c', '+', '+', '\0'}

	// 1. Complicated array declarations
// [Read from inside out] P_array points to an 'array of 10 ints'
int (*P_array)[10] = &arr;  
int (&arr_Ref)[10] = arr; //arrRef refers to an 'array of ten ints'
int *(&arry)[10] = ptrs;  // arry is a reference to an 'array of ten pointers'
```

### 3.5.2 Access the elements of an array

```c++
int main()
{
	unsigned scores[11] = {};
	unsigned grade;
	while (cin >> grade){
		if (grade <= 100)
			++scores[grade/10];
	}

	for (auto i : scores)
		cout << i << " ";
	cout << endl;
}
```

### Pointers and Arrays

> 指针和数组的联系非常紧密！

```c++
	// 1. equivalent to "*p = nums[0]"
string nums[] = {"one", "two", "three"};
string *p = nums; 
++p;  // 'p' points to nums[1]

	// 2. auto(array) returns a pointer [decltype(array) returns an array]
int ia[] = {0, 1, 2, 3, 4, 5};
auto ia2(ia);  // 'ia2' is an int* that points to the first element in 'ia'
	
	// 3. pointers can be used like iterators
/* Method I */
int main()
{
	int arr[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
	int *e = &arr[10];  //  "&arr[10]==v.end()"
	for (int *b = arr; b != e; ++b)  // "*b = arr ---> v.begin()"
		cout << *b << endl;
	return 0;
}

/* Method II "better!" */
using std::begin; 
using std::end;
int main()
{
	int arr[10] = {0, -1, 2, -3, 4, 5, 6, 7, 8, 9};
	int *p_beg = begin(arr);  // =="v.begin()"
	int *p_end = end(arr);    // =="v.end()"

	while(p_beg != p_end && *p_beg >= 0)
		++p_beg;
	cout << *p_beg << endl;
}

	// 4. Subscripts and Pointers
int ia[] = {0, 1, 2, 3, 4};
int *p = &ia[2];  // 'p' points to ia[2] will not change.
int j = p[1];  // =="*(p+1)", 'p[1]'points to 'ia[3]', but 'p' still points 'ia[2]'
int k = p[-2]; // =="*(p-2)", 'p[-2]' points to 'ia[0]'
```



## 3.6 Multidimensional Arrays

> Multidimensional arrays are actually **arrays of arrays.**

```c++
	// 1. Define and Initialize
int ia[3][4] = {
    {0, 1, 2, 3},
    {4, 5, 6, 7},
    {8, 9, 10, 11}
};

int ib[3][4] = {{1}, {2}, {3}};

	// 2. Exp 1
constexpr size_t rowCnt = 3, colCnt = 4;
int ia[rowCnt][colCnt]; 
for (size_t i = 0; i != rowCnt; i++)
    for (size_t j = 0; j != colCnt; j++)
        ia[i][j] = i * colCnt + j;

	// 3. Exp 2
int ia[3][4];
size_t cnt = 0;
for (auto &row : ia)
    for (auto &col : row){  // "row"!!
        col = cnt;
        cnt++;
    }
```



