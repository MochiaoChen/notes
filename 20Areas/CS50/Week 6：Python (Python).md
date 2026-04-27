# Week 6：Python (Python)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#Python 简介 (Introduction to Python)]]
* [[#你好世界 (Hello World)]]
* [[#变量与类型 (Variables and Types)]]
* [[#条件语句 (Conditionals)]]
* [[#循环 (Loops)]]
* [[#异常处理 (Exceptions)]]
* [[#列表与字典 (Lists and Dictionaries)]]
* [[#命令行参数 (Command-Line Arguments)]]

## Python 简介 (Introduction to Python)

*   Python 是一种高级的、**解释型 (Interpreted)** 语言（不需要单独的编译步骤）。
*   专注于可读性和简洁性，抽象掉了内存管理。
*   **权衡：** Python 通常比 C 语言慢，因为它在“底层”处理了内存和其他低级任务。

## 你好世界 (Hello World)

*   C 语言：需要 `#include`, `int main(void)`, `printf` 和分号。
*   Python：`print("hello, world")`。

## 变量与类型 (Variables and Types)

*   **无需类型声明：** 你不需要指定 `int` 或 `string`；Python 会推断类型。
*   **F-字符串 (Format strings)：** `print(f"hello, {answer}")`。
*   **常用类型：** `bool`, `float`, `int`, `str`。
*   **集合类型：** `list` (数组), `dict` (哈希表), `set` (唯一元素), `tuple` (不可变列表)。

## 条件语句 (Conditionals)

*   使用 `if`, `elif` 和 `else`。
*   **语法：** 使用冒号 (`:`) 和**缩进 (Indentation)** 而不是大括号 `{}`。
*   **逻辑运算符：** 使用单词 `and`, `or`, `not` 而不是 `&&`, `||`, `!`。

## 循环 (Loops)

*   `while` 循环与 C 语言类似。
*   `for` 循环通常使用 `range()`：`for i in range(3):`。
*   遍历列表：`for item in my_list:`。

## 异常处理 (Exceptions)

*   用于优雅地处理错误。
*   `try` 和 `except` 块可以防止程序在输入无效数据时崩溃（例如，当预期为 `int` 时输入了字符串）。

## 列表与字典 (Lists and Dictionaries)

*   **列表 (Lists)：** 具有 `.append()` 等方法的动态数组。
*   **字典 (Dictionaries, `dict`)：** 存储键值对：`people = {"Carter": "+1-617...", "David": "+1-617..."}`。在字典中搜索是高度优化的（接近常数时间）。

## 命令行参数 (Command-Line Arguments)

*   通过 `sys` 库访问：`from sys import argv`。
*   `argv[0]` 是脚本的名称。
*   `sys.exit(0)` 表示成功；`sys.exit(1)` 表示错误。
