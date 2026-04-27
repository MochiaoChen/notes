# Week 2：数组 (Arrays)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#编译 (Compiling)]]
* [[#调试 (Debugging)]]
* [[#数组 (Arrays)]]
* [[#字符串 (Strings)]]
* [[#命令行参数 (Command-Line Arguments)]]
* [[#退出状态 (Exit Status)]]
* [[#密码学 (Cryptography)]]

## 编译 (Compiling)

*   **编译的步骤：**
    1.  **预处理 (Preprocessing)：** 处理头文件（如 `#include`），将其内容复制到文件中。
    2.  **编译 (Compiling)：** 将源代码转换为**汇编代码 (Assembly code)**。
    3.  **汇编 (Assembling)：** 将汇编代码转换为**机器码 (Machine code)**（二进制）。
    4.  **链接 (Linking)：** 将库文件与程序合并为一个可执行文件。

## 调试 (Debugging)

*   **方法：**
    1.  **printf：** 打印变量值以观察代码运行情况。
    2.  **调试器 (Debugger)：** 使用 `debug50` 等工具设置**断点 (Breakpoints)** 并逐行执行。
    3.  **小黄鸭调试法 (Rubber Duck Debugging)：** 通过大声解释逻辑来发现错误。

## 数组 (Arrays)

*   **定义：** 在内存中连续存储数据的一种方式。
*   **内存大小：** `char` (1 字节), `int` (4 字节), `float` (4 字节), `long` (8 字节)。
*   **索引：** 数组索引从零开始（第一个元素在 `[0]`）。
*   **声明：** `int scores[3];` 为三个整数分配空间。

## 字符串 (Strings)

*   **字符串本质：** `string` 本质上是 `char` 变量的数组。
*   **NUL 字符：** 字符串以一个特殊的隐藏字符 `\0` (NUL) 结尾，告诉计算机字符串在哪里结束。
*   **字符串长度：** `string.h` 中的 `strlen` 函数计算 NUL 终止符前的字符数。

## 命令行参数 (Command-Line Arguments)

*   **argc：** “参数计数” (Argument count)，即在提示符下输入的单词数。
*   **argv：** “参数矢量” (Argument vector)，包含这些单词的字符串数组。`argv[0]` 始终是程序名称。

## 退出状态 (Exit Status)

*   **返回值：** `main` 函数返回一个整数。`0` 通常表示成功，非零值（如 `1`）表示错误。

## 密码学 (Cryptography)

*   **概念：** **明文 (Plaintext)** + **密钥 (Key)** → **算法** → **密文 (Ciphertext)**。
*   **密钥：** 一个决定算法如何转换文本的秘密参数。
