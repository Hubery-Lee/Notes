# C++与C的不同

[toc]

## 1.输入输出

### 1.1 C输入输出
- C中使用“stdio.h”标准输入输出库
- printf打印输出，scanf接受输入；
- getchar()输入单个字符

```c++
#include <stdio.h>

int main()
{
	int a;
	int b;

	printf("input a,b\n");
	scanf("%d,%d",&a,&b);
	printf("a=%d,b=%d\n",a,b);

	char ch1;
	printf("input ch1\n");
	ch1=getchar();
	putchar(getchar());
        printf("\n");	
	

	printf("input ch2\n");
	char ch2=getchar();
	printf("%c",getchar());

	//-----------
	//单独时可用
	// printf("\n");
	// char ch3;
	// printf("input ch3\n,");
	// scanf("%c",&ch3);
	// printf("ch3=%c\n",ch3);
	//----------------------

	//------------
	//字符串输入输出
	printf("\n");
	char s0[10];
	printf("input string\n");
	scanf("%s",s0);
	printf("%s",s0);

	char s1[]="array";
	char s2[6]="array";
	char *str = s1;
	printf("%s,%c\n",s1,s1[2]);
	printf("%s,%c\n",str,*(str+2));


	return 0;
}
```
### 1.2 C++输入输出

#### 1.2.1 cin/cout显示器输入/输出

- C++使用iostream
- 用标准命名空间，using namespace std;
- string 用于处理字符串；
- cin.get()和cin.getline()

`cin.get()读取会保留回车或换行，cin.getline()会丢弃换行或回车`
This is the code for reading a line into an array:
```c++
cin.getline(char*, 20);
```
This is the code for reading a line into a string object:
```c++
getline(cin,str);
```
```c++
cin >> str; // read a word into the str string object
```

```c++
#include "iostream"
#include "string"

using namespace std;
int main()
{
  double a,b;
  cout<<"input a,b"<<endl;
  cin>>a>>b;
  cout<<"a= "<<a<<",b= "<<b<<endl;

  char ch;
  cout<<"input ch"<<endl;
  cin>>ch;
  cout<<"ch= "<<ch<<endl;

  string str;
  cout<<"input string"<<endl;
  cin>>str;
  cout<<"str= "<<str<<endl;

}
```
```c++
#include "iostream"
#include "string"
const int Limit = 255;
int main()
{
  using std::cout;
  using std::cin;
  using std::endl;
  std::string str;
  cout << "Enter a string for getline() processing:\n";
  getline(cin,str,'#');
  cout << "Here is your input:\n";
  cout << str << "\nDone with phase 1\n";
  char ch;
  cin.get(ch);
  cout << "The next input character is " << ch << endl;
  
  char input[Limit];
  cout << "Enter a string for cin.getline() processing:\n";
  cin.getline(input, Limit, '#');
  cout << "Here is your input:\n";
  cout << input << "\nDone with phase 1\n";
  // char ch;
  cin.get(ch);
  cout << "The next input character is " << ch << endl;
  
  if (ch != '\n')
    cin.ignore(Limit, '\n'); // discard rest of line
  cout << "Enter a string for get() processing:\n";
  cin.get(input, Limit, '#');
  cout << "Here is your input:\n";
  cout << input << "\nDone with phase 2\n";
  cin.get(ch);
  cout << "The next input character is " << ch << endl;
  return 0;
}

// getline()函数为读完的将放到缓存中，结尾符号丢弃；cin>>类似
// cin.get()函数为读完的将放到缓存中，结尾符号也会保存到缓存中
```
![Alt](/home/hubery_lee/Pictures/Screenshot from 2020-03-04 23-28-14.png)

#### 1.2.3 C++字符串如何转换成C字符串

（1）strcpy()

```c++
#include "iostream"
#include "cstring" //c字符串函数头文件
#include "string"
using namespace std;

int main()
{
    string A="abcd";
    const char*a = A.c_str();//const char * 等价于string 而char *只能指向字符数组
    char ab[10]; //同理也可以使用
    char cd[10];
    // strcpy(a, A.c_str());
    strcpy(ab,A.c_str());
    strcpy(cd,A.data());
    cout << "a=" << a << endl
         << "ab=" << ab << endl;
    return 0;
}
```

（2）c_str()函数

```c++
#include<iostream>
#include<string>
using namespace std;
int main(){
    string str="Hello world.";
    const char * cstr=str.c_str();
    cout<<cstr<<endl;
    str="Abcd.";
    cout<<cstr<<endl;
    return 0;
}
```

(3) stringstream流用于类型转换

