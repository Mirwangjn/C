# <windows.h>

## Sleep函数

> 作用:让当前线程暂停执行一段指定的时间。

语法: `Sleep(毫秒)`

---

# <stdlib.h>

> 全称: standard library 标准库

## system()

语法: `system(command)`

**操作系统指令**
- `cls` - 清屏
- `cd` - 切换当前目录
- `mkdir` - 创建新的目录
- `shutdown /s /t <seconds>` - 关机指令
- `shutdown /a` - 取消关机指令

```c
    system("cls");// 清空控制台
```

---

## rand()


> rand作用为生成随机数，而srand用于设置随机数生成器的种子。它两通常是一对.
>
>>rand的范围是**0 - RAND_MAX**,而RAND_MAX是由`#define`定义的值为
>>**0x7fff**是一个十六进制,在C语言中，0x表示后面的数字是十六进制数。7fff对应的十进制为*32767*
>
>> rand函数全称为random，而srand函数全称应该是 seed random
```c
    #include <stdlib.h>

    #include <time.h>
    // RAND_MAX --- 0 ~ 32767
    int main () {
        //所以变量必须在函数最上方
        int i = 0;
        /*
            srand参数类型为unsigned int，而time函数返回类型为time_t
            而time_t是通过typedef定义而来它实际上就是一个long类型

        */
        srand((unsigned int)time(NULL));
        //在使用rand函数之前需要提前设置种子，不然就没有随机数，而是统一的一个值
        i = rand();

        return 0;
    }
    
```

---

## srand()

语法：`void srand(unsigned int seed)`

> srand函数用于设置随机数生成器的种子，一般使用当前时间作为种子。

---

## qsort()

原型: `void qsort(void *base, size_t number, size_t size, int (*compare)(const void *, const void *))`

- base: 指向要排序的数组的指针
- number: 数组中元素的个数
- size: 每个元素的大小（以字节为单位）
- compare: 比较函数的指针，用于确定元素的顺序

compare函数指针细节: `int compare(const void *a, const void *b)`

在比较函数compare中，返回值代表着两个元素的大小关系。
这样，qsort函数根据比较函数的返回值来确定元素的顺序，从而实现对数组的排序。

- 返回值 > 0 表示第二个元素应该排在第一个元素之前
- 返回值 = 0 表示两个元素相等，它们的相对位置不变
- 返回值 < 0 表示第一个元素应该排在第二个元素之前

> 具体使用参考

---

# <time.h>

## time()

语法:`time_t time(time_t *t);`

时间戳获取: `time(NULL);`

---

# <stdio.h>

## `scanf`细节

> 在输入时格式需要注意，在输入中需要对应

```c
    //在输入时应写--- 1#2#3
    scanf("%d#%d#%d", &i, &z, &y);
    //在输入时应写--- 1 2 3
    scanf("%d %d %d", &i, &z, &y);
```

---

## printf打印格式

> 打印字符格式的数据

- %d - 打印int类型的整型
- %c - 打印字符
- %s - 表示输入一个字符串
- %lf - 表示输入一个双精度浮点数
- %f - 打印浮点数 - 小数
- %ld - 表示输入一个长整数。
- %p - 以地址的形式打印 (每一块内存空间都有着自己的地址)(占位符将会被实际指针的十六进制表示所替代)
- %x - 打印16进制
- %zd - 打印size_t类型(为typedef定义的类型实际就是unsigned int)的参数的整数
- %u - 打印无符号整数(包括负数---负数打印的结果为负数的绝对值与无符号整型的取值范围取模后得到的结果)
- %nd - 输出的整数占n位，不足n位则在前面补空格(n为整数)
- %-nd - 输出的整数占n位，不足n位则在后面补空格(n为整数)
- ...

---

# <string.h>

## strlen()

语法: `size_t strlen(const char* str)`

- str -- 要计算长度的字符串.

返回值: 字符串的长度.

> 1. 计算字符串长度时，不包括`\0`
>
> 2. 返回值类型`size_t`实际上是`typedef unsigned int size_t`
>
> 3. 当无符号数 - 无符号数时结果也是一个无符号数, 是一个>=0的数

