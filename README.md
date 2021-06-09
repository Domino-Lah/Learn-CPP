# Learn-CPP
## 第七章
1. C++的函数返回值类型不能是数组，但可以是其他任何类型：整数、浮点数、指针、结构、对象等。<br>
	`C++不能返回数组但是可以将数组作为结构或对象的组成部分来返回`
2. C++函数三要素：函数定义、函数原型、函数调用。规范的写法应该是prototype写在前面然后main函数最后才定义函数内容<br>
	`C++的风格是将main函数放在最前面，因为它定义了程序的整体结构`
3. 输出多个文件且文件名中有变量的写法：
```cpp
char buf[30] = "";
sprintf_s(buf, "./Result/BoxPosition_%d.txt", cnt+1);
ofstream output;
output.open(buf);
output << "..." << endl;
output.close();
```