如果你打算在多次转换中使用同一个stringstream对象，记住再每次转换前要使用clear()方法；

```c++
    stringstream stream;
    int first, second;
 
    stream<< "456"; //插入字符串
    stream >> first; //转换成int
    cout << first << endl;
 
    stream.clear(); //在进行多次转换前，必须清除stream，否则第二个数据可能输出乱码
    
    stream << true; //插入bool值
    stream >> second; //提取出int
    cout << second << endl;
```



#### 1.2.3 输入输出格式

- 输入输出格式由ios_base类控制，具体设置有setf()方法实施

- setf()的格式控制如下表

  ![format](./images/Screenshot from 2020-03-04 23-41-13.png)

  ```
  ios_base::fmtflags orig = cout.setf(ios_base::fixed, ios_base::floatfield);
  std::streamsize prec = cout.precision(3);
  /////
  cout.setf(ios_base::hex, ios_base::basefield);
  ```

  ![](./images/Screenshot from 2020-03-04 23-44-58.png)

```c++
#include <iostream>
#include <cmath>
int main()
{
  using namespace std;
  // use left justification, show the plus sign, show trailing
  // zeros, with a precision of 3
  cout.setf(ios_base::left, ios_base::adjustfield);
  cout.setf(ios_base::showpos);
  cout.setf(ios_base::showpoint);
  cout.precision(3);
  // use e-notation and save old format setting
  ios_base::fmtflags old = cout.setf(ios_base::scientific,
				     ios_base::floatfield);
  cout << "Left Justification:\n";
  long n;
  for (n = 1; n <= 41; n+= 10)
    {
      cout.width(4);
      cout << n << "|";
      cout.width(12);
      cout << sqrt(double(n)) << "|\n";
    }
  // change to internal justification
  cout.setf(ios_base::internal, ios_base::adjustfield);
  // restore default floating-point display style
  cout.setf(old, ios_base::floatfield);  //============
  cout << "Internal Justification:\n";
  for (n = 1; n <= 41; n+= 10)
    {cout.width(4);
      cout << n << "|";
      cout.width(12);
      cout << sqrt(double(n)) << "|\n";
    }
  // use right justification, fixed notation
  cout.setf(ios_base::right, ios_base::adjustfield);
  cout.setf(ios_base::fixed, ios_base::floatfield);
  cout << "Right Justification:\n";
  for (n = 1; n <= 41; n+= 10)
    {
      cout.width(4);
      cout << n << "|";
      cout.width(12);
      cout << sqrt(double(n)) << "|\n";
    }
  return 0;
}
```

![运行结果](./images/Screenshot from 2020-03-04 23-55-48.png)

#### 1.2.4 文件输入输出

- 使用fstream 头文件

- ifstream 文件输入，ofstream 文件输出

```c++
#include <iostream> // not needed for many systems
#include <fstream>
#include <string>
int main()
{
  using namespace std;
  string filename;
  cout << "Enter name for new file: ";
  cin >> filename;
  // create output stream object for new file and call it fout
  ofstream fout(filename.c_str());
  fout << "For your eyes only!\n";
  // write to file
  cout << "Enter your secret number: ";
  // write to screen
  float secret;
  cin >> secret;
  fout << "Your secret number is " << secret << endl;
  fout.close();
  // close file
  // create input stream object for new file and call it fin
  ifstream fin(filename.c_str());
  cout << "Here are the contents of " << filename << ":\n";
  char ch;
  while (fin.get(ch))
    // read character from file and
    cout << ch;
  // write it to screen
  cout << "Done\n";
  fin.close();
  return 0;
}
```
判断文件能否打开的条件
```c++
//c++11新版本 is_open()
if (!fin.is_open())// open attempt failed
{
...
}
//老版本
fin.open(argv[file]);
if (fin.fail()) // open attempt failed
{
...
}
if (!fin) // open attempt failed
{
...
}
if(!fin.good()) ... // failed to open
```

多个文件读取

```c++
ifstream fin;				//create stream using default constructor
fin.open("fat.txt");		//associate stream with fat.txt file
...							//do stuff
fin.close();				//terminate association with fat.txt
fin.clear();				//reset fin (may not be needed)
fin.open("rat.txt");		//associate stream with rat.txt file
...
fin.close();
```



文件的读写权限
![](./images/Screenshot from 2020-03-05 00-22-25.png)

