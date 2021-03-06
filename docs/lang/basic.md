## 代码框架

如果你不想深究背后的原理，初学时可以直接将这个“框架”背下来：

```cpp
#include <cstdio>
#include <iostream>

int main() {
  // do something...
  return 0;
}
```

??? note "什么是 include？"
     `#include` 其实是一个预处理命令，意思为将一个文件“放”在这条语句处。也就是说，在编译时，编译器会“复制” `iostream` 头文件中的内容，“粘贴”到 `#include <iostream>` 这条语句处。这样，你就可以使用 `iostream` 中提供的 `std::cin` 、 `std::cout` 、 `std::endl` 等对象了。

    如果你学过 C 语言，你会发现 C++ 中的头文件一般都不带 `.h` 后缀，而那些 C 语言中的头文件 `xx.h` 都变成了 `cxx` ，如 `stdio.h` 变成了 `cstdio` 。

    一般来说，应当根据你需要使用的 C++ 内置的函数、对象来确定你要 `#include` 哪些头文件。但如果你 `#include` 了多余的头文件，也几乎不会造成什么影响。

    可以 `#include` 自己写的头文件吗？答案是，可以。

    你可以自己写一个头文件，如： `myheader.h` 。然后，将其放到和你的代码相同的目录里，再 `#include "myheader.h"` 即可。需要注意的是，自定义的头文件需要使用引号而非尖括号。当然，你也可以使用编译命令 `-I <header_file_path>` 来告诉编译器在哪找头文件，就不需要将头文件放到和代码相同的目录里了。

??? note "什么是 main 函数？"
    可以理解为程序运行时就会执行 `main` 函数中的代码。

    实际上， `main` 函数是由系统或外部程序调用的。如，你在 cmd 中调用了你的程序，也就是调用了你程序中的 `main` 函数（在此之前先完成了全局变量的构造）。

    最后的 `return 0;` 表示程序运行成功。默认情况下，程序结束时返回 0 表示一切正常，否则表示错误代码。这个值返回给谁呢？其实就是调用你写的程序的系统或外部程序，它会在你的程序结束时接收到这个返回值。

    在 OI 中，程序的返回值不为 0 会导致运行时错误（RE）。

## 注释

在 C++ 代码中，注释有两种写法：

1.  行内注释

    以 `//` 开头，行内位于其后的内容全部为注释。

2.  注释块

    以 `/*` 开头， `*/` 结尾，中间的内容全部为注释，可以跨行。

注释对程序运行没有影响，可以用来解释程序的意思。

在工程开发中，注释可以便于日后维护、他人阅读。

在 OI 中，很多人都很少写注释，但注释可以便于日后复习，而且，如果要写题解、教程的话，适量的注释可以便于读者阅读。

## 输入与输出

### cin 与 cout

```cpp
#include <iostream>

int main() {
  int x, y;                          // 声明变量
  std::cin >> x >> y;                // 读入 x 和 y
  std::cout << y << std::endl << x;  // 输出 y，换行，再输出 x
  return 0;                          // 结束主函数
}
```

??? note "什么是 std？"
     `std` 是 C++ 标准库所使用的 **命名空间** 。使用命名空间是为了避免重名。

    例如：你定义了一个名为 `cin` 的变量，有了命名空间后，就可以通过 `cin` 和 `std::cin` 区分它们。

    访问命名空间内的成员有三种方式：

    1.  在成员名称前加上 `命名空间::` 。
    2.  使用指令 `using 命名空间::成员名;` ，这样的话，可以直接通过成员名访问成员，但如果定义了和成员同名的变量或函数，就会产生冲突。
    3.  使用指令 `using namespace 命名空间;` ，这样的话，可以直接通过成员名访问命名空间中的任何成员，但一旦定义了和命名空间中任何一个成员同名的变量或函数，就会产生冲突。

    在工程开发中，是不推荐使用 `using namespace 命名空间` 的。在 OI 中，很多人为了方便，总是使用 `using namespace std;` ，但这样做会有导致编译错误的风险。

    上面的代码还可以写成下面两种样子：

    ```cpp
    #include <iostream>

    using std::cin;
    using std::cout;
    using std::endl;

    int main() {
      int x, y;
      cin >> x >> y;
      cout << y << endl << x;
      return 0;
    }
    ```

    ```cpp
    #include <iostream>

    using namespace std;

    int main() {
      int x, y;
      cin >> x >> y;
      cout << y << endl << x;
      return 0;
    }
    ```

### scanf 与 printf

 `scanf` 与 `printf` 其实是 C 语言中的函数。大多数情况下，它们的速度比 `cin` 和 `cout` 更快，并且能够方便地支持格式控制。

