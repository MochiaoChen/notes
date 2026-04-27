# Week 4：内存 (Memory)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#十六进制 (Hexadecimal)]]
* [[#内存 (Memory)]]
* [[#指针 (Pointers)]]
* [[#字符串 (Strings)]]
* [[#指针算术 (Pointer Arithmetic)]]
* [[#字符串比较与复制 (Comparison and Copying)]]
* [[#malloc 与 valgrind]]
* [[#文件读写 (File I/O)]]

## 十六进制 (Hexadecimal)

*   **16 进制系统：** 使用 16 个值：`0 1 2 3 4 5 6 7 8 9 a b c d e f`。
*   每列是 16 的幂。
*   **示例：** 10 是 `0A`，15 是 `0F`，16 是 `10`，255 是 `FF` (16 x 15 + 15)。
*   **简洁性：** 十六进制很有用，因为它比二进制或十进制使用更少的位数来表示信息。

## 内存 (Memory)

*   内存可以被可视化为连续的块，通常使用带 `0x` 前缀的十六进制编号（例如 `0x10`）。
*   **C 语言内存操作符：**
    *   `&`：提供存储在内存中的某个东西的**地址**。
    *   `*`：指示编译器前往内存中的某个位置（**解引用**）。
*   `%p` 是 `printf` 中用于查看内存地址的格式说明符。

## 指针 (Pointers)

*   指针是一个包含某个值地址的变量。
*   `int *p = &n;` 声明了一个存储整数 `n` 地址的指针 `p`。
*   指针通常是 8 字节的值。

## 字符串 (Strings)

*   `string` 是一个字符数组，但从技术上讲，它是指向该数组第一个字节的**指针**。
*   `char *s = "HI!";` 是字符串的原始 C 语言表示。
*   `cs50.h` 库通过 `typedef char *string;` 简化了这一点。

## 指针算术 (Pointer Arithmetic)

*   你可以使用指针数学来访问字符串中的字符。
*   `*(s + 1)` 等同于 `s[1]`。它将指针按数据类型的大小移动到下一个内存位置。

## 字符串比较与复制 (Comparison and Copying)

*   在字符串上使用 `==` 比较的是它们的**内存地址**，而不是内容。
*   必须使用 `strcmp(s, t)` 来比较实际字符。
*   **复制：** `string t = s;` 只复制地址。要创建真正的副本，必须：
    1.  使用 `malloc` 分配内存。
    2.  逐个字符复制（或使用 `strcpy`）。
*   **malloc：** 分配特定大小的内存。
*   **free：** 释放之前分配的内存以防止**内存泄漏 (Memory leaks)**。

## malloc 与 valgrind

*   **Valgrind：** 用于检查内存相关问题的工具，例如忘记 `free` 内存或“缓冲区溢出” (Buffer overflows)。

## 文件读写 (File I/O)

*   `FILE *file = fopen("filename", "a");` 打开文件。
*   `fprintf` 写入文件；`fclose` 关闭文件。
*   `fread` 和 `fwrite` 用于读写原始字节（例如 BMP 图像）。
