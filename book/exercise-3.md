# 练习 3: 格式化输出 #

----------

使用`Makefile`文件能帮助你发现错误，当我们需要更多自动化功能的时候，我们将会添加`Makefile`文件。

语多编程语言使用类似C的方式格式化输出，那么让我们来试一试：
```
#include<stdio.h>

int main()
{
	int age = 10;
	int height = 72;
	
	printf("I am %d years old.\n", age);
	printf("I am %d inches tall.\n", height);
	
	return 0;
}
```

编写好以上代码后，使用`make ex3`命令去构建并运行。确保你已经修复了所有警告信息。

这个练习中，这些少量代码执行了很多操作，让我们来分解一下：
- 首页，你包含了另一个叫`stdio.h`的“头文件”。这告诉编译器你将使用“标准输入/输出函数”。其中一个就是`printf`。
- 然后你使用了一个叫`age`的变量，并为它赋值等于10。
- 接下来你使用了一个`height`变量，并赋值为72。
- 然后你使用`printf`函数去打印age和height。
- 在`printf`函数中你传递一个字符串参数，和其他许多编程语言一样，它是一个用来格式化的字符串。
- 在格式化字符串后，你使用一个变量用来替换`printf`函数中格式化字符串中的相应位置。

这样做的结果就是，你传递一些变量给`printf`函数，它会根据格式化字符串构建一个新的字符串，并把新字符串输出到终端。

# 显示结果 #

构建完整个程序，你应该能看到如下输出内容：
```
$ make ex3
cc -Wall -g    ex3.c   -o ex3
$ ./ex3
I am 10 years old.
I am 72 inches tall.
$
```

后面我将不会再告诉你如何去执行make命令，所以请确保你以上的程序都是正确的，并且能良好运行。

# 额外研究 #
在这里，原作者推荐你去研究`printf`函数的各种格化式的含义。比如`%s`,`%d`，以及精度，对齐等属性的使用。以及转义字符`\n`，`\t`。请自己研究相关文档。这里给出一个参考文档。http://man7.org/linux/man-pages/man3/printf.3.html

# 如何突破 #
尝试下面的方式去突然你的程序，这些操作可能会使你的程序崩溃，也许不会：

- 把`age`变量从第一个`printf`函数中移动，然后重新编译。你应该会得到一些警告信息。
- 运行新的程序，它或许会崩溃，或许会打印一个非常疯狂的年龄数字。
- 还原`printf`函数，然后不初始化`age`变量的值，然后重建编译运行。

```
# edit ex3.c to break printf
$ make ex3
cc -Wall -g    ex3.c   -o ex3
ex3.c: In function 'main':
ex3.c:8: warning: too few arguments for format
ex3.c:5: warning: unused variable 'age'
$ ./ex3
I am -919092456 years old.
I am 72 inches tall.
# edit ex3.c again to fix printf, but don't init age
$ make ex3
cc -Wall -g    ex3.c   -o ex3
ex3.c: In function 'main':
ex3.c:8: warning: 'age' is used uninitialized in this function
$ ./ex3
I am 0 years old.
I am 72 inches
```
# 补充内容 #
- 尽你的可能找到更多的方法去突破`ex3.c`
- 运行`man 3 printf`命令，阅读其他的`%`格化式字符。
- 添加`ex3`到你的`Makefile`的`all`列表。使用`make clean all`命令构建你所有的练习。
- 同样添加`ex3`到你`Makefile`的`clean`列表，然后使用`make clean`命令删除它。

