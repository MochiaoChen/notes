# Week 1：C (C)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#欢迎！ (Welcome!)]]
* [[#Hello World]]
* [[#函数 (Functions)]]
* [[#变量 (Variables)]]
* [[#条件语句 (Conditionals)]]
* [[#循环 (Loops)]]
* [[#操作符与抽象 (Operators and Abstraction)]]
* [[#Linux 与命令行 (Linux and the Command Line)]]
* [[#类型与内存 (Types and Memory)]]
* [[#总结 (Summing Up)]]

## 欢迎！ (Welcome!)

*   **编程概念：** 在 Scratch（视觉化编程）中学到的概念适用于所有编程语言。
*   **二进制与机器码：** 计算机只理解二进制（1 和 0）。人类编写的是**源代码 (Source code)**，由**编译器 (Compiler)** 转换为**机器码 (Machine code)**。
*   **评价指标：** 代码的评判标准包括**正确性 (Correctness)**（是否运行？）、**设计 (Design)**（构建得如何？）和**风格 (Style)**（美学上是否一致？）。

## Hello World

*   **集成开发环境 (IDE)：** 课程使用基于 VS Code 的 `cs50.dev`。
*   **工作流命令：**
    *   `code hello.c`：创建/打开源文件。
    *   `make hello`：将源代码编译为可执行文件。
    *   `./hello`：运行编译后的程序。
*   **基础语法：** C 程序需要 `#include <stdio.h>` 来使用 `printf` 函数。`main` 函数是程序的入口。`\n` 是换行转义字符。

## 变量 (Variables)

*   **get_string：** CS50 库中的函数，用于获取用户输入。
*   **赋值：** `string answer = get_string("...");` 将输入存储在变量中。
*   **格式代码 (Format Codes)：** `printf` 中的占位符，如 `%s`（字符串）、`%i`（整数）、`%c`（字符）和 `%f`（浮点数）。
*   **cs50.h：** 包含 `string` 类型和 `get_string` 等函数所需的自定义库。

## 条件语句 (Conditionals)

*   **赋值与相等：** `=` 用于赋值；`==` 用于检查相等。
*   **逻辑运算符：** `||` 代表“或”，`&&` 代表“与”。
*   **递增/递减：** `counter++` 加一；`counter--` 减一。

## 循环 (Loops)

*   **while 循环：** 只要条件为真就运行。
*   **for 循环：** 在一行中包含初始化、条件和递增：`for (int i = 0; i < 3; i++)`。
*   **死循环：** `while (true)` 永远运行（使用 `Ctrl+C` 停止）。

## Linux 与命令行 (Linux and the Command Line)

*   **常用命令：**
    *   `ls`：列出文件。
    *   `cd`：切换目录。
    *   `mkdir`：创建目录。
    *   `cp`：复制文件。
    *   `mv`：移动/重命名文件。
    *   `rm`：删除文件。

## 类型与内存 (Types and Memory)

*   **内存限制：** 每种数据类型在内存中都有固定大小（位）。
*   **整数溢出 (Integer Overflow)：** 当数字超过类型能容纳的最大值时发生，导致计算错误。
*   **常见类型：** `bool`, `char`, `double`, `float`, `int`, `long`, `string`。
