### 最近开发中遇到的比较难的问题

#### 内存溢出

##### 缓冲区溢出

C/C++标准库有个strcpy，会一直复制内存，直到遇到\0。

```cpp
const int MAX_LENGTH = 16;
bool is_administrator = false;
char destination[MAX_LENGTH];

std::string source = read_string_from_client();
strcpy(destination, source.c_str());
```

如果构造一个source大于16字节，就会修改到destination之外的内存。很多平台的栈变量是跟按地址顺序倒着分配的。所以destination溢出以后会修改先前定义的变量。比如把is_administrator修改成true。

##### 栈溢出

栈的空间一般都比较小，Linux下可以用命令`ulimit -a`查询栈大小，一般默认为8M

```c
int length = read_int_from_client();
char buffer[length];
int data = read_int_from_client();
```

如果黑客给一个超大的length，buffer就会占用巨大的空间，这个时候，data就被定义到栈外了，如果编译器没有做代码越界检查的话，通过输入不同的length和data可以修改任意内存。

另外迭代也会造成栈溢出，迭代多少次，函数中申请的变量就会重复加入栈中多少次。

#### 内存泄漏

### 智能指针

### vector的扩容方式

### C++设计模式

### GDB调试