# 练习1：重温编译器 #

----------
下面是第一个简单的C程序：
```
int main(int argc, char *argv[])
{
    puts("Hello world.");

    return 0;
}
```
把上面的代码保存到ex1.c文件中，然后输入如下命令：
```
$ make ex1
cc     ex1.c   -o ex1
```
你的电脑也许使用细微不同的命令，但最终结果应该是生成一个名为`ex1`的可执行文件。

# 显示结果 #
你现在可以运行程序并且观察输出。
```
$ ./ex1 
Hello world.
```
如果你没有得到如上输出，返回去修复程序。

# 如何突破 #
在这本书中，我将会用一个小段落去研究如何突破每一个程序。我会让你对这个程序做奇怪的事情，用奇怪的方式运行它们，或者改变代码，这样你就能看到崩溃和编译器错误。
对于上面的程序，设置编译器显示所有警告并重新构建它：
```
$ rm ex1
$ CFLAGS="-Wall" make ex1
cc -Wall    ex1.c   -o ex1
ex1.c: In function ‘main’:
ex1.c:3: warning: implicit declaration of function ‘puts’

$ ./ex1 
Hello world.
```
现在你得到一个警告说函数“puts”是隐式定义的。C编译器是非常智能的，它能知道你想要的，但是你也应该尽可能解决编译器警告。解决上述警告的方法就是在`ex1.c`文件第一行加上如下代码并重新编译：
```
#include<stdio.h>
```
然后像之前一样重新编译，你会发现警告消失了。

# 补充内容 #

- 用文本编辑器打开`ex1`文件，随意修改或者删除一些内容，尝试运行看看会发生什么。
- 修改hello world程序，多打印5行文本或者其他更复杂的内容。
- 运行`man 3 puts`并阅读这个函数的手册和更多的内容。

# 译者补充 #
fputc, fputs, putc, putchar, puts
以上这些函数用来输出字符和字符串。函数定义如下：
```
#include <stdio.h>

int fputc(int c, FILE *stream);

int fputs(const char *s, FILE *stream);

int putc(int c, FILE *stream);

int putchar(int c);

int puts(const char *s);
```