### 本讲目录
*   面向对象编程 (Object-Oriented Programming)
*   类 (Classes)
*   `raise` 异常抛出
*   装饰器 (Decorators)
*   与课程先前内容的联系
*   类方法 (Class Methods)
*   静态方法 (Static Methods)
*   继承 (Inheritance)
*   继承与异常
*   运算符重载 (Operator Overloading)
*   总结

## 面向对象编程 (Object-Oriented Programming)

编程有多种不同的**范式**（paradigms）。随着你学习更多编程语言，你会开始识别出这些模式。

到目前为止，你的编程方式都是**过程式**的——一步一步地执行指令。

而**面向对象编程**（Object-Oriented Programming, OOP）是解决编程问题的另一套强大且优雅的方案。

首先，让我们从一个熟悉的过程式程序开始。在终端窗口中输入 `code student.py` 并编写以下代码：

```python
name = input("Name: ")
house = input("House: ")
print(f"{name} from {house}")
```

请注意，这个程序遵循了过程式的、一步一步执行的范式，就像你在本课程之前看到的大部分代码一样。

### 运用函数进行抽象

借鉴我们前几周学习的内容，我们可以使用函数来抽象程序的部分功能，使其结构更清晰。

```python
def main():
    name = get_name()
    house = get_house()
    print(f"{name} from {house}")


def get_name():
    return input("Name: ")


def get_house():
    return input("House: ")


if __name__ == "__main__":
    main()
```

注意 `get_name` 和 `get_house` 函数如何将获取输入的细节从 `main` 函数中分离（抽象）出去。此外，代码末尾的 `if __name__ == "__main__":` 语句块会告诉解释器去执行 `main` 函数。

### 使用元组 (Tuple) 存储数据

我们可以通过将学生信息存储为**元组 (tuple)** 来进一步简化程序。元组是一个值的序列，但与列表不同，**元组是不可变的 (immutable)**，一旦创建就不能修改。在概念上，我们这里是从一个函数返回了两个值。

```python
def main():
    name, house = get_student()
    print(f"{name} from {house}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return name, house # 这里隐式地创建并返回了一个元组 (name, house)


if __name__ == "__main__":
    main()
```

注意 `get_student` 函数如何同时返回 `name` 和 `house`。这种同时为多个变量赋值的语法称为“元组解包 (tuple unpacking)”。

我们也可以将返回的元组打包进一个名为 `student` 的变量中，代码可以修改如下：

```python
def main():
    student = get_student()
    # 通过索引访问元组的元素
    print(f"{student[0]} from {student[1]}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return (name, house) # 显式地返回一个元组


if __name__ == "__main__":
    main()
```

请注意，`(name, house)` 这种写法向阅读代码的任何人明确表示，我们将两个值打包在一个数据结构中返回。此外，我们可以使用索引 `student[0]` 或 `student[1]` 来访问元组中的元素。

元组的**不可变性**是其重要特性，这意味着我们不能更改其中的值。这种特性是一种防御性编程的手段，可以防止数据被意外修改。

```python
def main():
    student = get_student()
    if student[0] == "Padma":
        student[1] = "Ravenclaw" # 尝试修改元组的第二个元素
    print(f"{student[0]} from {student[1]}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return name, house


if __name__ == "__main__":
    main()
```
运行这段代码会产生一个 `TypeError` 错误，因为元组是不可变的，我们无法重新分配 `student[1]` 的值。

### 使用列表 (List) 带来的灵活性

如果我们希望为其他程序员提供更大的灵活性，我们可以使用**列表 (list)**：

```python
def main():
    student = get_student()
    if student[0] == "Padma":
        student[1] = "Ravenclaw" # 修改列表是允许的
    print(f"{student[0]} from {student[1]}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return [name, house] # 返回一个列表


if __name__ == "__main__":
    main()
```

注意，列表是**可变的 (mutable)**。这意味着程序员可以更改列表中元素的顺序或值。在某些情况下，你可能希望提供这种灵活性，但这会牺牲代码的安全性。毕竟，如果值的顺序是可变的，与你协作的程序员未来可能会因为弄错顺序而出错。

### 使用字典 (Dictionary) 提高可读性

在这种场景下，**字典 (dictionary)** 也是一个很好的选择。回想一下，字典存储的是“键-值”(key-value)对。

