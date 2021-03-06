#C语言程序执行

这一讲，将解析一个Hello World程序。并利用该程序，讲解C语言执行的过程。

##Hello World

工程创建完以后，Xcode默认给出了一个Hello World的输出，先来分析下：

```c
// 预编译头
#include <stdio.h>

// main函数，程序入口
int main(int argc, const char * argv[]) {

    // 输出语句
    printf("Hello, World!\n");

    // 返回值
    return 0;
}

```

因为现在还没学`函数`部分，所以我们只对这段代码做简单了解。

#### `#include <stdio.h>`

引入预编译头文件，`.h`意思是`head`头文件。

因为在程序中，不是所有事情都是我们自己做，比如看到的`printf`这是系统提供的，那么我们要用，就必须引入相应的头文件，好让编译器做相应链接。

那么关于`#include`的方式有两种：

1. 一种是`<>`，系统头文件，如`#include <stdio.h>`
2. 一种是`""`，自定义头文件，如`#include "myhead.h"`

#### `int main(int argc, const char * argv[])`

main函数，程序入口。

对于为什么要这样写，大家大可不必现在着急去理解（函数部分会详细讲解）。只需要知道，写main函数的几个注意点就行。

1. 一个工程<font color=red>只能有一个</font>main函数；
2. main函数是程序执行的入口；
3. main后面必须有`()`；
4. `{}`内部是函数体。

除了系统提供的，常见的main函数写法有：

```c
int main() {

    // 函数体

    return 0;
}

```
在最新的C99标准下，已经不推荐或不支持以下写法了。但是遇到了一定要能看懂。

```c
void main() {


}

```

```c
main() {


}

```

#### `printf("Hello, World");`

输出语句。在控制台上打印Hello World

#### `return 0;`

返回值。

如果main函数前面是`int`而不是`void`，就需要在最后加上`return 0;`。函数遇到`return`就结束。

##注释

在写程序的过程中，可以看到很多`//`或者`/**/`这样的字符，一般编译器的默认颜色都是<font color=green>绿色</font>。他们叫做*注释*。注释在程序运行时，是不会进行编译的，因为注释是写给人看的，而不是写给机器。Xcode注释的快捷键是`Command + /`。

常见的注释形式：

```c
// 这是一句单行注释
```

```c
/*
    这是多行注释
    可以换行
*/

```

```c
#pragma mark - 苹果独有的注释方式，通常用于标记一类函数的作用

```

####注释怎么用

对于函数的注释，我推荐VVDocuments插件，猫神开发，值得信赖。

1.对比较复杂逻辑，需要写详细注释，方便理解与纠错；

```c
// 循环，i从0开始........
for (int i = 0; i < 4 ; i ++) {

    // 逻辑处理
}

```
2.对于容易混淆的变量，要给出变量注释；

```c
int myVar = 0;         // 用于存放xxx
double ourVar = 1.0;   // 用于存放xxxx

```

3.对于函数，要给出函数的作用、参数、返回值注释；

```c
/**
 *  测试函数
 *
 *  @param a 测试变量
 *
 *  @return 返回值含义....
 */
int test(int a) {

    return 0;
}

```

4.对于暂时不需要的代码，可以进行注释；

```c
//    printf("Hello");
printf("World");

```

##程序执行过程

一个C语言的程序，在运行就可以看到结果。其实在这个过程中，编译器帮我们做了两件大事：<font color=red>编译</font>与<font color=red>链接</font>。

###编译器：

写C语言的时候，虽然我们写得很畅快，但是计算机只认识二进制代码，所以我们与计算机之前，还需要一个“翻译”——编译器。在苹果几乎变态的强迫症下，它所使用的编译器是Clang（Xcode只是IDE集成开发环境而已）。关于平时听到的GCC，LLVM，Clang的区别与关系，[知乎上这篇文章还不错](http://www.zhihu.com/question/20039402)。

###编译：

在编译过程中，工程中的每一个`.c`文件都会对应编译成二进制文件，并且编译器还会在这一步对程序的<font color=red>语法</font>（不是程序逻辑）进行检查。在Xcode中，我们常说的编译不通过(Build Fail)，意思就是程序有语法错误（也有可能是工程配置错误）。

编译成功，会生成一个`.o`二进制文件（windows下是`.obj`）。如`main.c`将编译为`main.o`，这个文件被称为*目标文件*。

###链接

编译完以后，所生成的目标文件还不能直接运行，因为：

1. 一个工程中有很多的`.c`文件，他们一般密不可分，运行时，需要将它们相互关联；
2. 程序中所依赖的函数库也需要关联；

我们将上面的这两个步骤，成为*链接*。

链接后，生成*可执行文件*`.out`，windows下是`.exe`。

##总结

这一讲主要讲解了：

1. Hello World程序；
2. 三种注释方式；
3. 程序的执行经过的编译与链接这两个过程。

关于文中，提到的函数等知识点，不明白可以先听着，不用着急去理解。知道main函数的写法，写程序要写注释，程序怎么执行就行。