```cpp
#include <cstdio>

int main() {
  int x, y;
  scanf("%d%d", &x, &y);   // 读入 x 和 y
  printf("%d\n%d", y, x);  // 输出 y，换行，再输出 x
  return 0;
}
```

其中， `%d` 表示读入/输出的变量是一个有符号整型 ( `int` 型）的变量。

类似地：

1.   `%s` 表示字符串。
2.   `%c` 表示字符。
3.   `%lf` 表示双精度浮点数 ( `double` )。
4.   `%lld` 表示长整型 ( `long long` )。根据系统不同，也可能是 `%I64d` 。
5.   `%u` 表示无符号整型  ( `unsigned int` )。
6.   `%llu` 表示无符号长整型 ( `unsigned long long` )，也可能是 `%I64u` 。

特殊地，还有一些控制格式的方式：

1.   `%1d` 表示长度为 1 的整型。在读入时，即使没有空格也可以逐位读入数字。在输出时，若指定的长度大于数字的位数，就会在数字前用空格填充。
2.   `%.6lf` ，用于输出，保留六位小数。

??? note "为什么 scanf 中有 & 运算符？"
    在这里， `&` 实际上是取址运算符，返回的是变量在内存中的地址。而 scanf 接收的参数就是变量的地址。

??? note "什么是 \n？"
     `\n` 是一种 **转义字符** ，表示换行。

    转义字符用来表示一些无法轻易输入的字符，如由于字符串字面值无法换行而无法输入的换行符，由于表示字符串字面值的开头结尾而无法输入的引号，由于表示转义字符而无法输入的反斜杠。

    常用的转义字符还有：

    1. `\t` 表示制表符。

    2. `\\` 表示 `\` 。

    3. `\"` 表示 `"` 。

    4. `\0` 表示空字符，用来表示 C 风格字符串的结尾。

    5. `\r` 表示回车。Linux 中换行符为 `\n` ，Windows 中换行符为 `\r\n` 。在 OI 中，如果输出需要换行，使用 `\n` 即可。但读入时，如果需要读入换行符，使用逐字符读入可能造成一些问题，需要注意。

## 一些扩展内容

### C++ 中的空白字符

在 C++ 中，所有空白字符（空格、制表符、换行），多个或是单个，都被视作是一样的。（当然，引号中视作字符串的一部分的不算。）

因此，你可以自由地使用任何代码风格（除了行内注释、字符串字面值与预处理命令必须在单行内），例如：

```cpp
/* clang-format off */

#include <iostream>

 int 

    main(){
int/**/x, y;  std::cin
>> x >>y;
                std::cout <<
          y  <<std::endl   
     << x
          
          ;
    
    return       0;     }
```

当然，这么做是不被推荐的。

一种不那么丑陋而与 **OI Wiki** 要求的码风不同的代码风格：

```cpp
/* clang-format off */

#include <iostream>

using namespace std; // 其实这么做是不被推荐的

int main()
{
    int x, y;

    cin >> x >> y;
    cout << y << endl << x;

    return 0;
}
```

### define 命令

 `#define` 是一种预处理命令，用于定义宏，本质上是文本替换。例如：

```cpp
#include <iostream>
#define n 233
// n 不是变量，而是编译器会将代码中所有 "n" 文本替换为 "233"

int main() {
  std::cout << n;  // 输出 233
  return 0;
}
```

宏可以带参数，带参数的宏可以像函数一样使用：

```cpp
#include <iostream>
#define sum(x, y) x + y
// 这里应当为 #define sum(x, y) (x + y)
#define square(x) ((x) * (x))

int main() {
  std::cout << sum(1, 2) << ' ' << 2 * sum(3, 5) << std::endl;
  // 输出为 3 11，因为 #define 是文本替换，后面的语句被替换为了 2 * 3 + 5
  int i = 1;
  std::cout << square(++i) << ' ' << i;
  // 输出为 9 3 或 6 3，因为 ++i 被执行了两遍
  // 而同一个语句中出现多个 ++ 是未定义行为
}
```

使用 `#define` 是有风险的（由于 `#define` 作用域是整个程序，因此可能导致文本被意外地替换），因此应谨慎使用。较为推荐的做法是：使用 `const` 限定符声明常量，使用函数代替宏。

但是，在 OI 中， `#define` 依然有用武之处（依然是不被推荐的，会降低代码的规范性）：

1.   `#define int long long` + `signed main()` 。通常用于避免忘记开 long long 导致的错误，或是调试时排除忘开 long long 导致错误的可能性。（也可能导致增大常数甚至 MLE。）
2.   `#define For(i, l, r) for (int i = l; i <= r; ++i)` 、 `#define push_back pb` 、 `#define mid ((l + r) / 2)` ，用于减短代码长度。
