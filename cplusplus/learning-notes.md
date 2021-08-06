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