---

## strcpy()

语法：`strcpy(目标字符串, 源字符串)`

`char *strcpy(char *dest, const char *src)`

return value: destination string(目标字符串)


> `strcpy`方法是一个字符串复制函数，用于将一个字符串复制到另一个字符串中。需要注意的是，`strcpy`函数不会检查目标字符串的长度，如果目标字符串的空间不足以容纳源字符串，则会导致**内存溢出**的问题。因此，在使用`strcpy`函数时需要确保目标字符串有足够的空间来容纳源字符串。`strcpy`会把源字符串的`\0`也拷贝过来。

---

```c
    /*
        const char* 意味着指针指向的元素的类型为 const char
	    所以这么做是防止在编写这个函数的时候搞混参数
    */s
    void my_strcpy(char* dest, const char* src) {
        if(dest == NULL || src == NULL) return;

        while(*src != '\0') {
            *(dest++) = *(src++);
        };
        //等于'\0'时执行的操作
        *dest = *src;
    }

    char* my_strcpy(char* dest, const char* src) {
        assert(dist != NULL);
		assert(src != NULL);
        //保留原味。因为存储的是地址，所以内部的值怎么改跟地址没什么关系
        char* result = dest;
        //将src的数据拷贝到dest包括'\0'
        while (*(dest++) = *(src++))
        {
            ;
        }
        //不直接返回dest是因为它因为通过++改变了
        return result;
    }
       
```

