# Learn-CPP
## 第七章
1. C++的函数返回值类型不能是数组，但可以是其他任何类型：整数、浮点数、指针、结构、对象等。<br>
	`C++不能返回数组但是可以将数组作为结构或对象的组成部分来返回`
2. C++函数三要素：函数定义、函数原型、函数调用。规范的写法应该是prototype写在前面然后main函数最后才定义函数内容。C++的风格是将main函数放在最前面，因为它定义了程序的整体结构
```cpp
double cude(double x);  //prototype: returns a double
double cude(double);    //okay to drop variable name in prototype, 原型中的变量名相当于占位符，因此不必与函数定义中的变量名相同
```
3. 输出多个文件且文件名中有变量的写法：
```cpp
char buf[30] = "";
sprintf_s(buf, "./Result/BoxPosition_%d.txt", cnt+1);
ofstream output;
output.open(buf);
output << "..." << endl;
output.close();
```
4. argument(实参)、parameter(形参)
5. 读取字符：
```cpp
cin>>ch;        //读取的字符跳过空格和换行符
cin.get(ch);    //等价于ch=cin.get()，cin.get()函数会读取所有的输入字符，包括空格和换行符
```
6. 交替进行乘除运算的策略可以防中间结果超过最大的浮点数：(10/2)×(9/1) better than (10×9)/(2×1)
7. 如果已知变量为正整数，就可以声明为unsigned
8. 输入字符退出循环的简洁写法：
```cpp
cout<<"Enter q to quit"
while(cin>>number>>picks)
{...}
```
9. 将数组作为函数参数：
```cpp
int sum_arr(int arr[], int n);	//arr is array name, n is size
```
10. 将数组类型和元素数量告诉数组处理函数，要通过两个参数传递而不要用方括号表示法来传递数组长度：
```cpp
void fillArray(int arr[], int size);	//prototype
void fillArray(int arr[size]);		//bad prototype
```
11. 以下函数原型并不意味着传入函数的原始数组必须是常量，只是意味着不能在show_array()函数中使用ar来修改这些数据。因此show_array()将数组视为只读数据
```cpp
void show_array(const double ar[], int n);
```
12. 处理非法输入的简便方法：
```cpp
cout << "Enter revalue factor: ";
double factor;
while (!(cin >> factor))
{
cin.clear();				//clear()可以清除buffer中的数据
while (cin.get() != '\n') continue;	//get()读取单个字符
cout << "Bad input, please reinput: ";
}
cout << factor << endl;
```
13. 两种方式将const用于指针：<br>
一是让指针指向一个常量对象，可以保证指针指向的值不会被修改；二是将指针本身声明为常量，可以防止改变指针指向的位置。
```cpp
//第一种，声明一个指向常量的指针pt
int age=30;
const int *pt=&age;
//这里pt指向一个const int(此处为30)，因此不能用pt来修改这个值，即*pt的值为const，不能被修改
//这种方式的pt声明并不意味着它指向的值实际上就是一个常量，只是意味着对pt而言这个值是常量。例如pt指向age而age不是const
//可以直接通过age变量来修改age的值但不能使用pt指针来修改它：
*pt=20;	//INVALID because pt points to a const int
age=20;	//VALID because age is not declared to be const
```
还有另外两种赋值可能：将const变量的地址赋值给const的指针、将const的地址赋给常规指针。但第一种可行第二种不可行：
```cpp
const float g_earch=9.8;
const float *pe=&g_earch;	//VALID

const float g_moon=1.63;
float *pm=&g_moon;		//INVALID
```
第二种情况非法的原因是：如果将g_moon的地址赋值给pm，则可以使用pm来修改g_moon的值，就使得g_moon的const状态会发生冲突，因此C++禁止将const变量赋值给非const指针。如果非要这样做，可以用强制类型装换来const_cast来突破限制