```c++
#include <iostream>
#include <fstream>
#include <string>
#include <cstdlib>
// (for exit()
const char * file = "guests.txt";
int main()
{
  using namespace std;
  char ch;
  // show initial contents
  ifstream fin;
  fin.open(file);
  if (fin.is_open())
    {
      cout << "Here are the current contents of the "
	   << file << " file:\n";
      while (fin.get(ch))
	cout << ch;
      fin.close();
    }
  // add new names
  ofstream fout(file, ios::out | ios::app);
  if (!fout.is_open())
    {
      cerr << "Can't open " << file << " file for output.\n";
      exit(EXIT_FAILURE);
    }
  cout << "Enter guest names (enter a blank line to quit):\n";
  string name;
  while (getline(cin,name) && name.size() > 0)
    {
      fout << name << endl;
    }
  fout.close();
  // show revised file
  fin.clear();
  // not necessary for some compilers
  fin.open(file);
  if (fin.is_open())
    {
      cout << "Here are the new contents of the "
	   << file << " file:\n";
      while (fin.get(ch))
	cout << ch;
      fin.close();
    }
  cout << "Done.\n";
  return 0;
}
```

## 2.for 循环

### 2.1 C++ 11普通for循环

```c++
#include "iostream"
using namespace std;

int main()
{

  //针对c++11，c++98暂不支持
  double prices[5] = {4.99, 10.99, 6.87, 7.99, 8.49};
  for (double x : prices)
    cout<<x<<" ";
   cout<<endl;
    
  for (int i=0;i<5;i++)
      cout<<prices[i]<<" ";
    cout<<endl;
}
```

### 2.2 C++11容器类中迭代器

迭代器循环

```c++
vector<int>::iterator pr;
for(pr=a.begin();pr!=a.end();pr++)
    cout<<*pr<<" ";
        
for_each(a.begin(),a.end(),[](int n){cout<<n<<" ";});   //需要包含algorithm头文件

#include <iterator>
...
vector<int> dice;
ostream_iterator<int, char> out_iter(cout, " ");
copy(dice.begin(), dice.end(), out_iter);	// copy vector to output stream
        
```

