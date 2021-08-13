# cpp learning
## C语言特点
结构化编程（structured programming），结构化编程将分支限制为一小组行为良好的结构。 另一个原则则是自上而下（top-down），将大型程序分解为小型、便于管理的任务
## 面向对象编程（OOP）
C++是一种面向对象编程的语言，类（class）是一种规范，描述了一种新型数据格式，对象是根据这种规范构造的特定数据结构
OOP程序设计首先设计类（数据和方法合并）。从低级组织（class）到高级组织（program）的处理过程叫做（bottom-up）的编程
## 泛型编程（generic programming）
泛型编程是C++支持的另一编程模式。OOP强调数据，泛型编程强调独立于特定数据类型。 generic指的是创建独立于类型的代码
## C++预处理器和iostream文件
C++和C一样使用一个预处理器，处理以#开头指令（头文件)
```
#include <iostream>
```
C++的输入/输出方案依赖iostream文件中的多个定义
## 名称空间
名称空间支持是一种C++特性，让厂商能够将产品封装在一个叫做名称空间的单元中
```
using std::cout; //make cout available
using namespace std; // lazy approach, all names in std available
```
## 从cout初识c++面向对象特性
与c语言的printf(）相比，cout不需要输入cout<<something; 中something的具体类型，可以自动识别和显示所开发的新数据类型。
## C++变量类型
+ short/int/long/long long/unsigned *  __c++中，如果整形外溢，则会溢出到范围的另一端。__
+ char是比short更小的一类整形，cin和cout会根据变量的声明来自行判断输出的是字符还是整形。
+ cout.put()为cout类的一个成员函数，功能为显示一个字符
+ char在默认下既不是没有符号也不是有符号，根据需要自己定义signed char/unsigned char
+ 需要处理的字符串无法用一个8位字节来表示时，有另外一个类型wcha_t（宽字符类型）表示拓展字符集。cin/cout无法处理wcha_t，需要iostream中另外的新工具wcin/wcout
+ C++ 11新增的类型： char16_t, char32_t，均无符号
+ bool类型： true/false
## const限定符
```
const int Month = 12; //Month is a symbolic constant for 12
```
+ const是一个限定符，限定了变量的类型和含义，一旦初始化后无法更改。
+ const比C中#define 语句更好， 明确指定类型， 可以用C++的作用域规则限定在特定的函数或者文件中，且可以用于更复杂的结构
## 浮点数

一部分表示数，一部分表示缩放因子。
两种表示方法：8.00    8e-2/8E+3
三类： float, double, long double，  希望浮点类型为float， 通常后面+f/F， 为long double， +l/L

## 类型转换

+ 赋值时会自动进行转换。比如：

```
so_long = thirty; // assigning a short to long
```

此时会自动将thirty的值变成long传给so_long， thirty的内容不变。
这样会造成把一个小范围的值给一个大范围的值的时候，只是占用的字节变大，但是把一个大范围的赋值给小范围，可能出现问题，会造成误差

+ 以{}方式进行转换

c++11 将使用{}的初始化称为列表初始化（list initialization）,用于给复杂的数据类型提供值列表，对类型转化更严格，不允许narrowing

```
char c1 {31325}; //narrowing, not allowed
char c2 = {66}; //allowed, char can hold 66
```

+ 表达式中的转换
+ 传递参数时转换
+ 强制类型转换
```
float x = 1.0;
(int) x; //coming from c
int(x); //c++
```

## auto字符
auto是一个c语言关键字，但很少使用。如果使用关键词auto，不指定变量的类型。编译器会把变量类型变成其初始值相同。
``` 
auto x = 100; // x is int
```

## 数组
声明数组需要三点：
+ 元素中值的类型
+ 数组名
+ 元素个数
```
short months[12]; // creates array of 12 short
```
注意一些定义细节：
+ 只有在定义数组时才能初始化
```
int cards[4] = {3, 4, 5, 6}; // allowed
int cards[4];
cards[4] = {3, 4, 5, 6}; // not allowed
```
+ 如果只对数组一部分初始化，编译器会将其他元素设置为0
```
int zeros[500] = {0}; // a array of zeros
```
+ 如果初始化时[]内为空，则编译器将计算元素个数
```
short a[]={1, 2}; // a has 2 elements
```
### C++11 数组初始化方法
使用{}的初始化
```
double earnings[4] {1.2e4, 1.6e4, 1.1e4};
float blance[100] {}; // all elements set to 0
```

## 字符串
+ C-style 字符串， 以空字符\0结尾， 不是以空字符\0结尾的不是字符串， 是字符数组
+ 字符串常量（string constant）， 使用双引号， 并隐式地包括了结尾的空字符   注意赋值时双引号包括的字符串表示的是字符串所在的内存地址

## 在数组中使用字符串
标准头文件cstring提供了很多实用的函数。 注意sizeof(）指出整个数组的长度（包含空字符）， strlen()只计算可见的字符（忽略空字符） 所以将字符串输入到数组时，数组长度至少为strlen(example）+1

## 字符串输入
+ 面向行的输入： getline()
cin.getline(name, size)有2个参数， 第一个参数用来存储输入行的数组的名称，第二个参数是要读取的字符数。 
getline()成员函数在读取指定数目的字符或遇到换行符时停止读取，但不保存换行符，将换行符换成空字符
+ 另一面向行的输入： get()
cin.get(name, size)与getline()不同在于，get并不再读取并丢弃换行符，而是留在输入队列中。这带来了一个问题是再次调用get()函数时由于换行符在输入队列之首，于是无法发现新的可读取的内容。
使用另外一种变体来解决这个问题：
```
cin.get(name1, size); // read first line
cin.get(); // read newline
cin.get(name2, size); // read second line
```
or
```
cin.get(name, size).get(); //concatenate member functions 直接读完第一行，getline()可用同种拼接方式连续读2行内容
```
## 空行和其他输入问题
需要注意getilne()和get()可能遇到读取空行，或者输入的字符串比分配的空间长。 get()读取空行后会设置失效位，getline()在输入大于分配空间会设置失效位。 cin.clear()可以恢复并继续输出。

## 混合输入字符串和数字
先用cin读取数字的话，回车产生的换行符可能留在输入队列导致cin.getline()认为后续输出为空行。应该先读取并丢弃换行符。
```
cin >> year;
cin.get(); // or (cin >> year).get();
```

## string类
string允许c-风格初始化，也可以c++11字符串初始化
```
string str1;  //create an empty string
string str2 = "partner";
string str3 {“The book”};
```
string 允许cin输入，cout显示，可以使用数组表示法访问string对象中的字符

string赋值、拼接和附加

数组无法直接赋值，需要用strcpy()方法，但是string可以直接赋值
```
str1 = str2; // allowed for string
```

string可以直接用加法拼接， 数组需要用strcat()
```
string str3;
str3 = str1 + str2; //allowed
str1 += str2; //allowed 
```

string的其他操作
```
strcpy(charr1, charr2); //copy charr2 to charr1
strcat(charr1, charr2); //append contents of charr2 to charr1
strlen(str1); //length of str1, excluding the '\n'
charr1.size(); //length of charr1, including the '\n'
```
string类I/O
```
getline(cin, str); //set next line as input to str
```

## struct
```
struct inflatable {
    char name[20];
    float volume;
    double price;
};
inflatable guest {
    "basketball",
    1.88,
    29.9
};
```
结构数组：
生成一个inflatable数组，里面每个元素都是一个inflatable对象
```
inflatable gifts[100];
cin >> gifts[0].name;
cout << gifts[0].name;
```
结构可以指定结构成员的占用字段
```
struct torgle_register {
    unsigned int SN : 4; //4 bits for SN value
    unsigned int : 4; //4 bits unused
    bool goodIn : 1; //valid input (1 bit)
    bool goodTorgle :1; 
};
```

## union
共用体是一种数据格式， 能够存储不同的数据类型，但只能同事存储其中一种类型。 比如， 一个产品的id可能是int也可能是char， 这个时候可以用union。 可以和struct混用
```
struct widget {
    char brand[20];
    int type;
    union id  //format depends on widget type
    {
      long id_num; // type1 widgets
      char id_char[20]; //other widgets
    } id_val;   // id_val 是union id的中间标志符， 可以没有 ，如果没有id_val， 则共用体为匿名共用体， id_num和id_char为prize的2个成员， 但位于相同地址， 因此只能有一个为当前成员
};
...
widget prize;
...
if (prize.type == 1)
  cin >> prize.id_val.id_num;
else
  cin >> prize.id_val.id_char;
```

## enum
c++的enum工具提供了另一种创建符号常量的方式， 可以代替const，允许定义新类型, 但必须按照严格限制
```
enum spectrum {red, orange, yellow, green, blue, violet, indigo, ultraviolet}；
```
一般enum成员值默认为从0开始依次+1的整数， 也可以用赋值语句在定义时显示表示，但必须是整数

## pointer
初始化和赋值
```
int * p; //initializaztion
int * p1, p2; // p1 is a pointer, p2 is an int
int * p3 = &p2; // initialize a pointer p3 and assign it to p2
p = &p2; 
```
指针的危险
在指针应用解锁应用运算符* 前， 要将指针初始化为一个确定的、适当的地址。 不然随意给* p赋值， 可能让* p指向一个危险的地址

指针和数字
指针不是整形， 但计算机经常讲指针当做整形吹了。 如果要给指针一个整形地址， 要加 (int * )
```
int * pt;
pt = (int *) 0xB8000000;
```
## new 创建动态数组
```
int * p = new int[10]; // create a block of 10 ints
p = p + 1; //动态数组和数组， 数组名不能运算 ，但指针可以运算， 指针指这个动态数组的初位置， 这里+ 1 指向下一个位置
delete [] p;
```
使用new和delete时，注意以下规则：
+ 不要用delete释放不是new分配的内存
+ 不要用delete释放同一个内存块2次
+ 使用new [] 分配的内存用 delete [] 释放
+ 对空指针用delete安全

## 指针算数
指针变量+1， 增加的量等于它指向的类型的字节数。  自然， 对于一个数组指针， 数组指针+1表示它增加一个指向类型的字节， 自然等价于指向下一个地址
* (p + 1) 等价于 p[1]

## new 创建动态结构
```
inflatable * ps = new inflatable;
```
注意，指针访问内部成员的运算符时->， 结构访问内部成员的运算符是.
```
ps->price; //ps指向的结构的price成员
(*ps).price; //*ps等价于指向的结构
```

## 自动存储、静态存储和动态存储
+ 自动存储
函数内部定义的常规变量使用自动存储空间。 所属的函数被调用时自动产生， 函数结束时消亡
自动变量通常存储在栈中， 遵循（LIFO）
+ 静态存储
整个程序执行期间都存在的存储方式。 使变量成为金泰的方式有2种， 第一种是在函数外面定义， 另一种是声明时加上关键词static
+ 动态存储
new/delete 提供的更灵活的控制内存方法， 管理了一个内存池， 在c++种称为free store or heap. 
在栈中， 自动添加和删除机制使得占用的内存总是连续的， 但new和delete的相互影响可能导致占用的free store不连续， 使得跟踪新分配内存的位置更困难

## 内存泄露
new在free store上创建变量后没有delete， 那么即使包含指针的内存由于作用于规则和对象生命周期的原因而被释放， 在free store上动态分配的变量或结构将继续存在。 
将会无法访问free store中的这些结构， 这将导致内存泄漏。被泄露的内存在程序的整个生命周期中都不可使用，被分配出去但无法回收。

## vector
vector是一种动态数组，使用new创建的动态数组的替代品。vector类使用new/delete管理内存，但这个工作自动完成.
```
#include <vector>
using namespace std;
// vector<typeName> vt(n_elem);
vector<int> vi; //create a zero-size array of int
int n;
cin >> n;
vector<double> vd(n); //create a double array of size n 
```
## array
vector类的功能比数组强大，但效率略低。如果需要的时固定长度的数组，使用数组时更加的选择。array类位于std中，对象的长度固定，使用栈分配内存，因此效率于数组相同，更方便更安全。
```
include <array>
using namespace std;

// array<typeName, n_elem> arr;
array<int, 5> ai; //create array object of 5 ints
array<double, 4> ad1 = {1.2, 2.1, 3.4, 5};
array<double, 4> ad2;
ad2 = ad1 //allowed for same-size array, not allowed for char[]
 ```