> [关于const char类型请参考`const修饰指针`](#const修饰指针)
>
> [关于assert使用请参考`assert.h`](#asserth头文件)
>
> 查看源文件查考`D:\Windows Kits\10\Source\10.0.22621.0\ucrt`

---

## strcmp()

语法:`int strcmp(const char *str1, const char *str2);`

- str1 -- 要进行比较的第一个字符串.
- str2 -- 要进行比较的第二个字符串.

返回值如下:

- 如果返回值 < 0，则表示 str1 小于 str2。
- 如果返回值 > 0，则表示 str1 大于 str2。
- 如果返回值 = 0，则表示 str1 等于 str2。

> 该函数接受两个参数，分别是要比较的两个字符串str1和str2。如果两个字符串相等，函数返回值为0；如果str1小于str2，返回值为负数；如果str1大于str2，返回值为正数。
>
> 在VS编辑器下str1 大于 str2返回值为-1; str1 小于 str2返回值为1
>
> [关于`strcmp`如何排列字符串的请参考字符串的比较方式](./show_detail/detail.md#字符串的比较方式)

---

## strcat()

语法: `char* strcat(char* dest, const char* src)`

功能:合并字符串

- dest -- 目标字符数组,且**足够容纳追加后的字符串。**
- src -- 指向要追加的字符串，该字符串不会覆盖目标字符串。

> 注意点`strcat`无法自己追加自己

---

## strstr()

语法: `char* strstr(const char* haystack, const char* needle)`

- haystack -- 要被检索的 C 字符串。
- needle -- 在 haystack 字符串内要搜索的小字符串。

返回值: `haystack`中第一次出现`needle`字符串的位置的地址，如果未找到则返回`NULL空指针`

---

## strncat()

语法: `char* strncat(char* dest, const char* src, size_t count)`

功能:合并字符串,且可以合并自己

- dest -- 目标字符数组, 且足够容纳追加后的字符串，包括额外的空字符。
- src -- 要追加的字符串。
- count -- 要追加的最大字符数。

> - 追加`count`个字符之后会主动补一个`'\0'`
> - 当`count` > 实际的`src`长度时, 多余的部分直接放弃不管
> 
> [strncat的注意点参考strncat的细节](./show_detail/detail.md#strncat的细节)

---

## strncpy()

语法: `char* strncpy(char* dest, const char* src, size_t count)`

- dest -- 指向用于存储复制内容的目标数组。
- src -- 要复制的字符串。
- count -- 要从源中复制的字符数。

返回值: 最终dest被复制完成后的结果

> 如果`count`的长度大于`src`, 超出的长度会给dest补`0`
>
> [strncpy的注意点参考strncpy的细节](./show_detail/detail.md#strncpy的细节)

---

## strtok()

语法: `char* strtok(char* str, const char* delim)`

- str -- 要被分解成一组小字符串的字符串.
- delim -- 包含分隔符的C字符串。

返回值: 被分解的第一个子字符串，如果没有可检索的字符串，则返回一个空指针.

> `strtok`函数会改变原来的字符串, 所以在使用时最好提前备份. 
>
> 当遇到`delim`包含的分隔符时, 会把分隔符替换为`'\0'`, 并且会记住这个位置(静态)

---

## strerror()

语法: `char* strerror(int errnum)`

- errnum -- 错误号，通常是 `errno`.

返回值: 一个指向错误字符串的指针，该错误字符串描述了错误errnum(错误信息)。

> [`errno`的作用参考errno.h头文件的errno](#errno)

---

## memcpy()

语法: `void* memcpy(void* dest, const void* src, size_t num)`

作用: 在内存中将`src`的数据copy到dest中

- dest -- 用于存储复制内容的目标数组
- src -- 复制的数据源
- num -- 要被复制的字节数

在使用时最好不要令`dest`与`src`一直, 如果必须则最好使用`memmove()`

> [`memcpy`函数使用参考这里](./show_detail/detail.md#memcpy基本使用)
>
> [`memcpy`实现方式参考这里](./subject/头文件实现.md#memcpy)


---

# <assert.h>

语法:`assert(condition)`

若用户指定的条件非true，则异常终止程序。可以在发行版本禁用。

```c
    #define NDEBUG 
    //若在上方定义宏名，则assert不做任何事(功能消失)
    #include <assert.h>
```

> 当定义了`NDEBUG`宏时，`assert`宏将被禁用，程序将不会执行这些检查，从而提高
> 
> 程序的执行效率。通常在发布版本中使用`NDEBUG`宏来禁用`assert`宏，以避免不必要的开销和性能损失。
> 
> - 宏 assert 的定义依赖于标准库不定义的另一个宏 NDEBUG 
> - ASSERT 只有在 Debug 版本中才有效，如果编译为 Release 版本则被忽略。



---

# <errno.h>

## errno

`errno`是通过`#define`定义的宏, **通过由系统调用设置**. 当C语言的库函数在执行
过程中, 发生了错误, 就会把对应的错误码(每一个错误码对应不同的信息),赋值给`errno`

错误码:

- 0 -- No error
- 1 -- Operation not permitted
- 2 -- No such file or directory
- ...更多的错误码参考C语言<errno.h>

---

# <ctype.h>

## isdigit()

语法: `int isdigit(int c)`

作用: 检查所传的字符是否是十进制数字

- c -- 需要检查的`字符`.

返回值: 如果 c 是一个数字，则该函数返回非零值`(true)`，否则返回 0`(false)`。

---

## islower()

语法: `int isalnum(int c)`

作用: 检查所传的字符是否为字母和数字

- c -- 需要检查的`字符`.

返回值: 如果 c 是一个数字或一个字母，则该函数返回非零值，否则返回`0`

---

## isupper()

语法: `int isupper(int c)`

作用: 检查所传的字符是否是大写字母

- c -- 需要检查的`字符`.

返回值: 如果 c 是一个大写字母，则该函数返回非零值，否则返回 0

---

## isalpha()

语法: `int isalpha(int c)`

作用:  检查所传的字符是否是字母

- c -- 需要检查的`字符`.

返回值: 如果 c 是一个字母，则该函数返回非零值，否则返回 0

---

# <stddef.h>

## offsetof()

语法: `offsetof(structName, memberName)`

作用: 计算结构成员相对于结构体开头的字节偏移量

- structName -- 结构体类型名
- memberName -- 结构体成员名

返回值: 该宏返回类型为`size_t`的值，表示`structName`中成员(memberName)的偏移量。

```c
#include <stddef.h>

struct S1
{
	char c1;// 1
    // 7
	double d;// 8
};

int main()
{
	struct S1 s1 = { 0 };
	printf("%zd\n", offsetof(struct S1, d));// 8
	return 0;
}
```