```python
def main():
    student = get_student()
    print(f"{student['name']} from {student['house']}")


def get_student():
    student = {} # 创建一个空字典
    student["name"] = input("Name: ")
    student["house"] = input("House: ")
    return student


if __name__ == "__main__":
    main()
```
注意，在这种情况下，我们返回了两个键值对。这种方法的一个巨大优势是，我们可以通过有意义的键（如 `'name'` 和 `'house'`）来访问数据，而不是依赖于不直观的数字索引。

我们还可以进一步优化代码。`student = {}` 这个变量其实是不必要的，我们可以直接构建并返回字典。

```python
def main():
    student = get_student()
    print(f"{student['name']} from {student['house']}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return {"name": name, "house": house} # 直接在 return 语句中创建字典


if __name__ == "__main__":
    main()
```
注意我们如何在 `return` 语句中直接使用 `{}` 大括号来创建并返回字典，这让代码更加简洁。

我们也可以在字典版本的代码中处理 Padma 的特殊情况：
```python
def main():
    student = get_student()
    if student["name"] == "Padma":
        student["house"] = "Ravenclaw"
    print(f"{student['name']} from {student['house']}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return {"name": name, "house": house}


if __name__ == "__main__":
    main()
```
注意，与列表的实现类似，我们可以使用键名来索引并修改 `student` 字典中的值。

## 类 (Classes)

在面向对象编程中，**类 (Class)** 是一种强大的工具，它允许我们创建自己的数据类型并为其命名。

> 一个类就像一个数据类型的“模具”或“蓝图”——我们可以据此创造出自己的数据类型，并赋予它们独特的属性和行为。

我们可以将代码修改如下，以实现一个我们自己的 `Student` 类：

```python
class Student:
    ... # ... 表示这部分代码我们稍后会回来完成


def main():
    student = get_student()
    print(f"{student.name} from {student.house}")


def get_student():
    student = Student() # 使用 Student() 创建一个 Student 类的实例
    student.name = input("Name: ")
    student.house = input("House: ")
    return student


if __name__ == "__main__":
    main()
```
请注意以下几点：
1.  按照惯例，类名 `Student` 的首字母大写。
2.  `...` 只是一个占位符，表示我们稍后会填充类的具体内容。
3.  在 `get_student` 函数中，我们使用 `student = Student()` 语法创建了一个 `Student` 类的**实例**或**对象 (object)**。
4.  我们使用“点标记法”（dot notation），如 `student.name`，来访问这个 `student` 对象的**属性 (attributes)**。

> 每当你使用一个类作为蓝图来创造一个具体的东西时，你创建的就是一个**对象 (object)** 或一个**实例 (instance)**。在我们的代码中，`student` 就是一个对象。

接下来，我们可以在 `Student` 类中明确定义其对象应该具备哪些属性。这通常通过一个特殊的方法 `__init__` 来完成。

```python
class Student:
    # __init__ 是一个特殊的方法，称为构造方法 (constructor)
    # 当创建类的新实例时，它会被自动调用
    def __init__(self, name, house):
        self.name = name
        self.house = house


def main():
    student = get_student()
    print(f"{student.name} from {student.house}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    student = Student(name, house) # 在创建实例时直接传入参数
    return student


if __name__ == "__main__":
    main()
```
请注意，我们在 `Student` 类内部定义了 `__init__` 方法，用于规范化该类实例的属性。在类内部定义的函数称为**方法 (method)**。`__init__` 方法接收传入的 `name` 和 `house` 参数，并将它们赋值给当前对象的属性。

这里的 `self` 关键字非常重要，它**指向刚刚创建的那个对象实例本身**。因此 `self.name = name` 的意思是：“将这个对象（`self`）的 `name` 属性设置为传入的 `name` 参数的值”。

构造实例的调用 `student = Student(name, house)` 会自动触发 `__init__` 方法的执行。

我们可以将 `get_student` 函数简化如下：

```python
class Student:
    def __init__(self, name, house):
        self.name = name
        self.house = house


def main():
    student = get_student()
    print(f"{student.name} from {student.house}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return Student(name, house) # 直接返回新创建的 Student 实例


if __name__ == "__main__":
    main()
```

注意 `return Student(name, house)` 如何将上一版本代码中的两行（创建实例和返回实例）合并为一行，使代码更简洁。

