## `scanf()`的注意点

*注意*：需要注意的是，`scanf`函数在**读取数据时会忽略空格(并且以空白字符输入而结束获取数据)、制表符和换行符等空白字符，直到读取到一个非空白字符为止**。因此，在读取多个数据时，需要按照格式控制字符串中的格式说明符的顺序依次输入数据，并确保输入的数据与格式控制字符串的格式相匹配，否则可能会导致程序出现错误。另外，scanf函数也存在一些安全问题，~~建议使用安全版本的`scanf`函数`scanf_s`来替代.~~


而且在visual studio编辑器中使用scanf输入函数会报错
> This function or variable may be unsafe. Consider using scanf_s instead. To disable deprecation, use _CRT_SECURE_NO_WARNINGS 
>
> 解决方法：
>   - 在顶部定义
>   - `#define _CRT_SECURE_NO_WARNINGS 1 //定义为其他数字的话，可能会导致编译器不再忽略这些警告信息，从而影响代码的编译和运行。`

*特别特别注意*: `scanf`函数为C语言提供而`scanf_s`函数为**VS编辑器**提供,他不是标准C语言提供的.(所以并没有跨平台性和移植性)

`#define`是一个预处理指令，用于定义宏常量或宏函数。定义的宏常量可以在代码中使用，将其替换为指定的值。注意: `#define定义的常量后面不加分号 ;`

`_CRT_SECURE_NO_WARNINGS`是一个宏常量，用于禁用一些与安全性相关的警告信息。当使用一些不安全的标准库函数（如`scanf`、`strcpy`等）时，编译器会发出警告，提示可能存在安全风险。通过定义`_CRT_SECURE_NO_WARNINGS`为1，可以禁用这些警告信息。

---