用例：

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm> //for for_each(),sort()...
using namespace std;
void Show(const int &b)
{cout<<b<<" ";}
int main()
{
	vector<int> a;
    int b;
    while(cin>>b)
        a.push_back(b);
    cout<<"case 1:"<<endl;
    vector<int>::iterator pr;
    for(pr=a.begin();pr!=a.end();pr++)
        cout<<*pr<<" ";
    cout<<endl;
    
    cout<<"case 2:"<<endl;
	for_each(a.begin(),a.end(),Show);
    cout<<endl;

    cout<<"case 3:"<<endl;
    for_each(a.begin(),a.end(),[](int n){cout<<n<<" ";});
    cout<<endl;
    
    return 0;
}
```

```c++
#include <iostream>
#include <iterator>
#include <vector>
int main()
{
    using namespace std;
    int casts[10] = {6, 7, 2, 9 ,4 , 11, 8, 7, 10, 5};
    vector<int> dice(10);
    // copy from array to vector
    copy(casts, casts + 10, dice.begin());
    cout << "Let the dice be cast!\n";
    // create an ostream iterator
    ostream_iterator<int, char> out_iter(cout, " ");
    // copy from vector to output
    copy(dice.begin(), dice.end(), out_iter);
    cout << endl;
    cout <<"Implicit use of reverse iterator.\n";
    copy(dice.rbegin(), dice.rend(), out_iter);
    cout << endl;
    cout <<"Explicit use of reverse iterator.\n";
    vector<int>::reverse_iterator ri;
    for (ri = dice.rbegin(); ri != dice.rend(); ++ri)
    cout << *ri << ' ';
    cout << endl;
}
```

## 3. 类

### 3.1 类的继承、抽象、封装与多态
- 继承：面向对象程序设计中最重要的一个概念是继承。继承允许我们依据另一个类来定义一个类，这使得创建和维护一个应用程序变得更容易。这样做，也达到了重用代码功能和提高执行效率的效果。
- 多态：多态意味着调用成员函数时，会根据调用函数的对象的类型来执行不同的函数。
- 抽象：数据抽象是一种仅向用户暴露接口而把具体的实现细节隐藏起来的机制。
- 封装：数据封装是一种把数据和操作数据的函数捆绑在一起的机制。

### 3.2 虚函数与纯虚函数

纯虚函数是针对抽象基类。类申明中包含纯虚函数则不能创建该类对象。如求椭圆与圆类的面积实现，可定义一个抽象类，利用抽象基类指针数组同时管理，椭圆和圆类。


### 3.3 友元

获取友元类的类的私有成员

### 3.4 泛型编程

所谓泛型编程目的就是将数据和算法分离，使算法不依赖数据类型。其中的典型就是模板函数/模板类；泛型编程还涉及到代码的重用；

`iterator 指针在泛型编程用的比较广泛，比如copy(),sort(),unique(),end(),front()...`

```c++
// inserts.cpp -- copy() and insert iterators
#include <iostream>
#include <string>
#include <iterator>
#include <vector>
#include <algorithm>
void output(const std::string & s) {std::cout << s << " ";}
int main()
{
    using namespace std;
    string s1[4] = {"fine", "fish", "fashion", "fate"};
    string s2[2] = {"busy", "bats"};
    string s3[2] = {"silly", "singers"};
    vector<string> words(4);
    copy(s1, s1 + 4, words.begin());
    for_each(words.begin(), words.end(), output);
    cout << endl;
    // construct anonymous back_insert_iterator object
    copy(s2, s2 + 2, back_insert_iterator<vector<string> >(words));
    for_each(words.begin(), words.end(), output);
    cout << endl;
    // construct anonymous insert_iterator object
    copy(s3, s3 + 2, insert_iterator<vector<string> >(words,
    words.begin()));
    for_each(words.begin(), words.end(), output);
    cout << endl;
    return 0;
}
```

#### 3.4.1.模板函数

```c++
template <class AnyType>
void Swap(AnyType &a, AnyType &b)
{
    AnyType temp;
    temp = a;
    a = b;
    b = temp;
}
```

用列：

```c++
#include <iostream>
// function template prototype
template <typename T> // or class T
void Swap(T &a, T &b);
int main()
{
	using namespace std;
    int i = 10;
    int j = 20;
    cout << "i, j = " << i << ", " << j << ".\n";
    cout << "Using compiler-generated int swapper:\n";
    Swap(i,j); // generates void Swap(int &, int &)
    cout << "Now i, j = " << i << ", " << j << ".\n";
    double x = 24.5;
    double y = 81.7;
    cout << "x, y = " << x << ", " << y << ".\n";
    cout << "Using compiler-generated double swapper:\n";
    Swap(x,y); // generates void Swap(double &, double &)
    cout << "Now x, y = " << x << ", " << y << ".\n";
    // cin.get();
    return 0;
}
// function template definition
template <typename T> // or class T
void Swap(T &a, T &b)
{
    T temp;
    // temp a variable of type T
    temp = a;
    a = b;
    b = temp;
}
```

#### 2.模板类

`最典型的应用就是标准模板库里的vector,queue,list,map ,set...`

```c++
// stcktp1.h -- modified Stack template
#ifndef STCKTP1_H_
#define STCKTP1_H_
template <class Type>
class Stack
{
private:
	enum {SIZE = 10};	// default size
	int stacksize;
	Type * items;		// holds stack items
	int top;			// index for top stack item
public:
    explicit Stack(int ss = SIZE);
    Stack(const Stack & st);
    ~Stack() { delete [] items; }
    bool isempty() { return top == 0; }
    bool isfull() { return top == stacksize; }
    bool push(const Type & item);	// add item to stack
    bool pop(Type & item);			// pop top into item
    Stack & operator=(const Stack & st);
};
template <class Type>
Stack<Type>::Stack(int ss) : stacksize(ss), top(0)
{
	items = new Type [stacksize];
}
template <class Type>
Stack<Type>::Stack(const Stack & st)
{
    stacksize = st.stacksize;
    top = st.top;
    items = new Type [stacksize];
    for (int i = 0; i < top; i++)
   	 items[i] = st.items[i];
}
template <class Type>
bool Stack<Type>::push(const Type & item)
{
    if (top < stacksize)
    {
        items[top++] = item;
        return true;
    }
    else
    	return false;
}
template <class Type>
bool Stack<Type>::pop(Type & item)
{
    if (top > 0)
    {
        item = items[--top];
        return true;
    }
    else
        return false;
}
template <class Type>
Stack<Type> & Stack<Type>::operator=(const Stack<Type> & st)
{
    if (this == &st)
    return *this;
    delete [] items;
    stacksize = st.stacksize;
    top = st.top;
    items = new Type [stacksize];
    for (int i = 0; i < top; i++)
    	items[i] = st.items[i];
    return *this;
}
#endif
```

```c++
// stkoptr1.cpp -- testing stack of pointers
#include <iostream>
#include <cstdlib>
// for rand(), srand()
#include <ctime>
// for time()
#include "stcktp1.h"
const int Num = 10;
int main()
{
    std::srand(std::time(0)); // randomize rand()
    std::cout << "Please enter stack size: ";
    int stacksize;
    std::cin >> stacksize;// create an empty stack with stacksize slots
    Stack<const char *> st(stacksize);
    
    // in basket
    const char *in[Num] = {
    " 1: Hank Gilgamesh", " 2: Kiki Ishtar",
    " 3: Betty Rocker", " 4: Ian Flagranti",
    " 5: Wolfgang Kibble", " 6: Portia Koop",
    " 7: Joy Almondo", " 8: Xaverie Paprika",
    " 9: Juan Moore", "10: Misha Mache"
     };
    
    // out basket
    const char * out[Num];
    int processed = 0;
    int nextin = 0;
    while (processed < Num)
    {
        if (st.isempty())
        st.push(in[nextin++]);
        else if (st.isfull())
        st.pop(out[processed++]);
        else if (std::rand() % 2 && nextin < Num)
        st.push(in[nextin++]);
        else
        st.pop(out[processed++]);// 50-50 chance
    }
    for (int i = 0; i < Num; i++)
        std::cout << out[i] << std::endl;
    std::cout << "Bye\n";
    return 0;
}
```



```c++
//arraytp.h -- Array Template
#ifndef ARRAYTP_H_
#define ARRAYTP_H_
#include <iostream>
#include <cstdlib>
template <class T, int n>
class ArrayTP
{
private:
    T ar[n];
public:
    ArrayTP() {};
    explicit ArrayTP(const T & v);
    virtual T & operator[](int i);
    virtual T operator[](int i) const;
};
template <class T, int n>
ArrayTP<T,n>::ArrayTP(const T & v)
{
    for (int i = 0; i < n; i++)
        ar[i] = v;	
}
template <class T, int n>
T & ArrayTP<T,n>::operator[](int i)
{
    if (i < 0 || i >= n)
    {
    std::cerr << "Error in array limits: " << i
    << " is out of range\n";
    std::exit(EXIT_FAILURE);
    }
    return ar[i];
}
template <class T, int n>
T ArrayTP<T,n>::operator[](int i) const
{
    if (i < 0 || i >= n)
    {
    std::cerr << "Error in array limits: " << i
    << " is out of range\n";
    std::exit(EXIT_FAILURE);
    }
    return ar[i];
    }