你可以在 [Python 官方文档中学习更多关于类的内容](https://docs.python.org/3/tutorial/classes.html)。

## `raise` 异常抛出

面向对象编程鼓励你将一个类的所有功能都**封装 (encapsulate)** 在类的定义内部。但如果出现问题怎么办？比如用户试图输入一些随机的东西，或者尝试创建一个没有名字的学生？我们可以通过**抛出异常**来处理这些情况。

修改你的代码如下：

```python
class Student:
    def __init__(self, name, house):
        if not name:
            raise ValueError("Missing name") # 如果名字为空，抛出 ValueError
        if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
            raise ValueError("Invalid house") # 如果学院无效，抛出 ValueError
        self.name = name
        self.house = house


def main():
    student = get_student()
    print(f"{student.name} from {student.house}")


def get_student():
    name = input("Name: ")
    house = input("House: ")
    # 如果输入无效，这里的 Student(name, house) 调用会触发异常
    return Student(name, house)


if __name__ == "__main__":
    main()
```
注意我们现在是如何在 `__init__` 方法中检查 `name` 是否已提供以及 `house` 是否是有效的学院。`raise` 关键字允许我们主动触发一个异常，以提醒程序员或用户出现了错误。在上面的例子中，我们抛出了 `ValueError`，并附带了具体的错误信息。

### `__str__` 方法

Python 允许你定义一个名为 `__str__` 的特殊方法，用于控制当你尝试 `print()` 一个对象时，应该显示什么内容。

修改你的代码如下：

```python
class Student:
    def __init__(self, name, house, patronus):
        if not name:
            raise ValueError("Missing name")
        if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
            raise ValueError("Invalid house")
        self.name = name
        self.house = house
        self.patronus = patronus

    # 当 print(student) 或 str(student) 被调用时，这个方法会被执行
    def __str__(self):
        return f"{self.name} from {self.house}"


def main():
    student = get_student()
    print(student) # 直接打印 student 对象


def get_student():
    name = input("Name: ")
    house = input("House: ")
    patronus = input("Patronus: ")
    return Student(name, house, patronus)


if __name__ == "__main__":
    main()
```
注意 `def __str__(self)` 方法提供了一种自定义对象“字符串表示”的方式。因此，作为程序员，你现在可以直接打印一个对象，并得到你想要的、格式化的输出，而不是一个默认的、难以理解的对象内存地址。

### 自定义方法

`__str__` 是 Python 类内置的特殊方法之一。我们当然也可以为类创建我们自己的方法！修改代码如下：

```python
class Student:
    def __init__(self, name, house, patronus=None):
        if not name:
            raise ValueError("Missing name")
        if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
            raise ValueError("Invalid house")
        # 增加对守护神的验证
        if patronus and patronus not in ["Stag", "Otter", "Jack Russell terrier"]:
            raise ValueError("Invalid patronus")
        self.name = name
        self.house = house
        self.patronus = patronus

    def __str__(self):
        return f"{self.name} from {self.house}"

    # 这是我们自定义的方法
    def charm(self):
        match self.patronus:
            case "Stag":
                return "🦌"
            case "Otter":
                return "🦦"
            case "Jack Russell terrier":
                return "🐶"
            case _:
                return "🪄"

def main():
    student = get_student()
    print("Expecto Patronum!")
    print(student.charm()) # 调用自定义的 charm 方法


def get_student():
    name = input("Name: ")
    house = input("House: ")
    # 如果用户不输入守护神，默认为 None
    patronus = input("Patronus: ") or None
    return Student(name, house, patronus)


if __name__ == "__main__":
    main()
```
注意我们是如何定义自己的 `charm` 方法的。与字典不同，类可以拥有内置的函数（即方法）。在这个例子中，我们定义的 `charm` 方法会根据学生的守护神返回不同的结果。另外，值得注意的是，Python 代码可以直接支持使用 emoji 表情符号。

在继续之前，让我们移除关于守护神的代码，以便专注于下一个概念。将代码修改回如下状态：

```python
class Student:
    def __init__(self, name, house):
        if not name:
            raise ValueError("Invalid name")
        if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
            raise ValueError("Invalid house")
        self.name = name
        self.house = house

    def __str__(self):
        return f"{self.name} from {self.house}"


def main():
    student = get_student()
    # 这一行会产生问题，因为它绕过了我们的验证逻辑
    # student.house = "Number Four, Privet Drive"
    print(student)


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return Student(name, house)


if __name__ == "__main__":
    main()
```
注意，当前我们的代码只有 `__init__` 和 `__str__` 两个方法。但是，在 `main` 函数中，我们仍然可以直接修改 `student.house`，这会绕过我们在 `__init__` 中设置的验证逻辑。这是一个安全隐患。

## 装饰器 (Decorators)

我们可以利用**属性 (Properties)** 和**装饰器 (Decorators)** 来加固我们的代码，防止属性被随意修改。在 Python 中，我们使用以 `@` 符号开头的函数“装饰器”来定义属性。

修改你的代码如下：

```python
class Student:
    def __init__(self, name, house):
        # 注意，这里的 self.name 和 self.house 赋值
        # 会自动调用下面的 setter 方法
        self.name = name
        self.house = house

    def __str__(self):
        return f"{self.name} from {self.house}"

    # house 属性的 Getter
    @property
    def house(self):
        return self._house

    # house 属性的 Setter
    @house.setter
    def house(self, house):
        if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
            raise ValueError("Invalid house")
        self._house = house


def main():
    student = get_student()
    print(student)


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return Student(name, house)


if __name__ == "__main__":
    main()
```

让我们来解析这段代码：
1.  我们在一个名为 `house` 的方法上方写了 `@property`。这样做就将 `house` 定义为了一个**属性**。
2.  一旦 `house` 成为一个属性，我们就能定义如何设置和检索与它关联的内部变量 `_house`。
3.  我们用 `@house.setter` 定义了一个名为 "setter" 的方法。每当有人尝试给 `house` 属性赋值时（例如 `student.house = "Gryffindor"`），这个 setter 方法就会被调用。
4.  在 setter 方法中，我们加入了验证逻辑。如果 `house` 的值无效，就抛出 `ValueError`；否则，就将这个值赋给内部变量 `_house`。
5.  **为什么是 `_house` 而不是 `house`？** 这里的 `house` 是我们定义的那个带有 getter 和 setter 功能的“公共属性接口”，而 `_house` 才是真正存储数据的“内部属性变量”。**前导下划线 `_` 是一种约定**，它告诉其他程序员：你不应该直接修改这个变量的值。`_house` 只应该通过 `house` 的 setter 方法来设置。
6.  `@property` 下的 `house` 方法充当了 "getter"。当用户访问 `student.house` 时，他们实际上是通过这个 getter 获取了 `_house` 的值。

我们也可以用同样的方式来保护学生的名字。将代码修改如下：

```python
class Student:
    def __init__(self, name, house):
        self.name = name
        self.house = house

    def __str__(self):
        return f"{self.name} from {self.house}"

    # name 属性的 Getter
    @property
    def name(self):
        return self._name

    # name 属性的 Setter
    @name.setter
    def name(self, name):
        if not name:
            raise ValueError("Invalid name")
        self._name = name

    # house 属性的 Getter
    @property
    def house(self):
        return self._house

    # house 属性的 Setter
    @house.setter
    def house(self, house):
        if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
            raise ValueError("Invalid house")
        self._house = house


def main():
    student = get_student()
    print(student)


def get_student():
    name = input("Name: ")
    house = input("House: ")
    return Student(name, house)


if __name__ == "__main__":
    main()
```
注意，与之前的代码非常相似，我们为 `name` 属性也提供了一个 getter 和一个 setter，确保名字不能为空。

你可以在 [Python 官方文档中学习更多关于方法和装饰器的内容](https://docs.python.org/3/library/functions.html#property)。

## 与课程先前内容的联系

虽然在课程的前半部分没有明确说明，但你其实**一直都在使用类和对象**。

*   如果你深入研究 `int` 的文档，你会发现它是一个类，拥有自己的构造方法。它是创建 `int` 类型对象的蓝图。 ([Python `int` 文档](https://docs.python.org/3/library/functions.html#int))
*   **字符串** `str` 也是一个类。当你使用 `str.lower()` 时，你实际上是在调用 `str` 类的一个方法。 ([Python `str` 文档](https://docs.python.org/3/library/stdtypes.html#str))
*   **列表** `list` 也是一个类。查看 `list` 的文档，你可以看到它包含的方法，如 `list.append()`。 ([Python `list` 文档](https://docs.python.org/3/library/stdtypes.html#list))
*   **字典** `dict` 同样是 Python 中的一个类。 ([Python `dict` 文档](https://docs.python.org/3/library/stdtypes.html#dict))

为了证明你一直在使用类，打开你的控制台，输入 `code type.py` 并编写以下代码来亲自验证：

```python
# 验证整数的类型
print(type(50))
# 输出: <class 'int'>
```
执行这段代码，它会显示 50 的类是 `int`。

我们也可以对 `str` 做同样的操作：
```python
print(type("hello, world"))
# 输出: <class 'str'>
```

对 `list` 也是如此：
```python
print(type([]))
# 输出: <class 'list'>
```
或者使用 `list` 类的构造函数：
```python
print(type(list()))
# 输出: <class 'list'>
```

最后是 `dict`：
```python
print(type({}))
# 输出: <class 'dict'>
```
或者使用 `dict` 类的构造函数：
```python
print(type(dict()))
# 输出: <class 'dict'>
```

## 类方法 (Class Methods)

有时候，我们希望为**类本身**添加功能，而不是为类的某个**实例**添加功能。这时就可以使用**类方法**。

`@classmethod` 装饰器可以用来定义一个作用于整个类的方法。

下面是一个**不使用**类方法的例子。在你的终端窗口，输入 `code hat.py` 并编写如下代码：

```python
import random

class Hat:
    def __init__(self):
        self.houses = ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]

    def sort(self, name):
        print(name, "is in", random.choice(self.houses))


hat = Hat() # 必须先创建一个 Hat 的实例
hat.sort("Harry") # 然后通过这个实例来调用 sort 方法
```
注意，我们必须先通过 `hat = Hat()` **实例化**一个帽子对象。分院的功能总是由 `Hat` 类的这个特定实例来处理。

然而，我们可能希望在不创建任何特定帽子实例的情况下运行分院功能（毕竟，分院帽只有一个！）。我们可以将代码修改如下：
```python
import random

class Hat:

    # 将 houses 变为类变量，而不是实例变量
    houses = ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]

    @classmethod
    def sort(cls, name):
        print(name, "is in", random.choice(cls.houses))


Hat.sort("Harry") # 直接通过类名调用 sort 方法
```
请注意这里的变化：
1.  `__init__` 方法被移除了，因为我们不再需要实例化一个帽子对象。
2.  因此，`self` 也不再需要，我们用 `cls` 来替代。`cls` 是一个约定俗成的参数名，**代表类本身**（在这里就是 `Hat` 类）。
3.  我们使用 `@classmethod` 装饰器来标记 `sort` 方法。
4.  最后，我们直接通过类名 `Hat.sort("Harry")` 来调用这个方法，注意 `Hat` 是大写的，因为它就是我们的类名。

现在让我们回到 `student.py` 文件，利用类方法来优化我们的代码：
```python
class Student:
    def __init__(self, name, house):
        self.name = name
        self.house = house

    def __str__(self):
        return f"{self.name} from {self.house}"

    @classmethod
    def get(cls):
        name = input("Name: ")
        house = input("House: ")
        # cls(name, house) 等同于 Student(name, house)
        return cls(name, house)


def main():
    # 直接通过 Student 类调用 get 方法来创建实例
    student = Student.get()
    print(student)


if __name__ == "__main__":
    main()
```
注意，我们移除了全局的 `get_student` 函数，并在 `Student` 类中创建了一个名为 `get` 的 `@classmethod`。这个方法现在可以被直接调用来创建并返回一个 `Student` 实例，而无需先拥有一个 `student` 对象。这使得创建学生的逻辑被更好地封装在了 `Student` 类内部。

## 静态方法 (Static Methods)

除了与实例绑定的普通方法和与类绑定的类方法之外，还有第三种方法：**静态方法**。

使用 `@staticmethod` 装饰器可以定义静态方法。它与类或实例的状态无关，更像是一个碰巧被放在类定义中的普通函数。虽然本课程不深入讲解，但你可以自行去了解静态方法与类方法的区别。

## 继承 (Inheritance)

**继承 (Inheritance)** 可能是面向对象编程中最强大的特性之一。

它允许你创建一个“子类”，这个子类可以**继承**另一个“父类”的所有方法和属性。

在终端中，执行 `code wizard.py` 并编写以下代码：

```python
class Wizard:
    def __init__(self, name):
        if not name:
            raise ValueError("Missing name")
        self.name = name

    ...


class Student(Wizard): # Student 继承自 Wizard
    def __init__(self, name, house):
        super().__init__(name) # 调用父类(Wizard)的 __init__ 方法
        self.house = house

    ...


class Professor(Wizard): # Professor 也继承自 Wizard
    def __init__(self, name, subject):
        super().__init__(name) # 调用父类(Wizard)的 __init__ 方法
        self.subject = subject

    ...


wizard = Wizard("Albus")
student = Student("Harry", "Gryffindor")
professor = Professor("Severus", "Defense Against the Dark Arts")
...
```
请注意：
1.  我们有一个顶层的 `Wizard` 类。
2.  我们还有 `Student` 和 `Professor` 类。
3.  学生和教授都有名字，而且他们都是巫师。因此，`Student` 和 `Professor` 都继承了 `Wizard` 类的特性。
4.  在“子类” `Student` 中，`super().__init__(name)` 这行代码会调用其“父类”（或“超类”）`Wizard` 的 `__init__` 方法，从而复用了设置名字的逻辑。
5.  最后几行代码分别创建了一个巫师、一个学生和一个教授的实例。

## 继承与异常

虽然我们刚刚才正式介绍继承，但其实你在使用异常处理时也一直在接触这个概念。

Python 的内置异常本身就是一个具有继承关系的层级结构，其中有子类、父类和祖父类。下面是这个层级结构的一部分：

```
BaseException
 +-- KeyboardInterrupt
 +-- Exception
      +-- ArithmeticError
      |    +-- ZeroDivisionError
      +-- AssertionError
      +-- AttributeError
      +-- EOFError
      +-- ImportError
      |    +-- ModuleNotFoundError
      +-- LookupError
      |    +-- KeyError
      +-- NameError
      +-- SyntaxError
      |    +-- IndentationError
      +-- ValueError
 ...
```
例如，`ZeroDivisionError` 继承自 `ArithmeticError`，而 `ArithmeticError` 又继承自 `Exception`。你可以在 [Python 官方文档中学习更多关于内置异常的内容](https://docs.python.org/3/library/exceptions.html#exception-hierarchy)。

## 运算符重载 (Operator Overloading)

某些运算符，如 `+` 和 `-`，可以被“重载”，这意味着我们可以让它们在处理我们自定义的对象时具有超越简单算术的新功能。

在你的终端窗口，输入 `code vault.py`，然后编写如下代码：

```python
class Vault:
    def __init__(self, galleons=0, sickles=0, knuts=0):
        self.galleons = galleons
        self.sickles = sickles
        self.knuts = knuts

    def __str__(self):
        return f"{self.galleons} Galleons, {self.sickles} Sickles, {self.knuts} Knuts"

    # 重载 '+' 运算符
    def __add__(self, other):
        galleons = self.galleons + other.galleons
        sickles = self.sickles + other.sickles
        knuts = self.knuts + other.knuts
        return Vault(galleons, sickles, knuts)


potter = Vault(100, 50, 25)
print(potter)

weasley = Vault(25, 50, 100)
print(weasley)

# 这里的 '+' 会自动调用 potter.__add__(weasley)
total = potter + weasley
print(total)
```
注意，`__add__` 这个特殊方法允许我们为 `Vault` 类的实例定义加法操作。当代码执行 `potter + weasley` 时，Python 会自动将其转换为 `potter.__add__(weasley)`。在这个方法中，`self` 指的是 `+` 号左边的对象（`potter`），而 `other` 指的是 `+` 号右边的对象（`weasley`）。

你可以在 [Python 官方文档中学习更多关于运算符重载的内容](https://docs.python.org/3/reference/datamodel.html#special-method-names)。

## 总结

通过本讲的学习，你已经掌握了面向对象编程这一强大的编程范式，解锁了全新的编程能力。

**核心概念回顾：**
*   **面向对象编程**
*   **类**
*   **`raise`**
*   **类方法**
*   **静态方法**
*   **继承**
*   **运算符重载**