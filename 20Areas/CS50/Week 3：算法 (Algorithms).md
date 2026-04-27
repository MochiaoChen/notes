# Week 3：算法 (Algorithms)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#线性搜索 (Linear Search)]]
* [[#二分搜索 (Binary Search)]]
* [[#运行时间 (Running Time)]]
* [[#数据结构 (Data Structures)]]
* [[#排序算法 (Sorting Algorithms)]]
* [[#递归 (Recursion)]]
* [[#归并排序 (Merge Sort)]]

## 线性搜索 (Linear Search)

*   **过程：** 从头到尾逐个检查数组的每个元素。
*   **效率：** $O(n)$（最坏情况下需要 $n$ 步）。

## 二分搜索 (Binary Search)

*   **前提条件：** 列表必须是**有序的 (Sorted)**。
*   **过程：** 分而治之。检查中间元素，然后舍弃不可能包含目标的那一半。
*   **效率：** $O(\log n)$。

## 运行时间 (Running Time)

*   **大 O 表示法 (Big O Notation)：**
    *   **上界 ($O$)：** 最坏情况。
    *   **下界 ($\Omega$)：** 最好情况。
    *   **紧确界 ($\Theta$)：** 当上界和下界相同时。
*   **常见阶数：** $O(n^2)$（最慢）, $O(n \log n)$, $O(n)$, $O(\log n)$, $O(1)$（最快）。

## 数据结构 (Data Structures)

*   **结构体 (struct)：** 一种创建自定义数据类型的方法，可以将不同的变量组合在一起（例如，一个包含 `name` 和 `number` 的 `person` 结构体）。
*   **点符号 (Dot Notation)：** 用于访问结构体的属性（例如：`people[i].name`）。

## 排序算法 (Sorting Algorithms)

*   **选择排序 (Selection Sort)：** 寻找最小元素并将其交换到前面。效率：$O(n^2)$, $\Omega(n^2)$。
*   **冒泡排序 (Bubble Sort)：** 重复交换相邻的错误顺序元素。效率：$O(n^2)$, $\Omega(n)$（如果优化为在没有交换发生时停止）。

## 递归 (Recursion)

*   **定义：** 调用自身的函数。
*   **基本情况 (Base Case)：** 停止递归的条件，防止无限循环。
*   **递归情况 (Recursive Case)：** 函数调用自身以处理更小规模问题的部分。

## 归并排序 (Merge Sort)

*   **过程：** 递归地将数组对半拆分，直到只剩下单个元素，然后按顺序合并。
*   **效率：** $\Theta(n \log n)$。在大数据集上比冒泡排序或选择排序快得多。