#endif
```

```c++
#include <iostream>
#include "arraytp.h"
int main(void)
{
    using std::cout;
    using std::endl;
    ArrayTP<int, 10> sums;
    ArrayTP<double, 10> aves;
    ArrayTP< ArrayTP<int,5>, 10> twodee;
    int i, j;
    for (i = 0; i < 10; i++)
    {
        sums[i] = 0;
        for (j = 0; j < 5; j++)
    	{
    		twodee[i][j] = (i + 1) * (j + 1);
    		sums[i] += twodee[i][j];
    	}
    	aves[i] = (double) sums[i] / 10;
    }
    for (i = 0; i < 10; i++)
    {
        for (j = 0; j < 5; j++)
        {
        cout.width(2);
        cout << twodee[i][j] << ' ';
        }
        cout << ": sum = ";
        cout.width(3);
        cout << sums[i] << ", average = " << aves[i] << endl;
    }
    cout << "Done.\n";
    return 0;
}
```

![输出结果](./images/Screenshot from 2020-03-05 09-35-01.png)

```c++
#include <iostream>
using std::cout;
using std::endl;
template <typename T>
class HasFriend
{
private:
	T item;
	static int ct;
public:
	HasFriend(const T & i) : item(i) {ct++;}
	~HasFriend() {ct--; }
	friend void counts();
	friend void reports(HasFriend<T> &); // template parameter
};
// each specialization has its own static data member
template <typename T>
int HasFriend<T>::ct = 0;
// non-template friend to all HasFriend<T> classes
void counts()
{
    cout << "int count: " << HasFriend<int>::ct << "; ";
    cout << "double count: " << HasFriend<double>::ct << endl;
}
// non-template friend to the HasFriend<int> class
void reports(HasFriend<int> & hf)
{
	cout <<"HasFriend<int>: " << hf.item << endl;
}
// non-template friend to the HasFriend<double> class
void reports(HasFriend<double> & hf)
{
	cout <<"HasFriend<double>: " << hf.item << endl;
}
int main()
{
    cout << "No objects declared: ";
    counts();
    HasFriend<int> hfi1(10);
    cout << "After hfi1 declared: ";
    counts();
    HasFriend<int> hfi2(20);
    cout << "After hfi2 declared: ";
    counts();
    HasFriend<double> hfdb(10.5);
    cout << "After hfdb declared: ";
    counts();
    reports(hfi1);
    reports(hfi2);
    reports(hfdb);
    return 0;
}
```

