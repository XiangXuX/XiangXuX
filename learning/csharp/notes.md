# C# 学习笔记 入门代码和 Visual Studio 常用功能的 Python 对照

今天开始学 C#。我更熟悉 Python，所以准备一边跟着教程学，一边把代码和 Python 对照起来。这份笔记记录目前学到的项目与输出、变量与运算、Visual Studio 常用功能、条件判断、数组基础、循环和字符串插值、函数、九九乘法表练习、字符串的格式化与操作、类和对象、继承、方法重写和多态、调试、F10、F11 和 Watch，以及枚举和模式匹配。

我一开始最想弄清楚的是：C#、.NET 和 Visual Studio 到底各自负责什么？后面又发现，即使两段代码看起来很像，类型和除法规则也可能不同。

## 第一节 创建项目和输出文字

### C# .NET 和 Visual Studio 的关系

| 名称 | 作用 |
| --- | --- |
| C# | 编程语言，规定变量、语句和程序结构的写法 |
| .NET | 开发平台，提供 SDK、编译工具、运行环境和常用功能库 |
| Visual Studio | 开发软件，用来编辑代码、管理项目、运行和调试 |
| Console App | 控制台应用，通过文字输入和输出与用户交互 |

主流 C# 开发通常使用 .NET。C# 有独立的语言标准，也允许其他实现；目前学习控制台程序、以后做 ASP.NET Core 后端，采用 C# 与 .NET 的组合就可以。

新建项目时，选择带 C# 标签的 **Console App**。它的结构简单，适合先练习语言和程序逻辑。Framework 下拉框选择的是项目面向的 .NET 版本；教程截图使用 .NET 7，我们当前按 .NET 10 学习。

平台与语言的关系参考 [微软 .NET 简介](https://learn.microsoft.com/en-us/dotnet/core/introduction) 和 [C# 语言规范](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/introduction)。

### 输出文字和注释

```csharp
// 单行注释：从 // 到本行末尾的内容不会作为代码执行
Console.WriteLine("Hello,world"); // 输出文字，然后换行
```

Python 对照：

```python
# Python 使用 # 写单行注释
print("Hello,world")  # 默认也会输出文字并换行
```

我第一次输入时写成了 `console.Weiteline(...)`。正确拼写是 **Console.WriteLine**：C、W、L 大写，WriteLine 是 Write 加 Line。C# 区分大小写，这种拼写差异会影响代码能否编译。

双引号里的内容是字符串。`()` 里放传给方法的参数，这里的参数是要输出的文字；末尾的 `;` 表示这条语句结束。

### 顶层语句

顶层语句（Top-level statements）允许直接在 `Program.cs` 的最外层写要执行的代码：

```csharp
Console.WriteLine("Hello,world");
```

传统结构会显式写出程序入口：

```csharp
using System; // 方便直接使用 System 命名空间中的 Console

class Program // 定义一个名为 Program 的类
{
    static void Main() // 程序入口；运行时从这里开始执行
    {
        Console.WriteLine("Hello,world");
    }
}
```

使用顶层语句时，编译器自动生成入口等结构。创建项目时，**Do not use top-level statements** 不勾选表示使用顶层语句，勾选则生成显式的 Program 和 Main 结构。

Python 脚本也可以直接写 `print(...)`，但两种语言处理程序入口的机制不同；这里是写法上的对照。参考 [微软 C# 概览](https://learn.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/overview)。

## 第二节 变量 数据类型和运算符

### 变量声明和类型

C# 常见的声明形式是 `类型 变量名 = 初始值;`。例如 `int i = 0;` 声明一个 int 类型的变量 i，并把它初始化为 0。这里的 `=` 是赋值。

| C# 类型或写法 | 含义 | Python 对照 |
| --- | --- | --- |
| short、int、long | 分别是 16、32、64 位的有符号整数 | 都可用 int；Python 的 int 支持任意精度，受可用内存限制 |
| double | 64 位二进制浮点数 | Python 内置 float 通常使用双精度，接近这一类型 |
| float | 32 位二进制浮点数 | Python 内置 float 的精度不同，没有直接等价的内置 32 位浮点类型 |
| decimal | 十进制数，适合需要十进制精度的计算 | decimal.Decimal；精度和范围规则并非完全相同 |
| bool | 布尔值 true 或 false | bool，写作 True 或 False |
| char | 一个 UTF-16 代码单元；图中的 A、a 都能用 char 表示 | Python 没有独立 char 类型，可用一个字符的 str |
| string | 字符串，使用双引号 | str，可使用单引号或双引号 |
| const | 声明常量，初始化后不能重新赋值 | 常用全大写名字表达约定，Python 运行时不会因此禁止赋值 |
| var | 编译器根据初始表达式推断局部变量的类型 | 外观接近 Python 赋值，但 C# 推断后的变量类型仍然固定 |

整数的位数和浮点数的后缀规则参考 [C# 整数类型](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types) 和 [C# 浮点数类型](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types)。Python 类型参考 [Python 内置类型](https://docs.python.org/3/library/stdtypes.html) 和 [decimal 模块](https://docs.python.org/3/library/decimal.html)。

### 截图代码的 C# 注释版

下面合并了三张截图的代码。截图中给 const 常量重新赋值的那一行会报编译错误，因此这里把它注释掉。

```csharp
// 整数：类型决定能存储的范围
int i = 0;       // 32 位有符号整数
short sh = 0;    // 16 位有符号整数
long lo = 0;     // 64 位有符号整数

// 浮点数：变量类型和数字后缀是两个相关但不同的概念
double d = 0;    // 整数 0 可以自动转换为 double
double d1 = 0d;  // d 后缀明确指定这个数字是 double

float f = 0;     // 整数 0 可以自动转换为 float
float f1 = 0f;   // f 后缀明确指定这个数字是 float

// 十进制数
decimal dm1 = 0;  // 整数 0 可以自动转换为 decimal
decimal dm2 = 0m; // m 后缀明确指定这个数字是 decimal

// 布尔值：C# 的 true、false 都小写
bool b = false;

// 字符：使用单引号；这里分别是大写 A 和小写 a
char c1 = 'A';
char c2 = 'a';

// 字符串：使用双引号
string s1 = "this is a string";

// const 表示常量，必须初始化，之后不能重新赋值
const string s2 = "this is a string";
// s2 = "string"; // 如果取消注释，会因修改常量而报编译错误

// 字符串 + 数字：这里会把数字转换成文字再拼接
Console.WriteLine("i = " + i); // 输出：i = 0

// {0}、{1} 是位置占位符，对应格式字符串后面的第 1、第 2 个参数
Console.WriteLine("i = {0}, {1}", i, "string");
// 输出：i = 0, string

// var 表示让编译器推断类型；类型确定后仍然固定
var r1 = (d + f) * 4 / 2;
// 先计算括号，再乘除；因为参与计算的 d 是 double，r1 也是 double
// 此处 d 和 f 都是 0，所以结果是 0

var r2 = 14 / 3;  // 两个整数相除，结果是整数 4，截去小数部分
var r3 = 14 % 3;  // % 取余数：14 = 3 * 4 + 2，所以结果是 2
var r4 = 14d / 3; // double 除法，结果约为 4.666666666666667
var r5 = 14f / 3; // float 除法，结果约为 4.6666665，精度不同

var r6 = s1 + s2; // 拼接两个字符串，不会自动添加空格或换行
// r6 的内容：this is a stringthis is a string

Console.WriteLine("s1 + s2 = {0}", r6);
// 输出：s1 + s2 = this is a stringthis is a string

var r7 = s1 + d + f + i + c1 + b;
// 从最左边的 s1 开始就是字符串拼接，后面的值依次转换成文字
// 当前这些值拼成：this is a string000AFalse
// 布尔值 false 转为文字时显示为 False
```

**后缀标记的是数字本身的类型**：`0d` 是 double，`0f` 是 float，`0m` 是 decimal。虽然 `float f = 0;` 合法，带小数的数字如 `0.1` 默认是 double，要写 float 时通常使用 `0.1f`。

**var 会省略类型名字，但不会取消类型检查。** 例如 `var count = 1;` 会推断为 int，之后不能直接写 `count = "hello";`。而 const 的约束是常量不能重新赋值。参考 [var 的类型推断](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables) 和 [const 常量](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/const)。

### 对应的 Python 注释版

下面对应的是相同的学习内容。C# float 和 Python float 的精度不同，因此小数运算的写法对照不代表精度完全相同。

```python
from decimal import Decimal  # 导入十进制数类型

# Python 这些整数都使用 int，不区分 short、int、long
i = 0
sh = 0
lo = 0

# Python 内置 float 通常接近 C# 的 double
d = 0.0
d1 = 0.0

# 这里用 Python float 展示对应的值，不能等同于 C# 的 32 位 float
f = 0.0
f1 = 0.0

# Python 没有 0m 这样的字面量后缀，要创建 Decimal 对象
dm1 = Decimal("0")
dm2 = Decimal("0")

b = False  # Python 的 True、False 首字母大写

# 单字符也是 str；Python 的单引号和双引号都能表示字符串
c1 = "A"
c2 = "a"

s1 = "this is a string"

# 用全大写名字约定这是常量，对应 C# 的 s2
S2 = "this is a string"
# S2 = "string"  # Python 允许运行，但违背了这里的常量约定

# Python 不会自动让字符串与整数直接相加，使用 str() 转成文字
print("i = " + str(i))  # 输出：i = 0

# 位置占位符：.format() 把参数填入 {0}、{1}
print("i = {0}, {1}".format(i, "string"))
# 输出：i = 0, string

r1 = (d + f) * 4 / 2  # 结果是 0.0

# 对截图中的这组正整数，用 // 得到与 C# 整数除法相同的结果
r2 = 14 // 3  # 4
r3 = 14 % 3   # 2

r4 = 14.0 / 3  # 约 4.666666666666667
r5 = 14.0 / 3  # 使用 Python float，不是对 C# float 精度的精确复现

r6 = s1 + S2  # 字符串拼接，没有额外空格
print("s1 + s2 = {0}".format(r6))

# f-string 会把花括号内的值格式化成文字再拼接
# :g 是一般数值格式；在此将 0.0 显示成 0，使这组示例的文字一致
r7 = f"{s1}{d:g}{f:g}{i}{c1}{b}"
# r7 的内容：this is a string000AFalse
```

### 除法和拼接需要特别留意

| 操作 | C# | Python |
| --- | --- | --- |
| 两个整数相除 | `14 / 3` 得到 `4` | `14 / 3` 得到约 `4.666666666666667` |
| 当前正整数示例的整数商 | `14 / 3` | `14 // 3` |
| 一个操作数是浮点数 | `14d / 3` 得到小数结果 | `14.0 / 3` 得到小数结果 |
| 字符串与数字组合 | `"i = " + i` 自动把 i 转成文字 | `"i = " + str(i)`，或 `f"i = {i}"` |
| 按位置填入文字 | `Console.WriteLine("i = {0}", i);` | `print("i = {0}".format(i))` |

C# 的整数除法向零截断，Python 的 `//` 向下取整。例如 C# 的 `-14 / 3` 是 `-4`，Python 的 `-14 // 3` 是 `-5`。上面的 `14 // 3` 对照只针对这组正整数；负数的取余规则也有差异。

C# 的字符串拼接与位置占位符是两种写法：前者使用 `+`，后者用 `{0}`、`{1}` 指定参数位置。这些索引从 0 开始。参考 [C# 算术运算符](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators)、[字符串加法](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/addition-operator) 和 [.NET 复合格式化](https://learn.microsoft.com/en-us/dotnet/standard/base-types/composite-formatting)。

我目前会重点检查变量的类型、除法两边的类型，以及字符串是否需要转换。用 Python 做对照能帮助理解，也需要把这些规则差异单独记下来。

## 第三节 Visual Studio 常用功能

### 1 Code Search

Code Search 是 Visual Studio 的代码导航功能，用来快速查找文件、类型和成员。它属于编辑器功能；Python 语言本身没有对应语句，写 Python 时要看所用编辑器提供哪些导航工具。

截图中输入 `program`，搜索结果找到了 `Program.cs`，下方显示文件内容的预览。

1. 按 **Ctrl + T** 打开 Code Search。
2. 输入文件名或代码名称，例如 `program`。
3. 选中结果，按 **Enter** 跳转到对应位置。

| 筛选 | 搜索内容 | 输入示例 |
| --- | --- | --- |
| files，前缀 `f:` | 文件名 | `f:Program` |
| types，前缀 `t:` | 类、接口等类型的名称 | `t:Student`，前提是项目中有这个类型 |
| members，前缀 `m:` | 方法、属性等成员的名称 | `m:Calculate`，前提是项目中有这个成员 |

旁边的 **Feature Search** 用来搜索 Visual Studio 的菜单、选项和功能，常用快捷键是 **Ctrl + Q**。这些快捷键按默认设置记录，自定义键位可能不同。

参考 [微软 Visual Studio 搜索说明](https://learn.microsoft.com/en-us/visualstudio/ide/visual-studio-search?view=visualstudio)。

### 2 Git Changes

Git Changes（Git 更改）是 Visual Studio 中管理代码版本的窗口，可以查看修改、选择要提交的内容，并创建提交。Git 也能管理 Python 项目，操作原理相同。

| 名称 | 含义 | 对应的 Git 命令示例 |
| --- | --- | --- |
| Changes | 已修改、尚未暂存的文件 | `git status` 查看状态 |
| 查看差异（Diff） | 对照修改前后的代码，确认改了什么 | `git diff` 查看尚未暂存的差异 |
| Stage / Staged Changes | 暂存：选择准备放入下一次提交的修改 | `git add Program.cs` |
| Commit Staged | 把已暂存的修改记录为本地仓库中的一次提交 | `git commit -m "添加 Hello World 输出"` |
| Push | 把本地提交发送到已配置的远程仓库，例如 GitHub | `git push` |

初学时可以按这个顺序操作：

1. 在 Changes 中双击文件，查看代码差异。
2. 点击文件旁的 **+**，将准备提交的修改放进 Staged Changes。
3. 写清楚这次改了什么，再点击 **Commit Staged**。
4. 如果已经配置远程仓库，并且需要上传提交，再执行 **Push**。

**保存文件、Commit 和 Push 是三个动作。** 保存把编辑内容写入文件；Commit 记录本地版本；Push 把提交发送到远程仓库。Commit 后可以暂时不 Push。

参考 [微软 Git 提交说明](https://learn.microsoft.com/en-us/visualstudio/version-control/git-make-commit?view=visualstudio)和 [Visual Studio Git 概览](https://learn.microsoft.com/en-us/visualstudio/version-control/git-with-visual-studio?view=visualstudio)。

### 3 Ctrl 键和窗口切换

键盘上写的是 **Ctrl**，全称 Control。它通常与其他按键组合使用，组合不同，触发的操作也不同。

截图显示的是 **IDE Navigator**，也就是 Visual Studio 的文件和工具窗口切换器。

| 截图中的名称 | 中文含义 | 示例 |
| --- | --- | --- |
| Active Tool Windows | 已打开的工具窗口 | Solution Explorer（解决方案资源管理器）、Git Changes、Diagnostic Tools（诊断工具） |
| Active Files | 已打开的文件 | `Program.cs`、`FileName.cs` |

| 快捷键 | 用途 |
| --- | --- |
| **Ctrl + Tab** | 打开切换器，在已打开的文件之间选择 |
| **Ctrl + Shift + Tab** | 在文件列表中反向选择 |
| **Alt + F7** | 打开切换器，选择已打开的工具窗口 |
| **Ctrl + T** | 打开前面记录的 Code Search，搜索文件、类型或成员 |
| **Ctrl + Q** | 打开 Feature Search，搜索 Visual Studio 功能 |

切换文件时，先按住 **Ctrl**，再按 **Tab**；继续按 Tab 可以选择其他文件。选中目标后松开 Ctrl，即可切换过去，也可以按 Enter 确认。切换工具窗口时，可按住 **Alt** 并反复按 **F7** 选择目标。

这些是 Visual Studio 的操作，不是 C# 语法。写 Python 时，快捷键由使用的编辑器决定，不能直接照搬；不同 Visual Studio 键盘方案或自定义设置也可能改变快捷键。

参考 [微软窗口和文件导航说明](https://learn.microsoft.com/en-us/visualstudio/ide/how-to-move-around-in-the-visual-studio-ide?view=visualstudio)和 [键盘操作说明](https://learn.microsoft.com/en-us/visualstudio/ide/reference/how-to-use-the-keyboard-exclusively?view=visualstudio)。

### 4 注释和取消注释的快捷键

截图中的 **Ctrl + K，Ctrl + C** 是 Visual Studio 的注释快捷键。先选中要注释的代码，再依次按这两组键：先 Ctrl + K，再 Ctrl + C；两组键按顺序使用。

| 快捷键 | 作用 |
| --- | --- |
| **Ctrl + K，再 Ctrl + C** | 注释选中的代码；本章 C# 代码会加上 `//` |
| **Ctrl + K，再 Ctrl + U** | 取消选中代码的注释 |

这属于编辑器操作。C# 单行注释用 `//`，Python 用 `#`；Python 编辑器的快捷键要按所用编辑器和键盘设置来确认。这里按 Visual Studio 默认快捷键记录。

参考 [微软 Visual Studio 快捷键说明](https://learn.microsoft.com/en-us/visualstudio/ide/default-keyboard-shortcuts-in-visual-studio?view=visualstudio)。


## 第四节 条件判断：if、else 和 switch

`if` 表示“如果条件成立，就执行下面的代码”；`else` 表示“否则，执行另一组代码”。

截图中有三个判断：前两行分别检查 `b1` 和 `!b1`；第三个判断检查 `b1 && b2`，并带有一个 `else` 分支。前两行是两个独立的 `if`，最后的 `else` 与第三个 `if` 配对。

### C# 写法和逐行注释

截图没有显示 `b1`、`b2` 的初始值。下面为了演示，设 `b1 = true`、`b2 = false`；这段代码可以作为独立的顶层语句示例。

```csharp
bool b1 = true;  // 定义布尔变量 b1，值为真；Python 对应 b1 = True
bool b2 = false; // 定义布尔变量 b2，值为假；Python 对应 b2 = False

// b1 为 true 时，执行这一条输出语句。
// 这里只有一条语句，所以截图省略了大括号。
if (b1) Console.WriteLine("b1 is true");

// ! 表示逻辑取反：!true 是 false，!false 是 true。
// 因此，这一行会在 b1 为 false 时输出；Python 对应 not b1。
if (!b1) Console.WriteLine("b1 is false");

if (b1 && b2) // && 表示“并且”：b1 和 b2 都为 true，条件才成立。
{ // 大括号标出这一组代码的开始。
    Console.WriteLine("b1 is true"); // 条件成立时，输出第一行。
    Console.WriteLine("b2 is true"); // 接着输出第二行。
} // if 分支的代码块结束。
else // b1 && b2 为 false 时，执行下面这组代码。
{
    Console.WriteLine("b1 && b2 is false"); // 至少有一个变量为 false。
} // else 分支的代码块结束。
```

### 对应的 Python 写法

```python
b1 = True   # Python 的布尔值 True 首字母大写。
b2 = False  # Python 的布尔值 False 首字母大写。

if b1:  # Python 的 if 条件后面写冒号。
    print("b1 is true")  # 缩进表示这行属于上面的 if。

if not b1:  # not 对应 C# 的 !，表示取反。
    print("b1 is false")

if b1 and b2:  # and 对应本例中 C# 的 &&：两个布尔条件都成立。
    print("b1 is true")  # 两行缩进相同，都属于 if 分支。
    print("b2 is true")
else:  # else 与它对应的 if 对齐；条件不成立时执行这个分支。
    print("b1 && b2 is false")  # 引号里是输出文字，所以保留截图原文。
```

这组初始值下，两段代码都会输出：

```text
b1 is true
b1 && b2 is false
```

第一行来自最前面的 `if (b1)`。第二个判断 `!b1` 不成立，因此跳过它的输出。最后，`b1 && b2` 不成立，所以执行 `else`。

### 两种语言的写法对照

| 要表达的意思 | C# | Python |
| --- | --- | --- |
| 真 / 假 | `true` / `false` | `True` / `False` |
| 如果 b1 成立 | `if (b1)` | `if b1:` |
| 如果 b1 不成立 | `if (!b1)` | `if not b1:` |
| b1 和 b2 都成立 | `b1 && b2` | `b1 and b2`，本例的两个变量都是布尔值 |
| 否则 | `else` | `else:` |
| 哪些语句属于分支 | 用 `{ }` 包住代码块 | 用缩进划分代码块 |
| 单条输出语句结束 | `Console.WriteLine(...);`，末尾有分号 | `print(...)`，通常不写分号 |

C# 的 `if` 条件需要得到布尔结果；Python 还可以判断数字、字符串等对象的真值。这里用布尔变量对照，行为最容易对应。

### && 的四种结果

| b1 | b2 | b1 && b2 | 执行最后哪个分支 |
| --- | --- | --- | --- |
| `true` | `true` | `true` | if，输出两行 |
| `true` | `false` | `false` | else |
| `false` | `true` | `false` | else |
| `false` | `false` | `false` | else |

`b1 && b2` 为假，只能说明**至少一个为假**，不能说两者都为假。C# 的 `&&` 和 Python 的 `and` 都会短路：左边已经为假时，不再计算右边。

虽然 C# 允许单条语句的分支省略大括号，初学时保留 `{ }` 更容易看清范围。`if (条件)` 后面不要直接加分号；分号放在 `Console.WriteLine(...)` 这样的语句末尾。

参考 [C# if / else 文档](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/selection-statements)、[C# 布尔逻辑运算符](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/boolean-logical-operators)和 [Python if 语句文档](https://docs.python.org/3/reference/compound_stmts.html#if)。

### 大括号：划分一起执行的代码块

C# 的 `{ }` 表示一个代码块。`{` 标出开始，`}` 标出结束；放在同一对大括号中的语句，属于同一组。这里每个例子都按各自设定的变量值单独运行。

| 符号 | 在本节中的作用 | 示例 |
| --- | --- | --- |
| 小括号 `( )` | 包住 if 的判断条件 | `if (b1)` |
| 大括号 `{ }` | 包住属于这个分支的一组语句 | 条件成立后执行两条输出语句 |
| 分号 `;` | 结束普通语句 | `Console.WriteLine("A");` |

```csharp
bool b1 = false; // 本例的条件为假。

if (b1)
{ // if 代码块开始：下面两条语句都受 b1 控制。
    Console.WriteLine("A");
    Console.WriteLine("B");
} // if 代码块结束。

Console.WriteLine("C"); // 在这对大括号外，执行完 if 后会继续执行。
```

本例只输出 `C`。把 `b1` 改为 `true`，就会依次输出 `A`、`B`、`C`。

对应的 Python：

```python
b1 = False

if b1:  # 冒号表示后面开始一个代码块。
    print("A")  # 缩进的两条语句都属于 if。
    print("B")

print("C")  # 缩进退回，表示已经离开 if 代码块。
```

在这些 C# 的 if 语句中，代码的归属看大括号，缩进帮助阅读。Python 的缩进直接决定代码归属。

**C# 省略大括号时，if 只控制紧接着的一条语句。** 截图顶部的 `if (b1) Console.WriteLine(...);` 只有一条输出，所以可以省略。如果要让两条输出都受这个条件控制，就把它们一起放进 `{ }`。初学时，即使只有一条语句，也可以保留大括号。

### 截图里的嵌套 if / else

第一张新截图的下半部分，在 `if (b1)` 里面又写了 `if (b2)`，这叫嵌套判断：先判断 b1；只有 b1 为真，才进入代码块继续判断 b2。

下面补全截图中省略的大括号，判断逻辑保持相同。截图未显示变量初始值，本例设 `b1 = true`、`b2 = false`。

```csharp
bool b1 = true;
bool b2 = false;

Console.WriteLine("boolean test"); // 在判断之外，先打印这个提示。

if (b1) // 外层判断：b1 是否为真？
{ // 外层 if 代码块开始。
    if (b2) // 内层判断：进入外层后，再判断 b2。
    {
        Console.WriteLine("b1 && b2 is true"); // 两者都为真。
    }
    else // 内层 else，对应 if (b2)。
    {
        Console.WriteLine("b1 is true, b2 is false");
    }
} // 外层 if 的整个代码块结束。
else // 外层 else，对应 if (b1)。
{
    Console.WriteLine("b1 is false"); // b1 为假时走这里。
}
```

对应的 Python：

```python
b1 = True
b2 = False

print("boolean test")

if b1:  # 外层 if。
    if b2:  # 多缩进一层，表示这是外层 if 里面的判断。
        print("b1 && b2 is true")
    else:  # 与内层 if 对齐，对应 if b2。
        print("b1 is true, b2 is false")
else:  # 与外层 if 对齐，对应 if b1。
    print("b1 is false")
```

本例输出：

```text
boolean test
b1 is true, b2 is false
```

| b1 | b2 | 嵌套判断的输出，不含开头提示 |
| --- | --- | --- |
| `true` | `true` | `b1 && b2 is true` |
| `true` | `false` | `b1 is true, b2 is false` |
| `false` | 任意布尔值 | `b1 is false`，不会进入内层判断 |

看嵌套代码时，先找外层大括号，再看里面的判断。Python 则先看缩进层级：一个 else 与它对应的 if 对齐。

### switch：按不同的值选择分支

第二张新截图使用 `switch` 检查同一个变量的值，再选择对应的 `case`。

```csharp
int i3 = 3; // 定义整数变量 i3，当前值为 3。

switch (i3) // 检查 i3 的值。
{ // switch 中各个分支的范围开始。
    case 1: // 当 i3 等于 1 时，执行这一组语句。
        Console.WriteLine("i3 = 1");
        break; // 退出这个 switch，继续执行 switch 后面的代码。

    case 2: // 当 i3 等于 2 时，执行这一组语句。
        Console.WriteLine("i3 = 2");
        break;
} // switch 结束。
```

**按照截图的值 `i3 = 3`，这一段不会输出文字。** 因为它没有匹配 `case 1` 或 `case 2`，也没有 `default` 分支。

本例可以用 Python 的 if / elif 表达同样的判断：

```python
i3 = 3  # 与截图保持相同的值。

if i3 == 1:  # == 表示比较是否相等。
    print("i3 = 1")
elif i3 == 2:  # elif 表示“否则，如果这个条件成立”。
    print("i3 = 2")

# 没有 else；i3 为 3 时两个条件都不成立，所以没有输出。
```

`=` 是赋值，例如 `i3 = 3`；`==` 是比较，例如 `i3 == 1`。本例的 Python 不需要写 `break`，选中的 if / elif 分支执行完后，就继续执行整个判断后面的代码。

| C# 名称 | 本例含义 | Python 对照 |
| --- | --- | --- |
| `switch (i3)` | 根据 i3 的值选择分支 | 用 if / elif 逐个比较 i3 |
| `case 1:` | i3 等于 1 时的分支 | `if i3 == 1:` |
| `case 2:` | i3 等于 2 时的分支 | `elif i3 == 2:` |
| `break;` | 退出本例的 switch | if / elif 中不需要对应语句 |
| `default:` | 没有匹配其他 case 时执行 | 在末尾加 `else:` |

如果希望没有匹配项时也有输出，可以在 switch 的大括号内、`case 2` 分支之后添加：

```csharp
default: // 未匹配到其他 case 时，执行这里。
    Console.WriteLine("其他数字");
    break;
```

Python 对应在已有的 if / elif 后面添加：

```python
else:
    print("其他数字")
```

上面两个小片段需要接在各自已有的判断中。添加后，`i3 = 3` 会输出 `其他数字`。

参考 [C# 代码块和语句规范](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/statements#133-blocks)、[C# 条件判断文档](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/selection-statements)和 [Python if / elif 教程](https://docs.python.org/3/tutorial/controlflow.html#if-statements)。

### 重点：case、break，以及 Python 为什么不用 break

`switch (i3)` 先取得 i3 的值，再选择匹配的 case。本例的 `case 1:` 表示 i3 等于 1，`case 2:` 表示 i3 等于 2；冒号后面是这个分支要执行的语句。

**这段 C# 代码中的 `break;` 会退出当前 switch，然后继续执行 switch 后面的代码。** 本例各个 case 使用 break 收尾。C# 不允许一个含有可执行语句的 case 直接接着进入下一个 case；例如删掉截图中 case 1 后的 break，会导致编译错误。实际代码也可能用 return、throw 等方式结束分支，本节先掌握 break。

为了看清 break 之后会怎样，下面把 i3 设为 1，并在 switch 后加一行输出：

```csharp
int i3 = 1; // 本例改为 1，进入 case 1。

switch (i3)
{
    case 1:
        Console.WriteLine("i3 = 1");
        break; // 离开整个 switch，继续执行大括号后面的代码。

    case 2:
        Console.WriteLine("i3 = 2");
        break;
}

Console.WriteLine("继续执行后面的代码"); // break 之后仍会执行到这里。
```

对应的 Python：

```python
i3 = 1

if i3 == 1:
    print("i3 = 1")
elif i3 == 2:
    print("i3 = 2")

print("继续执行后面的代码")  # 分支执行完，继续往下执行。
```

两段代码都输出：

```text
i3 = 1
继续执行后面的代码
```

**Python 这段代码不用 break，是因为 if / elif 本来就只执行第一个条件成立的分支。** 执行完选中的分支，就继续执行整个判断之后的语句。这里选中 `if i3 == 1` 后，不会再执行下面的 elif 分支。

**Python 也有 break。** 它用在 for / while 循环中，用来提前退出所在的循环；单独的 if / elif 结构中不能放一个脱离循环的 break。后面学习循环时，再具体对照它的用法。

| 使用场景 | break 的作用或是否需要 |
| --- | --- |
| 本例 C# 的 switch / case | 用 break 退出 switch；每个示例分支都用它收尾 |
| 本例 Python 的 if / elif | 不需要 break；选中的分支执行完后继续往下执行 |
| Python 的 for / while 循环 | 可以用 break 提前退出循环 |

参考 [C# break 语句规范](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/statements#13102-the-break-statement)和 [Python 控制流程教程](https://docs.python.org/3/tutorial/controlflow.html)。

### default：没有匹配到前面的 case 时执行

新截图在原来的 switch 中增加了 `default`。沿用本例的 `i3 = 3`，它会进入这个兜底分支。

```csharp
int i3 = 3;

switch (i3)
{
    case 1: // i3 等于 1 时执行。
        Console.WriteLine("i3 = 1");
        break;

    case 2: // i3 等于 2 时执行。
        Console.WriteLine("i3 = 2");
        break;

    default: // 没有匹配到上面的 case 1 或 case 2 时执行。
        Console.WriteLine("i3 > 2"); // 保留截图原文；这只是输出文字。
        break; // 退出 switch。
}
```

对应的 Python：

```python
i3 = 3

if i3 == 1:
    print("i3 = 1")
elif i3 == 2:
    print("i3 = 2")
else:  # 对应这个 switch 的 default。
    print("i3 > 2")  # 保留截图中的输出文字。
```

本例输出 `i3 > 2`。

**default 的条件是“没有匹配到其他 case”。** 这里除了 3，0、-1 等值也会进入 default。引号里的 `"i3 > 2"` 只是作者写的文字，不是程序实际检查的条件；如果要表达通用的兜底结果，写成 `"i3 既不是 1，也不是 2"` 更准确。

### switch 表达式：把选出的结果赋给变量

第二张截图是 **switch 表达式**。它根据匹配结果产生一个值，再将这个值赋给 `s5`。

模式匹配（pattern matching）表示检查一个值是否符合某种模式。本图只展示简单的整数匹配：`1` 和 `2` 是常量模式，`_` 是匹配任何值的弃元模式。

```csharp
int i3 = 3; // 为了让这个示例可以单独运行，补上变量定义。

var s5 = i3 switch // 根据 i3 的值，选择一个字符串赋给 s5。
{
    1 => "i3 is 1", // 匹配到 1，整个表达式的结果就是这个字符串。
    2 => "i3 is 2", // 匹配到 2，结果就是这个字符串。
    _ => "i3 > 2"   // _ 放在最后兜底：其余值都匹配这里。
}; // 大括号结束表达式；分号结束整个赋值语句。

Console.WriteLine(s5); // 为了查看结果而补上的输出语句。
```

| 写法 | 在这段代码中的含义 |
| --- | --- |
| `var s5` | 定义变量，编译器推断类型；这里各个结果都是字符串，所以 s5 的类型是 string |
| `i3 switch` | 检查 i3，让 switch 表达式选出一个结果 |
| `1 => "i3 is 1"` | 左边的模式匹配成功，就以右边的字符串作为结果 |
| `=>` | 在此处连接匹配模式与结果表达式 |
| `,` | 分隔各个匹配分支；最后一个分支的逗号可以省略 |
| `_ => ...` | 本例放在最后的兜底分支，与前面 default 的作用相近 |
| `};` | `}` 结束 switch 表达式，`;` 结束赋值语句 |

**这段 switch 表达式不用 break。** 匹配到一个分支后，它直接产生那个分支的值，完成 `s5` 的赋值。

截图本身只给 `s5` 赋值，没有打印。补上 `Console.WriteLine(s5);` 后，才会看到本例的结果 `i3 > 2`。这里的 `_` 同样匹配所有剩余的值，包括 0、-1；字符串内容仍然只是演示用的文字。

先用熟悉的 Python if / elif 表达相同的赋值：

```python
i3 = 3

if i3 == 1:
    s5 = "i3 is 1"  # 匹配到 1，给 s5 赋这个字符串。
elif i3 == 2:
    s5 = "i3 is 2"  # 匹配到 2，给 s5 赋这个字符串。
else:
    s5 = "i3 > 2"  # 其余值，给 s5 赋这个字符串；保留截图原文。

print(s5)  # 对应为了看结果而补上的 Console.WriteLine(s5)。
```

### Python 也有 match / case

Python 从 **3.10** 起支持 `match / case`。在这个整数匹配例子中，也可以这样写：

```python
i3 = 3

match i3:  # 根据 i3 的值做模式匹配。
    case 1:
        s5 = "i3 is 1"
    case 2:
        s5 = "i3 is 2"
    case _:  # _ 是通配模式，放在最后匹配其余值。
        s5 = "i3 > 2"  # 保留截图原文。

print(s5)
```

这里也不用 break，因为 match 只执行第一个匹配成功的 case 分支，然后继续执行整个 match 后面的语句。

Python 的 match 是一条语句，因此本例在各个 case 内给 s5 赋值；C# 的 switch 表达式本身就能产生一个值，用于赋值。这两种写法在本例中得到相同结果，语法机制有所区别。

| 写法 | 本例中做什么 | 是否写 break |
| --- | --- | --- |
| C# `switch (...) { case ... }` 语句 | 选择并执行 case 中的语句 | 本例用 break 结束各分支 |
| C# `i3 switch { ... => ... }` 表达式 | 选出一个值，赋给 s5 | 不写 |
| Python `if / elif / else` | 根据条件，在分支中赋值或输出 | 不写 |
| Python `match / case`，3.10 起 | 根据模式，在分支中赋值或输出 | 不写 |

参考 [C# switch 表达式文档](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/switch-expression)和 [Python match 语句文档](https://docs.python.org/3/reference/compound_stmts.html#the-match-statement)。

## 第五节 List 章节的数组基础

这一章先从数组（Array）开始。截图中出现了 `int[]`、`int[,]` 和 `string[]`。下面用 Python 原生列表和嵌套列表表达相同的样例数据；它们与 C# 数组在长度和类型要求上有所区别。

### 1 一维整数数组

```csharp
// int[] 表示整数数组；ints1 是变量名。
// = 后面的 { } 列出初始元素，依次是 1、2、3。
int[] ints1 = { 1, 2, 3 };

// new int[3] 创建一个长度为 3 的整数数组。
// 没有逐个指定元素值时，int 元素的默认值都是 0。
int[] ints2 = new int[3]; // 内容是 0、0、0。

// Length 是数组的元素总数，本例为 3；属性后面不写 ()。
Console.WriteLine("ints1 length is {0}", ints1.Length);

// 索引从 0 开始；ints1[1] 取第二个元素，因此是 2。
Console.WriteLine("ints1[1] is {0}", ints1[1]);
```

这里的 `new int[3]` 表示创建三个位置，不是把数字 3 作为唯一元素放进去。`ints2` 创建后已经有三个整数元素，并且它们的值都为 0。

对应的 Python：

```python
ints1 = [1, 2, 3]  # 创建一个列表，包含三个整数。
ints2 = [0] * 3   # 将 [0] 重复三次，得到 [0, 0, 0]。

print("ints1 length is {0}".format(len(ints1)))  # len 取得元素个数。
print("ints1[1] is {0}".format(ints1[1]))       # 索引 1 是第二个元素。
```

两段代码都会输出：

```text
ints1 length is 3
ints1[1] is 2
```

`ints1` 的三个位置分别是：索引 0 对应 1，索引 1 对应 2，索引 2 对应 3。长度是 3，有效索引是 0、1、2。

### 2 二维整数数组

```csharp
// int[,] 表示二维整数数组，需要两个索引来定位元素。
int[,] ints3 =
{ // 外层大括号列出整个二维数组的初始数据。
    { 1, 2, 3 }, // 第一行，行索引为 0。
    { 4, 5, 6 }  // 第二行，行索引为 1。
}; // 完成数组初始化，并用分号结束这条声明语句。

// 两个索引依次是行和列，行、列都从 0 开始。
Console.WriteLine("ints3[1,1] is {0}", ints3[1, 1]); // 第二行第二列：5。
Console.WriteLine("ints3[1,2] is {0}", ints3[1, 2]); // 第二行第三列：6。
```

把这组数据按行、列展开：

| 行索引 / 列索引 | 0 | 1 | 2 |
| --- | --- | --- | --- |
| 0 | 1 | 2 | 3 |
| 1 | 4 | **5** | **6** |

因此，`ints3[1, 1]` 是 5，`ints3[1, 2]` 是 6。这里是一个 2 行、3 列的矩形数组。

对应的 Python 使用嵌套列表：

```python
ints3 = [
    [1, 2, 3],  # 第一行，行索引 0。
    [4, 5, 6]   # 第二行，行索引 1。
]

# 输出提示文字沿用截图；Python 实际取值使用 [行][列]。
print("ints3[1,1] is {0}".format(ints3[1][1]))  # 先取第二行，再取第二个元素。
print("ints3[1,2] is {0}".format(ints3[1][2]))  # 先取第二行，再取第三个元素。
```

两段代码都会输出：

```text
ints3[1,1] is 5
ints3[1,2] is 6
```

**C# 二维数组用 `[行, 列]`，Python 原生嵌套列表用 `[行][列]`。** 前者是二维数组，后者是一个列表里面放两个列表。

本例的 `ints3.Length` 是元素总数 6；Python 的 `len(ints3)` 是外层列表的长度 2。到了二维数据，这两个长度不能直接当成同一个概念。

这里的 `{ }` 用来列出数组的初始数据；上一节 if / else 里的 `{ }` 用来圈出要执行的语句。理解符号时，要结合它所在的语句。

### 3 字符串数组

```csharp
// string[] 表示字符串数组，变量名为 s。
string[] s =
{
    "string 1", // 第一个元素，索引 0。
    "string 2", // 第二个元素，索引 1。
    "string 3", // 第三个元素，索引 2。
    "string 4", // 第四个元素，索引 3；末尾的逗号可以保留。
}; // 完整的声明语句要在 } 后面加分号。
```

对应的 Python：

```python
s = [
    "string 1",
    "string 2",
    "string 3",
    "string 4",
]
```

这两段代码只创建集合，没有打印。`s[0]` 是 `"string 1"`，`s[3]` 是 `"string 4"`；C# 的 `s.Length` 和 Python 的 `len(s)` 在本例中都是 4。

**最后一张截图的完整写法应以 `};` 结束。** 截图末尾的 `}` 附近有红色提示；声明语句末尾需要补上分号。最后一个元素之后的逗号是允许的。

### 本节写法对照

| 本节的 C# 写法 | 含义 | Python 对照 |
| --- | --- | --- |
| `int[] ints1 = { 1, 2, 3 };` | 创建一维整数数组 | `ints1 = [1, 2, 3]` |
| `new int[3]` | 创建三个默认值为 0 的 int 元素 | `[0] * 3`，得到相同初始数据 |
| 一维数组的 `Length` | 元素个数 | `len(列表)` |
| `ints1[1]` | 取第二个元素 | `ints1[1]` |
| `int[,]` | 二维整数数组 | 本例用嵌套列表表示相同数据 |
| `ints3[1, 2]` | 第二行第三列 | `ints3[1][2]` |
| `string[]` | 字符串数组 | 本例用包含字符串的列表 |

C# 数组对象创建后长度固定，已有元素的值可以修改。`int[]` 的元素类型是 int，`string[]` 的元素类型是 string。Python 普通列表可以增删元素，也可以容纳不同类型的对象。

参考 [C# 数组文档](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/arrays)和 [Python 列表教程](https://docs.python.org/3/tutorial/datastructures.html)。

## 第六节 Loop 循环和字符串插值

Loop 就是循环：让一段代码重复执行。这一节按教程中的 `for`、`while`、`do ... while` 和 `foreach` 整理，再把 `$`、`break`、`continue` 与 Python 对照起来。

### 1 本节使用的数组

截图里的循环输出依次是 1、2、3，因此下面按这组数据演示：

```csharp
int[] ints2 = { 1, 2, 3 }; // 三个整数，索引分别是 0、1、2。
```

```python
ints2 = [1, 2, 3]  # 用 Python 列表表示相同的数据。
```

上一节的 `new int[3]` 会得到三个 0；本节使用的是上面的 1、2、3。下面各小节分别运行，先准备这组数据。截图没有显示 `k` 和 `m` 的初始化，相关示例会明确补上从 0 开始的声明。

### 2 for 循环按索引遍历

```csharp
Console.WriteLine(); // 输出一个空行，对应 Python 的 print()。
Console.WriteLine("For loop"); // 输出标题。

// 初始化；继续循环的条件；每轮结束后的更新。
for (int i = 0; i < ints2.Length; i++) // 这里的 i++ 相当于 i = i + 1。
{ // 大括号圈出每一轮要执行的代码。
    // {0} 使用后面的 i，{1} 使用后面的 ints2[i]。
    Console.WriteLine("ints2[{0}] is {1}", i, ints2[i]);
}
```

`for` 括号里的两处分号把三个部分分开：

| 部分 | 本例代码 | 什么时候执行 |
| --- | --- | --- |
| 初始化 | `int i = 0` | 开始时执行一次，从索引 0 出发 |
| 条件 | `i < ints2.Length` | 每轮开始前判断，true 才执行循环体 |
| 更新 | `i++` | 循环体执行完后，把 i 加 1 |

顺序是：初始化 → 判断条件 → 执行循环体 → 更新 i → 再判断条件。这里的索引依次是 0、1、2；当 i 变成 3 时，`3 < 3` 为 false，循环结束。

**长度是 3，最后一个索引是 2，所以条件用 `<`。** 如果写成 `<= ints2.Length`，最后会尝试访问不存在的 `ints2[3]`。

对应的 Python：

```python
print()  # 空行。
print("For loop")

# len(ints2) 是 3；range(3) 依次提供 0、1、2，不包含 3。
for i in range(len(ints2)):
    # .format 的 {0}、{1} 与上面 C# 的占位符对应。
    print("ints2[{0}] is {1}".format(i, ints2[i]))
```

Python 没有这里的 `i++` 写法。单独让变量增加 1 时用 `i += 1`；这个 Python for 已经由 `range` 提供下一个索引，不需要再手动增加 i。

### 3 while 循环和 break

截图使用 `while (true)`，再通过 `break` 结束循环：

```csharp
Console.WriteLine();
Console.WriteLine("While loop");

int j = 0; // 先准备索引。
while (true) // 条件一直为 true；本例靠下面的 break 退出。
{
    Console.WriteLine("ints2[{0}] is {1}", j, ints2[j]);
    j++; // 打印之后，再把索引加 1。

    if (j == ints2.Length) break; // 已经打印完三个元素，退出当前循环。
}
```

`if (条件) break;` 是单条语句的简写，也可以写成：

```csharp
if (j == ints2.Length)
{
    break; // 退出包含它的这个 while 循环。
}
```

对应的 Python：

```python
print()
print("While loop")

j = 0  # 索引从 0 开始。
while True:  # Python 的 True 首字母大写。
    print("ints2[{0}] is {1}".format(j, ints2[j]))
    j += 1  # 对应 C# 的 j++。

    if j == len(ints2):
        break  # Python 也要用 break，才能在这里退出 while True。
```

**Python 的循环也有 break。** 之前 if / elif 不需要 break，是因为它在选择分支；这里的 break 是用来提前退出循环。

这个截图写法适用于当前非空数组。如果数组为空，它仍会先访问 `ints2[0]`，发生越界。把边界条件放进 while，可以让空数组执行零次：

```csharp
int j = 0;
while (j < ints2.Length) // 先确认这个索引存在。
{
    Console.WriteLine($"ints2[{j}] is {ints2[j]}");
    j++;
}
```

```python
j = 0
while j < len(ints2):  # 空列表时条件立即为 False。
    print(f"ints2[{j}] is {ints2[j]}")
    j += 1
```

### 4 do while 先执行再判断

截图里的 do / while 代码没有显示 k 的声明。这里补上 `int k = 0;`，并沿用截图中的循环体：

```csharp
int k = 0; // 为完整示例补上的初始化。
do // 先执行大括号里的代码。
{
    Console.WriteLine($"ints2[{k}] is {ints2[k]}");
    k++; // 打印后，让索引前进一个位置。
} while (k < ints2.Length); // 执行完再判断；这里末尾要有分号。
```

**while 先判断，可能一次也不执行；do / while 先执行，再判断是否继续。** 因此这个 do / while 示例同样需要非空数组，否则第一次访问就会越界。

Python 没有内置的 do / while 语句。可以用 `while True`，把退出判断放在循环体末尾，表达本例相同的执行顺序：

```python
k = 0  # 对应补上的 int k = 0。
while True:
    print(f"ints2[{k}] is {ints2[k]}")  # 先执行。
    k += 1

    if k >= len(ints2):  # 再决定要不要继续。
        break
```

前三种循环对本节的数组都会输出同样的三行，截图中的标题不同：

```text
ints2[0] is 1
ints2[1] is 2
ints2[2] is 3
```

### 5 美元符号和字符串插值

你提到的 `$`，就是截图中 `$"ints2[{k}] is {ints2[k]}"` 的前缀。它让字符串里的 `{表达式}` 被表达式的结果替换，叫做**字符串插值**。对应 Python 的 `f"..."` 写法。

```csharp
int k = 1; // 用第二个元素举例。

// $ 开启字符串插值。
// {k} 变成 1；{ints2[k]} 先取数组元素，再变成 2。
Console.WriteLine($"ints2[{k}] is {ints2[k]}");

// 不加 $，这些花括号和其中的内容只是普通文字。
Console.WriteLine("ints2[{k}] is {ints2[k]}");
```

```python
k = 1

# f 开启 Python 的字符串插值。
print(f"ints2[{k}] is {ints2[k]}")

# 不加 f，就打印字符串本身。
print("ints2[{k}] is {ints2[k]}")
```

两种语言在这里都依次输出：

```text
ints2[1] is 2
ints2[{k}] is {ints2[k]}
```

字符串中，`{k}` 表示代入值；花括号外面的 `[` 和 `]` 只是输出文字的一部分。`{ints2[k]}` 内部的 `[k]` 才是在取数组元素。

前面学过的编号占位符和这里的字符串插值，也可以得到相同的结果：

| 写法 | C# | Python |
| --- | --- | --- |
| 编号占位符 | `Console.WriteLine("ints2[{0}] is {1}", k, ints2[k]);` | `print("ints2[{0}] is {1}".format(k, ints2[k]))` |
| 直接在花括号里写表达式 | `Console.WriteLine($"ints2[{k}] is {ints2[k]}");` | `print(f"ints2[{k}] is {ints2[k]}")` |

这里的 `$` 放在字符串前面；它不是变量名的一部分，也不是循环专用的符号。

### 6 continue 跳过当前这一轮

截图中的 for 循环增加了一个判断：

```csharp
for (int i = 0; i < ints2.Length; i++)
{
    // % 是取余；除以 2 的余数为 0，说明这个整数是偶数。
    if (ints2[i] % 2 == 0) continue; // 偶数跳过本轮后面的代码。

    Console.WriteLine($"ints2[{i}] = {ints2[i]}"); // 本例只打印 1、3。
}
```

对应的 Python：

```python
for i in range(len(ints2)):
    if ints2[i] % 2 == 0:
        continue  # 跳过这次迭代剩余的代码，继续取下一个 i。

    print(f"ints2[{i}] = {ints2[i]}")
```

两段代码都会输出：

```text
ints2[0] = 1
ints2[2] = 3
```

**continue 跳过这一轮，break 结束当前循环。** 在这个 C# for 中，continue 之后仍会执行循环头里的 `i++`，然后判断下一轮的条件。

| 关键字 | C# 和 Python 在循环中的作用 |
| --- | --- |
| `break` | 退出当前这层循环，继续执行循环后面的代码 |
| `continue` | 跳过本轮剩余代码，转到下一轮的流程 |

如果在 while 循环里手动更新索引，要留意 continue 的位置：放在更新语句前面，会跳过那次更新。本节最后一张截图中的 m，正是类似情况。

### 7 foreach 直接取得每个元素

最后一张截图改成了 foreach。它直接取数组里的元素，Python 对应 `for item in ints2`。

下面保留截图的判断和输出写法；截图没显示 m 的初始化，这里补成 0：

```csharp
int m = 0; // 为完整示例补上；这里用它统计已经输出了几个元素。

foreach (var item in ints2) // item 依次是 1、2、3。
{
    // 本节数据都是正数，余数为 1 的是奇数：1、3。
    if (item % 2 == 1) continue;

    // 注意：m 不是 foreach 自动提供的数组索引。
    Console.WriteLine($"ints2[{m}] = {item}");
    m++; // 只有执行到这里，m 才会增加。
}
```

`var` 让 C# 编译器推断类型。因为 ints2 是 `int[]`，所以这里的 item 是 `int`，与截图中的类型提示一致。

对应的 Python：

```python
m = 0  # 与补上的 C# 初始化一致。

for item in ints2:  # 直接拿到值，而不是索引。
    if item % 2 == 1:
        continue

    print(f"ints2[{m}] = {item}")
    m += 1  # 被 continue 跳过的轮次，不会执行这行。
```

执行过程：

| item | 判断结果 | 这一轮发生什么 | 本轮结束后的 m |
| --- | --- | --- | --- |
| 1 | 奇数，continue | 跳过打印和 m++ | 0 |
| 2 | 不跳过 | 打印 `ints2[0] = 2`，然后 m++ | 1 |
| 3 | 奇数，continue | 跳过打印和 m++ | 1 |

**假设 m 从 0 开始，截图写法实际打印的是 `ints2[0] = 2`。但数组中 2 的真实索引是 1。** 因为 m 只在打印后增加，这个输出标签容易让人误以为它是数组索引。

这与上一张截图的条件也相反：for 里 `% 2 == 0` 跳过偶数，留下 1、3；foreach 里 `% 2 == 1` 在当前数据下跳过奇数，留下 2。

如果只需要元素值，输出标签直接写 `item = {item}` 就清楚了。如果要保留数组的真实索引，可以这样写：

```csharp
for (int i = 0; i < ints2.Length; i++) // i 始终跟着原数组的位置走。
{
    if (ints2[i] % 2 != 0) continue; // 跳过奇数，保留偶数。
    Console.WriteLine($"ints2[{i}] = {ints2[i]}");
}
```

```python
# enumerate 同时提供原列表的索引 i 和对应的元素 item。
for i, item in enumerate(ints2):
    if item % 2 != 0:
        continue
    print(f"ints2[{i}] = {item}")
```

这两段改写都会输出 `ints2[1] = 2`。这里用 `% 2 != 0` 判断奇数，也适用于负整数；C# 的负奇数除以 2 的余数为 -1，因此 `% 2 == 1` 不能判断所有奇数。

### 本节写法对照

| C# | Python 对照 | 记住什么 |
| --- | --- | --- |
| `for (int i = 0; i < ints2.Length; i++)` | `for i in range(len(ints2)):` | 按索引逐个访问 |
| `foreach (var item in ints2)` | `for item in ints2:` | 直接拿到每个元素 |
| `while (条件)` | `while 条件:` | 每轮执行前判断 |
| `do { ... } while (条件);` | `while True` 加循环体末尾的退出判断 | 先执行，再判断 |
| `i++` 在本节的更新位置 | `i += 1` | 变量增加 1 |
| `$"值是 {item}"` | `f"值是 {item}"` | 把表达式结果放入字符串 |
| `break` | `break` | 退出当前这层循环 |
| `continue` | `continue` | 跳过本轮剩余代码 |

参考 [C# 循环语句](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/iteration-statements)、[C# 字符串插值](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated)、[Python 循环和控制流](https://docs.python.org/3/tutorial/controlflow.html)和 [Python 格式化字符串](https://docs.python.org/3/tutorial/inputoutput.html)。

## 第七节 函数的定义 参数和返回值

函数把一段有名字的代码封装起来，方便多次调用。这里继续用顶层语句的 Console App 写法；在这种 Program.cs 中，下面这些声明属于局部函数。先区分两件事：**定义函数是在说明它怎么做；调用函数才会执行函数体。**

### 1 PrintSentence 无参数和无返回值

第一张截图只定义函数，第二张截图才加上调用：

```csharp
void PrintSentence() // void 表示不返回值；空括号表示没有参数。
{ // 大括号圈出函数体。
    Console.WriteLine("This is a sentence."); // 调用时打印这句话。
}

PrintSentence(); // 函数名后加括号，执行上面定义的函数。
```

对应的 Python：

```python
def PrintSentence():  # def 用来定义函数；没有参数。
    print("This is a sentence.")  # 缩进部分是函数体。

PrintSentence()  # 调用函数，才会打印。
```

两段代码都会输出：

```text
This is a sentence.
```

只写定义而没有调用时，不会打印这句话。再调用一次，就再执行一次。

C# 的 void 函数没有返回值，不能把它的调用结果赋给变量。Python 中，这个函数没有显式 return，调用后会隐式返回 None；这与 C# 的 void 在语言规则上有区别。

截图里的 `0 references`、`1 reference` 是 Visual Studio 显示的代码引用信息，帮助找到哪里使用了这个函数；它们不是程序运行次数，也不需要写进代码。

### 2 Power 参数和整数返回值

```csharp
int Power(int n) // 第一个 int 是返回类型；int n 是一个整数参数。
{
    return n * n; // 返回 n 的平方，并结束这次函数调用。
}

// 先执行 Power(3)，得到 9，再把 9 填入 {0} 并打印。
Console.WriteLine("Power(3) = {0}", Power(3));
```

对应的 Python：

```python
def Power(n):  # 定义参数 n。
    return n * n  # 计算平方，把结果返回给调用它的代码。

print("Power(3) = {0}".format(Power(3)))
```

两段代码都会输出：

```text
Power(3) = 9
```

把 `int Power(int n)` 拆开看：

| 部分 | 含义 |
| --- | --- |
| 开头的 `int` | 这个函数返回 int 类型的值 |
| `Power` | 自己起的函数名 |
| `int n` | 函数接收一个 int 参数，在函数体里用 n 表示 |
| `return n * n;` | 把计算结果交回调用处 |

定义中的 n 叫**形参**；调用 `Power(3)` 时传入的 3 叫**实参**。这次调用相当于让 n 取值为 3，再计算 `3 * 3`。函数名 Power 不会自动决定算法；这个函数的行为由 `n * n` 决定，所以它计算的是平方。

**return 不等于打印。** 单独调用 `Power(3);` 会计算并返回 9，但在这个控制台程序中不会自动显示它。要看到结果，需要像截图一样再用 Console.WriteLine；Python 脚本中同样需要 print。

return 结束当前函数，回到调用处。前面学过的 break 则退出当前循环或 switch；它们作用的范围不同。

### 3 DoubleString 字符串参数和字符串返回值

截图定义了这个函数，还没有显示它的调用。这里补一条调用演示：

```csharp
string DoubleString(string s) // 接收 string，返回 string。
{
    return s + s; // 字符串的 + 表示拼接，把文本重复两遍。
}

Console.WriteLine(DoubleString("Hi")); // 补充示例：输出 HiHi。
```

对应的 Python：

```python
def DoubleString(s):  # 接收字符串。
    return s + s  # 拼接两份相同文本。

print(DoubleString("Hi"))  # 补充示例：输出 HiHi。
```

两段代码都会输出 `HiHi`。DoubleString 是函数名；这里的返回类型是 string，和下一段的 double 数值类型要分开理解。

### 4 Add 两个参数和 double 返回值

```csharp
double Add(double a, double b) // 接收两个 double 参数，返回 double。
{
    return a + b; // 返回两个数的和。
}

// 实参按顺序对应：3 对应 a，4 对应 b。
Console.WriteLine("3 + 4 = {0}", Add(3, 4));
```

对应的 Python：

```python
def Add(a, b):  # 两个参数，用逗号分开。
    return a + b

print("3 + 4 = {0}".format(Add(3, 4)))
```

两段代码在本例中都会输出：

```text
3 + 4 = 7
```

C# 中，传入的整数 3、4 可以隐式转换为 double，函数返回的是 double 类型的 7。Python 上面这个版本用两个 int 相加，返回 int 类型的 7。**显示结果相同，不代表返回值的类型相同。** 如果 Python 使用 `Add(3.0, 4.0)`，得到的就是 float 类型的 7.0。

### 本节写法对照

| C# 写法 | 含义 | 本节的 Python 对照 |
| --- | --- | --- |
| `void PrintSentence()` | 无参数，不返回值 | `def PrintSentence():`，没有显式 return |
| `int Power(int n)` | 一个整数参数，返回整数 | `def Power(n):`，本例用 int 计算 |
| `string DoubleString(string s)` | 接收并返回字符串 | `def DoubleString(s):`，本例用 str |
| `double Add(double a, double b)` | 两个 double 参数，返回 double | `def Add(a, b):`；float 是常用对应类型 |
| `return 表达式;` | 返回结果并结束当前调用 | `return 表达式` |
| `函数名(实参);` | 调用函数 | `函数名(实参)` |
| 函数体中的 `{ }` | 圈出属于这个函数的代码 | 冒号后的缩进代码块 |

Python 的这些写法没有声明参数和返回类型；C# 中相应的类型是函数声明的一部分。

参考 [C# 局部函数](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/local-functions)、[C# 方法与参数](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods)和 [Python 函数定义](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)。

## 第八节 小项目 九九乘法表

这个练习把循环、函数、参数和字符串插值放在一起。先看上一批截图中的嵌套循环，再看新截图里按三列输出的 Row 函数。

### 1 嵌套循环的乘法练习

截图先用 1、2、3 演示两层循环：

```csharp
Console.WriteLine(); // 先空一行。
Console.WriteLine("乘法表");

for (int i = 1; i < 4; i++) // 外层：i 依次为 1、2、3。
{
    for (int j = 1; j < 4; j++) // 每次进入内层，j 都重新从 1 开始。
    {
        // i * j 是乘法；花括号把表达式的结果放进字符串。
        Console.WriteLine($"{i} * {j} = {i * j}");
    }
    Console.WriteLine(); // 内层循环全部结束后，空一行。
}
```

对应的 Python：

```python
print()
print("乘法表")

for i in range(1, 4):  # 1、2、3，不包括 4。
    for j in range(1, 4):  # 每一个 i，都配上 j 的三个值。
        print(f"{i} * {j} = {i * j}")
    print()  # 缩进在外层中、内层外：每组结束空一行。
```

外层执行三轮，每轮内层再执行三轮，总共打印 9 条算式。i 为 1 时，先打印 `1 * 1`、`1 * 2`、`1 * 3`；然后才让 i 变成 2。

这里用了 WriteLine，所以每条算式都单独占一行。最后的空行语句放在内层循环外面，因此是每组空一行。

### 2 Row 函数一次输出三列

新截图使用 `void Row(int n)`。n 决定从哪个乘数开始；一次调用会输出 9 行，每行三条算式。

| 调用 | 第一列 | 第二列 | 第三列 |
| --- | --- | --- | --- |
| `Row(1)` | 1 × i | 2 × i | 3 × i |
| `Row(4)` | 4 × i | 5 × i | 6 × i |
| `Row(7)` | 7 × i | 8 × i | 9 × i |

每一列中的 i 都从 1 到 9。三次调用合起来，覆盖 1 至 9 的完整乘法组合，共 81 条算式。

**截图最后一行看起来仍是 Row(1)。** 这样会再次打印 1、2、3 的那组，缺少 7、8、9；为了完成本项目，下面把第三次调用改为 Row(7)。为方便阅读，三组之间另外补了空行。

### 3 完整 C# 注释版

下面可以直接放进本节使用的 Console App 的 Program.cs。Row 内部保留截图的三列写法，以及字符串表达式外面的括号：

```csharp
void Row(int n) // 参数 n 是这一组三列的起始乘数；void 表示不返回值。
{
    for (int i = 1; i < 10; i++) // i 依次是 1 到 9。
    {
        // var 在这里推断出 string；s1、s2、s3 分别保存三条算式。
        // 逗号后的 3 指结果的最小显示宽度：占至少 3 个字符，右对齐。
        var s1 = ($"{n} * {i} = {n * i,3}");
        var s2 = ($"{n + 1} * {i} = {(n + 1) * i,3}");
        var s3 = ($"{n + 2} * {i} = {(n + 2) * i,3}");

        // {0}、{1}、{2} 分别代入 s1、s2、s3；空格把三列隔开。
        Console.WriteLine("{0}   {1}   {2}", s1, s2, s3);
    }
}

Row(1); // 打印 1、2、3 的三列。
Console.WriteLine(); // 补充：组间空一行。
Row(4); // 打印 4、5、6 的三列。
Console.WriteLine(); // 补充：组间空一行。
Row(7); // 修正截图中的重复调用，打印 7、8、9 的三列。
```

`($"...")` 外面的圆括号只是把字符串表达式括起来，本例可以省略，不会改变结果。字符串内部的 `(n + 1) * i` 则需要先把 n 加 1 再相乘；如果写成 `n + 1 * i`，会先做乘法，得到另一种结果。

Row 内部已经直接打印，因此无需 return；调用处也直接写 `Row(1);`。

### 4 对应的 Python 注释版

```python
def Row(n):  # n 是起始乘数；没有显式返回结果。
    for i in range(1, 10):  # 1 到 9，不包括 10。
        # :>3 表示至少 3 个字符宽，并且右对齐。
        s1 = f"{n} * {i} = {n * i:>3}"
        s2 = f"{n + 1} * {i} = {(n + 1) * i:>3}"
        s3 = f"{n + 2} * {i} = {(n + 2) * i:>3}"

        print(f"{s1}   {s2}   {s3}")  # 三条算式放在同一行。

Row(1)  # 1、2、3。
print()  # 组间空行。
Row(4)  # 4、5、6。
print()
Row(7)  # 7、8、9。
```

### 5 逗号和数字控制对齐

C# 的 `{n * i,3}` 可以拆成“表达式”和“显示宽度”：

| 部分 | 含义 | Python 对照 |
| --- | --- | --- |
| `n * i` | 计算要显示的结果 | `n * i` |
| `,3` | 最小宽度 3，靠右，不足时在左边补空格 | `:>3` |
| `,-3` | 最小宽度 3，靠左，不足时在右边补空格 | `:<3` |

比如把边界用竖线标出来：

```csharp
Console.WriteLine($"|{2,3}|");  // |  2|，左边补两个空格。
Console.WriteLine($"|{18,3}|"); // | 18|，左边补一个空格。
Console.WriteLine($"|{2,-3}|"); // |2  |，右边补两个空格。
```

```python
print(f"|{2:>3}|")   # |  2|
print(f"|{18:>3}|")  # | 18|
print(f"|{2:<3}|")   # |2  |
```

**这里的 3 是最小显示宽度，不是保留三位小数。** 当结果超过三个字符时，仍会完整输出，不会被截断。

本项目同时用到了两层格式化：先用 `$` 和花括号生成 s1、s2、s3，再用 `{0}`、`{1}`、`{2}` 把这三个字符串放到同一行。

### 6 完整版本的输出

```text
1 * 1 =   1   2 * 1 =   2   3 * 1 =   3
1 * 2 =   2   2 * 2 =   4   3 * 2 =   6
1 * 3 =   3   2 * 3 =   6   3 * 3 =   9
1 * 4 =   4   2 * 4 =   8   3 * 4 =  12
1 * 5 =   5   2 * 5 =  10   3 * 5 =  15
1 * 6 =   6   2 * 6 =  12   3 * 6 =  18
1 * 7 =   7   2 * 7 =  14   3 * 7 =  21
1 * 8 =   8   2 * 8 =  16   3 * 8 =  24
1 * 9 =   9   2 * 9 =  18   3 * 9 =  27

4 * 1 =   4   5 * 1 =   5   6 * 1 =   6
4 * 2 =   8   5 * 2 =  10   6 * 2 =  12
4 * 3 =  12   5 * 3 =  15   6 * 3 =  18
4 * 4 =  16   5 * 4 =  20   6 * 4 =  24
4 * 5 =  20   5 * 5 =  25   6 * 5 =  30
4 * 6 =  24   5 * 6 =  30   6 * 6 =  36
4 * 7 =  28   5 * 7 =  35   6 * 7 =  42
4 * 8 =  32   5 * 8 =  40   6 * 8 =  48
4 * 9 =  36   5 * 9 =  45   6 * 9 =  54

7 * 1 =   7   8 * 1 =   8   9 * 1 =   9
7 * 2 =  14   8 * 2 =  16   9 * 2 =  18
7 * 3 =  21   8 * 3 =  24   9 * 3 =  27
7 * 4 =  28   8 * 4 =  32   9 * 4 =  36
7 * 5 =  35   8 * 5 =  40   9 * 5 =  45
7 * 6 =  42   8 * 6 =  48   9 * 6 =  54
7 * 7 =  49   8 * 7 =  56   9 * 7 =  63
7 * 8 =  56   8 * 8 =  64   9 * 8 =  72
7 * 9 =  63   8 * 9 =  72   9 * 9 =  81
```

参考 [C# 字符串插值与对齐](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated)和 [Python 格式说明](https://docs.python.org/3/library/string.html#format-specification-mini-language)。

## 第九节 字符串的格式化与操作

这一节对应 Formatting and operations of strings，按截图学习对齐、数字格式、大小写、转义字符、路径、取字符、截取字符串和拆分字符串。下面沿用 `s1 = "Robert"`、`s2 = "John"`；本章可以作为一组独立练习运行。

### 1 对齐 补零和数值格式

表头和分隔线的空格按本例列宽整理，其他格式符号沿用截图：

```csharp
var s1 = "Robert"; // 推断为 string。
var s2 = "John";   // 推断为 string。
var a1 = 30;      // 推断为 int。
var a2 = 36;      // 推断为 int。

Console.WriteLine("  Name     Age"); // 表头。
Console.WriteLine("--------   ---"); // 两列之间用三个空格隔开。

// {0} 对应 s1；,8 表示最小宽度 8，并靠右。
// {1} 对应 a1；:000 表示数字至少有三位，不足时在前面补 0。
Console.WriteLine("{0,8}   {1:000}", s1, a1);

// -8 表示最小宽度 8，并靠左；年龄同时设置宽度和补零格式。
Console.WriteLine($"{s2,-8}   {a2,3:000}");

// N0：数字格式，使用分组分隔符，显示零位小数。
Console.WriteLine("Value: {0:N0}", 5678);

// C2：货币格式，显示两位小数；货币符号等跟随当前区域设置。
Console.WriteLine("Value: {0:C2}", 5678);
Console.WriteLine(); // 空行。
```

**逗号后的数字管对齐，冒号后的内容管显示格式。** 编号占位符的结构是 `{参数编号,宽度:格式}`；字符串插值的结构是 `{表达式,宽度:格式}`。宽度和格式都可以按需省略。

| C# 格式 | 本节含义 | Python 对照 |
| --- | --- | --- |
| `{0,8}` | 第一个实参，最小宽度 8，右对齐 | `{s1:>8}` |
| `{s2,-8}` | s2，最小宽度 8，左对齐 | `{s2:<8}` |
| `{1:000}` | 第二个实参，至少三位数字，前面补 0 | 年龄为整数时用 `{a1:03d}` |
| `{a2,3:000}` | 最小宽度 3，同时按三位补零 | 本例用 `{a2:03d}` |
| `{0:N0}` | 分组数字，零位小数 | 本例用 `{5678:,.0f}` |
| `{0:C2}` | 货币格式，两位小数 | 本例手动加美元符号，再用 `{5678:,.2f}` |

这些宽度都是最小宽度，内容更长时不会被截断。`:000` 中的三个 0 是数字占位符，不代表三位小数。

对应的 Python：

```python
s1 = "Robert"
s2 = "John"
a1 = 30
a2 = 36

print("  Name     Age")
print("--------   ---")
print(f"{s1:>8}   {a1:03d}")  # > 是右对齐；03d 是整数至少三位，补 0。
print(f"{s2:<8}   {a2:03d}")  # < 是左对齐。
print(f"Value: {5678:,.0f}")  # , 是千位分隔；.0f 显示零位小数。
print(f"Value: ${5678:,.2f}")  # 这里的 $ 是手动写入的货币符号。
print()
```

以下显示按 en-AU 的常见格式举例。C# 的 N0、C2 使用运行环境的区域设置，实际分组符号、货币符号和排列方式可能不同；上面的 Python 代码则明确写了逗号分组和 $，不会自动选择币种。

```text
  Name     Age
--------   ---
  Robert   030
John       036
Value: 5,678
Value: $5,678.00
```

格式化改变的是输出文字，不会把 a1 从整数 30 改成字符串 "030"，也不会改变数值 5678。

### 2 ToLower 和 ToUpper

```csharp
Console.WriteLine("ToLower(): {0}", s1.ToLower()); // Robert → robert。
Console.WriteLine("ToUpper(): {0}", s1.ToUpper()); // Robert → ROBERT。
Console.WriteLine("ToUpper(): {0}", "Lorrance".ToUpper()); // 也可以直接对字符串字面量调用。
Console.WriteLine("ToUpper(): {0}", "大家好".ToUpper()); // 本例中文字没有大小写，保持原样。
```

对应的 Python：

```python
print(f"ToLower(): {s1.lower()}")  # 本例对应 ToLower()。
print(f"ToUpper(): {s1.upper()}")  # 本例对应 ToUpper()。
print(f"ToUpper(): {'Lorrance'.upper()}")
print(f"ToUpper(): {'大家好'.upper()}")
```

本例输出：

```text
ToLower(): robert
ToUpper(): ROBERT
ToUpper(): LORRANCE
ToUpper(): 大家好
```

C# 和 Python 的字符串都是不可变的。调用这些方法得到转换后的字符串，原来的 s1 仍然是 "Robert"；如果想让变量保存转换结果，要把结果再赋给它。

### 3 转义字符和反斜杠

```csharp
// 前面的 \\t 显示成文字 \t；后面的 \t 才是实际的 Tab。
Console.WriteLine($"\\t: {s1}\t{s2}");

// 前面的 \\n 显示成文字 \n；后面的 \n 才是真正换行。
Console.WriteLine($"\\n: {s1}\n{s2}");

// 普通字符串里，两个反斜杠 \\ 表示实际的一个反斜杠。
Console.WriteLine($"{s1}\\{s2}");
```

对应的 Python：

```python
print(f"\\t: {s1}\t{s2}")  # 标签中的 \t 是文字；名字之间是真正的 Tab。
print(f"\\n: {s1}\n{s2}")  # 名字之间换行。
print(f"{s1}\\{s2}")      # 输出 Robert\John。
```

| 普通字符串里的写法 | 实际含义 | C# 与 Python 在本例中的关系 |
| --- | --- | --- |
| `\t` | 一个 Tab 制表符 | 相同 |
| `\n` | 换行符 | 相同 |
| `\\` | 一个反斜杠 | 相同 |
| `\\t` | 反斜杠和字母 t 两个普通字符 | 显示成文字 `\t` |
| `\\n` | 反斜杠和字母 n 两个普通字符 | 显示成文字 `\n` |

Tab 的显示位置取决于终端或编辑器的制表位，不保证固定等于几个空格。

```text
\t: Robert	John
\n: Robert
John
Robert\John
```

### 4 逐字字符串和 Windows 路径

第二、第三张截图展示的是同一组路径写法：

```csharp
var path1 = "c:\\windows"; // 普通字符串：\\ 表示一个反斜杠。
var path2 = @"c:\windows"; // @ 开启逐字字符串，反斜杠直接保留。

Console.WriteLine("path1: {0}", path1);
Console.WriteLine("path2: {0}", path2);
Console.WriteLine();
```

对应的 Python：

```python
path1 = "c:\\windows"  # 普通字符串，同样要把反斜杠写成 \\。
path2 = r"c:\windows"  # r 开启原始字符串，方便保留反斜杠。

print(f"path1: {path1}")
print(f"path2: {path2}")
print()
```

两种写法得到相同的路径文字：

```text
path1: c:\windows
path2: c:\windows
```

C# 的 `@"..."` 与 Python 的 `r"..."` 在本例中对应。前一章的 `$` 用来代入表达式，这里的 `@` 用来改变字符串字面量对反斜杠的处理；它们各自解决不同的问题。

### 5 字符索引和 Substring

Robert 的索引从 0 开始：

| 索引 | 0 | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- | --- |
| 字符 | R | o | b | e | r | t |

**截图第一行的提示写着 "the 3rd character"，但实际用了 s1[3]，取到的是第四个字符 e。** 第三个字符应该用 `[2]`，得到 b。因为这里 s1 和 robert 都是 "Robert"，下面统一使用 robert，并把提示改为 "4th"：

```csharp
var robert = "Robert";

// 索引 3 是第四个字符。
Console.WriteLine("the 4th character of Robert is: {0}", robert[3]);

// 从索引 1 开始，取 3 个字符：o、b、e。
Console.WriteLine("Substring(1,3): {0}", robert.Substring(1, 3));

// 从索引 4 开始，一直取到末尾：r、t。
Console.WriteLine("Substring(4): {0}", robert.Substring(4));
```

对应的 Python：

```python
robert = "Robert"

print(f"the 4th character of Robert is: {robert[3]}")
print(f"Substring(1,3): {robert[1:4]}")  # 结束位置不包含 4。
print(f"Substring(4): {robert[4:]}")    # 省略结束位置，取到末尾。
```

两段代码都会输出：

```text
the 4th character of Robert is: e
Substring(1,3): obe
Substring(4): rt
```

**C# 的 Substring(起点, 长度)，对应 Python 的 [起点:起点 + 长度]。** 第二个参数不是结束索引；Python 切片的右端则是结束索引，并且不包含那个位置。

本例中，C# 的 `robert[3]` 取出 char；Python 的 `robert[3]` 得到长度为 1 的 str。

### 6 Split 和 TrimEntries

```csharp
var s4 = "Marry, Terrice"; // 逗号后面有一个空格。

var s5 = s4.Split(','); // 按逗号拆分，结果是 string[]。
// 输出两边加单引号，方便看清片段里的空格。
Console.WriteLine($"'{s5[0]}'");
Console.WriteLine($"'{s5[1]}'"); // 第二个片段仍带着开头的空格。
Console.WriteLine();

var s6 = s4.Split(",", StringSplitOptions.TrimEntries);
// TrimEntries：拆分后，去掉各片段开头和结尾的空白。
Console.WriteLine($"'{s6[0]}'");
Console.WriteLine($"'{s6[1]}'");
```

对应的 Python：

```python
s4 = "Marry, Terrice"

s5 = s4.split(",")  # 结果是列表；指定逗号时不会自动去掉旁边的空格。
print(f"'{s5[0]}'")
print(f"'{s5[1]}'")
print()

# 先拆分，再对每个片段调用 strip()，去掉首尾空白。
s6 = [part.strip() for part in s4.split(",")]
print(f"'{s6[0]}'")
print(f"'{s6[1]}'")
```

两段代码都会输出：

```text
'Marry'
' Terrice'

'Marry'
'Terrice'
```

`Split(',')` 使用字符逗号，`Split(",", ...)` 使用字符串逗号；本例的分隔符都是逗号，空格是否去掉由 TrimEntries 这个选项决定。

TrimEntries 只处理片段首尾的空白，不会删除文本中间的空格，也不会自动删除空片段。C# 的 Split 返回 string[]；Python 的 split 返回 list。拆分操作不会把原来的 s4 改掉。

### 本节写法对照

| C# | Python 对照 | 本例结果或用途 |
| --- | --- | --- |
| `s1.ToLower()` | `s1.lower()` | robert |
| `s1.ToUpper()` | `s1.upper()` | ROBERT |
| `@"c:\windows"` | `r"c:\windows"` | 直接书写路径中的反斜杠 |
| `robert[3]` | `robert[3]` | 第四个字符 e |
| `robert.Substring(1, 3)` | `robert[1:4]` | obe |
| `robert.Substring(4)` | `robert[4:]` | rt |
| `s4.Split(',')` | `s4.split(",")` | 按逗号拆分，保留片段中的空格 |
| `StringSplitOptions.TrimEntries` | 拆分后对每个片段调用 `strip()` | 去掉片段首尾空白 |

参考 [.NET 标准数字格式](https://learn.microsoft.com/en-us/dotnet/standard/base-types/standard-numeric-format-strings)、[.NET 自定义数字格式](https://learn.microsoft.com/en-us/dotnet/standard/base-types/custom-numeric-format-strings)、[C# 字符串](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/strings/)、[C# Substring](https://learn.microsoft.com/en-us/dotnet/api/system.string.substring?view=net-10.0)、[StringSplitOptions](https://learn.microsoft.com/en-us/dotnet/api/system.stringsplitoptions)和 [Python 字符串方法](https://docs.python.org/3/library/stdtypes.html#string-methods)。

## 第十节 Class 类和对象

这一节开始把相关的数据和函数放进同一个类型。先用截图中的 Dog 理解：Name 保存名字，Sound() 根据这只狗的名字生成一句话。创建多个对象时，每个对象可以保存不同的名字。

介绍页同时列出了字段、属性、构造函数、访问权限、继承和方法重写。先沿着“定义 Dog → 创建对象 → 初始化名字 → 调用方法 → 得到字符串”这条顺序理解，后面的术语再跟教程逐个加入。

### 1 类 对象和成员

| 概念 | 本节例子 | 含义 |
| --- | --- | --- |
| Class 类 | `Dog` | 定义一种类型，规定对象包含什么数据和行为 |
| Object 对象 | `new Dog("Fred")` 创建的实例 | 按 Dog 的定义创建的一只具体的狗 |
| 变量 | `dog` | 本例保存对这只狗的引用 |
| Field 字段 | `Name` | 保存对象的数据 |
| Constructor 构造函数 | `Dog(string name)` | 创建对象时初始化它的数据 |
| Method 方法 | `Sound()` | 定义对象可以执行的行为 |

`Dog` 是类型名，`dog` 是变量名。大小写有区别；这个变量指向一个 Dog 对象。类可以定义一次，再创建多个实例，每个实例有自己的 Name。

函数放在类里、作为类的成员时，我们通常叫它“方法”。这里的 Sound 是实例方法，通过具体对象调用。

### 2 Dog 类的逐行注释

这一版来自实际编辑器截图，仅定义了带名字参数的构造函数。

**Dog.cs** 放类定义：

```csharp
namespace QuickStart; // 文件作用域命名空间，本文件里的 Dog 属于 QuickStart。

public class Dog // 定义一个名为 Dog 的类；public 表示公开的访问级别。
{
    public string Name; // 字符串类型的实例字段，保存这只狗的名字。

    public Dog(string name) // 构造函数：类名相同，没有返回类型。
    {
        Name = name; // 把传入的名字保存到当前对象的 Name 字段。
    }

    // 实例方法，返回 string；=> 是表达式体写法。
    public string Sound() => $"{Name} barks.";
}
```

**Program.cs** 放使用这个类的顶层语句：

```csharp
using QuickStart; // 让这里可以直接使用命名空间里的 Dog 等类型。

var dog = new Dog("Fred"); // 创建对象，调用 Dog(string name)，传入 "Fred"。
var sound = dog.Sound();  // 调用这个对象的方法，得到字符串 "Fred barks."。

// 截图只写到了上面赋值；下面这行是为了展示结果补上的。
Console.WriteLine(sound);
```

这两个 C# 代码块分别放在同一个 Console App 项目的两个文件中。Dog 的命名空间沿用截图中的 QuickStart。

截图中的 `var sound = dog.Sound();` 只是保存返回值，没有打印。加上上面的输出语句后，显示：

```text
Fred barks.
```

`var dog` 让编译器推断变量类型为 Dog；`var sound` 的类型是 string。这两个 var 都有确定的编译期类型。

### 3 用 Python 对照完整流程

```python
class Dog:  # 定义 Dog 类。
    def __init__(self, name):  # 实例创建时，用这段代码完成初始化。
        self.Name = name  # 把参数 name 保存到当前实例的 Name 属性。

    def Sound(self):  # 实例方法；self 代表这次调用所使用的对象。
        return f"{self.Name} barks."  # 返回字符串，没有直接打印。

dog = Dog("Fred")  # Python 直接调用类，不需要写 new。
sound = dog.Sound()  # 调用当前对象的方法，保存返回值。
print(sound)  # 为演示补上的输出语句。
```

也会输出 `Fred barks.`。这里保留 Name、Sound 的拼写，方便和教程逐行对应。

| C# | Python 在本例中的对照 |
| --- | --- |
| `public class Dog` | `class Dog:` |
| `public Dog(string name)` | `def __init__(self, name):` 中的初始化逻辑 |
| `Name = name;` | `self.Name = name` |
| `new Dog("Fred")` | `Dog("Fred")` |
| `dog.Sound()` | `dog.Sound()` |
| `this` 表示当前对象 | 实例方法中的 `self` |
| 返回类型 `string` | 本例返回 str；上面的 Python 没写类型声明 |

Python 的 __init__ 承担本例给实例赋初值的工作。调用 `dog.Sound()` 时，Python 会把 dog 作为 self 传给方法，所以调用处不用再显式传 self。

C# 方法内部访问 Name 时，可以省略当前对象的 `this.`。因此构造函数中的 `Name = name;` 也可以写成 `this.Name = name;`。

### 4 Name 和 name 的区别

`new Dog("Fred")` 的执行过程可以拆成：

1. 创建一个 Dog 对象。
2. 调用 `Dog(string name)`，这次的参数 name 是 "Fred"。
3. 执行 `Name = name;`，这个对象的 Name 字段保存 "Fred"。
4. dog 引用这个对象；之后 `dog.Sound()` 读取它的 Name，返回 "Fred barks."。

| 写法 | 角色 | 本例的值 |
| --- | --- | --- |
| `name` | 构造函数的参数 | 这次传入的 "Fred" |
| `Name` 或 `this.Name` | 当前对象的字段 | 初始化后保存 "Fred" |
| `dog.Name` | 在调用处访问这只狗的名字 | "Fred" |

**构造函数的名字与类名相同，前面没有 string、int 或 void。** 它在 new 创建对象时被调用。本例中的 Sound 是普通方法，有 string 返回类型，由 `dog.Sound()` 调用。

### 5 表达式体方法和返回值

Dog 的方法可以写成：

```csharp
// 这一行放在 Dog 类内部。
public string Sound() => $"{Name} barks.";
```

也可以在 Dog 类中展开为：

```csharp
public string Sound()
{
    return $"{Name} barks."; // 返回表达式的结果。
}
```

这两种写法在本例中相同。`=>` 后面的表达式提供返回值，末尾用分号结束声明；Python 对应方法里的 `return f"{self.Name} barks."`。

Name 属于这只狗，所以调用 Sound() 时不用再传入名字。Sound() 返回的是字符串；Console.WriteLine 或 print 才负责把它显示出来。

### 6 Cat 的属性和 get set

截图中的 Dog 使用字段：

```csharp
public string Name; // 实例字段：直接声明保存数据的位置。
```

Cat 使用的是自动实现属性：

```csharp
public string Name { get; set; } // 属性：提供读取和写入入口。
```

`get` 负责读取，`set` 负责赋值。自动实现属性由编译器提供存储用的字段。本例没有自定义检查规则，Name 可以公开读取和修改。

**Cat.cs** 对应截图：

```csharp
namespace QuickStart;

public class Cat
{
    public string Name { get; set; } // Name 是属性，公开可读、可写。

    public Cat(string name)
    {
        Name = name; // 给属性赋值，会使用它的 set。
    }

    public string Sound() => $"{Name} meows."; // 读取属性，使用它的 get。
}
```

下面是为说明读写补上的调用示例，放在使用 Cat 的 Program.cs 中：

```csharp
var cat = new Cat("Kitty"); // 构造函数初始化名字。
Console.WriteLine(cat.Name); // 读取属性，执行 get。

cat.Name = "Mimi"; // 给属性赋值，执行 set。
Console.WriteLine(cat.Sound()); // 现在方法读到的新名字是 Mimi。
```

输出：

```text
Kitty
Mimi meows.
```

在 Python 中，直接使用 `self.Name` 也能完成本节这种简单的保存和读取。如果要对应 C# 属性“读取和赋值走不同入口”的机制，可以看 @property：

```python
class Cat:
    def __init__(self, name):
        self.Name = name  # 通过下面的 setter 完成初始赋值。

    @property
    def Name(self):  # 读取 cat.Name 时执行，相当于 get。
        return self._name  # _name 用来保存实际的数据。

    @Name.setter
    def Name(self, value):  # 给 cat.Name 赋值时执行，相当于 set。
        self._name = value

    def Sound(self):
        return f"{self.Name} meows."  # 读取 Name 属性，使用 getter。

cat = Cat("Kitty")
print(cat.Name)  # 使用 getter。
cat.Name = "Mimi"  # 使用 setter。
print(cat.Sound())
```

Python 的 @property 和 @Name.setter 是装饰器语法，把读取、赋值逻辑连接成同一个属性；这里的 @ 与上一节 C# 字符串前的 @ 各有自己的语法含义。`_name` 的下划线表示内部使用的约定，并没有 C# private 那样的访问限制。

先记住：**字段负责存数据，属性负责提供访问入口；本例的 get 读、set 写。** 外面使用 `dog.Name` 和 `cat.Name` 时看起来相似，但 Dog 这一版声明的是字段，Cat 声明的是属性。

### 7 Sheep 的字段初始值

**Sheep.cs** 对应最后一张截图：

```csharp
namespace QuickStart;

public class Sheep
{
    public string Name = ""; // 字段先有一个空字符串初始值。

    public Sheep(string name) // 仍然是带参数的构造函数。
    {
        Name = name; // 创建时，再把传入的名字保存下来。
    }

    public string Sound() => $"{Name} baas.";
}
```

`Name = ""` 是字段的初始化，不会为类增加一个无参数构造函数。这个版本的 Sheep 创建时仍然需要传入名字。

对应的 Python 可直接在 __init__ 中保存传入的名字；当前例子中，空字符串初值会被构造时的赋值覆盖：

```python
class Sheep:
    def __init__(self, name):
        self.Name = name  # 对应构造函数最终保存的名字。

    def Sound(self):
        return f"{self.Name} baas."

# 下面是补充的调用演示，截图没有这两行。
sheep = Sheep("Dolly")
print(sheep.Sound())
```

输出 `Dolly baas.`。目前 Dog、Cat、Sheep 分别定义了各自的数据和方法；截图没有建立它们之间的继承关系。

### 8 介绍页中的两种构造函数

第一张介绍页里，Dog 的 Name 带空字符串初值，并且有两个构造函数。下面是那一版 Dog 类内部的相关成员：

```csharp
public string Name = "";

public Dog() { } // 无参数构造函数，保留字段的空字符串初值。

public Dog(string name) // 带一个 string 参数的构造函数。
{
    Name = name;
}
```

它可以同时支持 `new Dog()` 和 `new Dog("Max")`，这是本例中的**构造函数重载**：名字相同，参数列表不同。

之后实际编辑器里的 Dog.cs 仅定义了 `Dog(string name)`，因此那个版本需要传名字。对这个 Dog 来说，已经显式定义带参数构造函数后，编译器不会再自动补上无参数的 Dog()。这两段属于教程的不同版本，分开练习。

Python 常用一个带默认参数的 __init__ 支持本例的两种调用：

```python
class Dog:
    def __init__(self, name=""):  # 不传名字时，name 默认为空字符串。
        self.Name = name

    def Sound(self):
        return f"{self.Name} barks."

dog = Dog()  # 无参数，名字为空。
print(dog.Sound())
print()

dog1 = Dog("Max")  # 传入名字，得到另一只狗。
print(dog1.Sound())  # 这里使用 dog1，才会返回 Max 的名字。
print()
```

这段对应代码输出：

```text
 barks.

Max barks.
```

第一句开头有一个空格，因为名字为空，而返回的字符串是 `"{Name} barks."`。

第二张介绍页有一个笔误：创建了 `dog1 = new Dog("Max")` 后，输出行仍然调用了 `dog.Sound()`。这会再次使用前面那只名字为空的狗。对应的修正是：

```csharp
Console.WriteLine(dog1.Sound()); // 使用刚创建的 dog1，得到 Max barks.
```

Python 普通类里连续写两份不同参数的 __init__，后一次定义会覆盖前一次；上面的默认参数实现了这里需要的两种调用方式。

### 9 public 和访问权限

截图中每个 public 修饰的对象不同：

| 代码位置 | 控制什么 |
| --- | --- |
| `public class Dog` | Dog 类型的访问级别 |
| `public string Name` | Name 字段的访问级别 |
| `public Dog(string name)` | 构造函数的访问级别 |
| `public string Sound()` | Sound 方法的访问级别 |

介绍页中的四种常见访问级别：

| 修饰符 | 本节先理解的访问范围 |
| --- | --- |
| `public` | 允许公开访问，同时也需要所在类型等范围可访问 |
| `private` | 声明它的类型内部 |
| `protected` | 声明它的类型及派生类 |
| `internal` | 同一个程序集，也就是同一个编译生成的程序或库的范围 |

介绍页“只有 public 成员能在外面使用”是在简化说明当前示例。实际能否访问，还要看调用位置、程序集、继承关系和所在类型的访问级别；例如同一个程序集中的 internal 成员也可以访问。

Python 这一版 Dog 没有 public 关键字，通常直接访问 `dog.Name`。Python 常用下划线约定内部用途；C# 这里则由语言规则检查访问权限。

### 10 命名空间和类型

`namespace QuickStart;` 把 Dog、Cat、Sheep 等类型组织到 QuickStart 命名空间。文件作用域的分号写法让这个命名空间作用于该文件中的类型。

`using QuickStart;` 让 Program.cs 可以使用短名字 Dog，而不必每次写完整的 `QuickStart.Dog`。它处理的是类型名称的查找，不会创建狗，也不会调用 Sound。

Python 可以把 Dog 放进 `quick_start.py`，然后用 `from quick_start import Dog`。两种语言的组织方式不同：C# using 处理命名空间，Python import 处理模块。

另外，C# 的 `var dog = new Dog("Fred");` 让 dog 的变量类型确定为 Dog。当前 Cat 与 Dog 没有互相继承，所以不能随后把一个 Cat 对象直接赋给这个 Dog 变量。

Python 的变量可以重新绑定到其他类的对象，对象本身仍有具体类型。这里对比的是静态类型和动态类型；Python 也属于强类型语言。

### 11 介绍页里的后续术语

| 术语 | 在介绍页里的意思 |
| --- | --- |
| `Inheritance` 继承 | 用已有类作为基类，建立派生类，复用和扩展它的成员 |
| `virtual` | 允许派生类重写相应方法 |
| `override` | 在派生类中重写基类可重写的方法 |
| `overloading` 重载 | 同名成员使用不同的参数列表；前面的 Dog() 和 Dog(string name) 是本节例子 |

目前先沿着 Name、构造函数和 Sound() 读懂对象如何工作；继承和方法重写的代码，后续按教程再练。

参考 [C# 类](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/classes)、[C# 构造函数](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/constructors)、[C# 属性](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/properties)、[C# 访问修饰符](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/access-modifiers)、[C# 表达式体](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-operator)、[C# 命名空间](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/namespace)、[Python 类](https://docs.python.org/3/tutorial/classes.html)和 [Python property](https://docs.python.org/3/library/functions.html#property)。

## 第十一节 继承 方法重写和多态

上一节的 Dog、Cat、Sheep 各自保存名字、定义叫声。这一节把共同的名字和吃东西方法放进 Animal，再让三种动物分别实现自己的叫声。

这组截图展示了连续的修改过程：先加继承关系，发现同名成员被隐藏；再删除子类重复的 Name；然后用 virtual 和 override 建立方法重写关系；最后在 Dog.Sound() 内调用继承来的 Eat()。下面按这个顺序理解，练习时使用对应阶段的版本。

### 1 基类和派生类

`Animal` 是基类，也叫父类；`Dog`、`Cat`、`Sheep` 是派生类，也叫子类。这里的关系是“狗是一种动物”，所以 Dog 对象也可以通过 Animal 类型的引用来使用。

| 内容 | 放在哪里 | 为什么 |
| --- | --- | --- |
| 名字 `Name` | Animal | 三种动物都有名字，可以复用同一份属性定义 |
| 吃东西 `Eat()` | Animal | 本例三种动物可以复用这个行为 |
| 叫声 `Sound()` | Animal 提供虚方法，子类重写 | 都会发声，但狗、猫、羊的具体叫声不同 |

“复用 Name 的定义”不表示所有动物共用同一个名字。Fred、Luna、Oliver 仍属于三个不同对象，每个对象保存自己的 Name。

C# 用冒号声明继承：

```csharp
public class Dog : Animal // Dog 继承 Animal。
{
    // 在这里定义 Dog 自己的成员。
}
```

Python 的对应写法是 `class Dog(Animal):`，把基类放在类名后面的括号中。

### 2 第一张图中的 Animal 类

**Animal.cs**：

```csharp
namespace QuickStart; // 本文件中的 Animal 属于 QuickStart 命名空间。

public class Animal // 定义动物基类。
{
    // 自动实现属性：可读、可写；每个对象的初始名字为空字符串。
    public string Name { get; set; } = "";

    public Animal() { } // 无参数构造函数，不额外修改 Name。

    // 带参数构造函数；表达式体写法，把参数保存到 Name 属性。
    public Animal(string name) => Name = name;

    // 初始版本的普通实例方法，还没有 virtual。
    public string Sound() => "@#$%";

    // 受保护的实例方法：Animal 内部及派生类中可以按访问规则使用。
    protected string Eat() => $"Animal {Name} ate something";
}
```

两种构造函数分别支持 `new Animal()` 和 `new Animal("Fred")`。`Animal(string name) => Name = name;` 与下面的构造函数写法相同：

```csharp
// 放在 Animal 类内部，作为上面带参数构造函数的另一种写法。
public Animal(string name)
{
    Name = name;
}
```

这里的 `=>` 执行赋值；构造函数没有返回类型。Sound() 和 Eat() 则返回 string。

`"@#$%"` 是普通字符串，里面的符号是教程给动物通用叫声使用的占位内容；其中的 @ 在引号内部，与上一节的逐字字符串前缀 `@"..."` 不同。Eat() 返回一句话，本身没有 Console.WriteLine，不会主动打印。

### 3 绿色波浪线为什么出现

最初的 Dog 加了 `: Animal`，但仍保留上一节自己的 Name 字段和普通 Sound() 方法：

```csharp
namespace QuickStart;

public class Dog : Animal // 增加了继承关系。
{
    public string Name; // 又声明同名字段，隐藏了继承的 Animal.Name 属性。

    public Dog(string name)
    {
        Name = name; // 此时赋值的是 Dog 自己声明的 Name 字段。
    }

    // 此时 Animal.Sound 不是虚方法；这里是同名方法隐藏。
    public string Sound() => $"{Name} barks.";
}
```

Sheep 的截图明确显示了警告 **CS0108**：`Sheep.Name` 隐藏了继承来的 `Animal.Name`。Dog 的 Name 和 Sound 上也有同名成员隐藏的提示。

隐藏不会删掉或改写基类的成员。以这一版 Dog 为例，同一个对象里既保留 Animal.Name 属性，也有 Dog.Name 字段；通过不同声明类型的引用访问，可能读到不同的成员。

下面是为说明问题补上的调用，配合本节第 2、3 部分的初始版本使用：

```csharp
var dog = new Dog("Fred"); // dog 的编译期类型是 Dog。
Animal animal = dog;      // animal 引用同一对象，编译期类型是 Animal。

Console.WriteLine(dog.Name);       // Fred：读 Dog.Name 字段。
Console.WriteLine(animal.Name);    // 空行：读 Animal.Name 属性，仍是 ""。
Console.WriteLine(dog.Sound());    // Fred barks.：调用 Dog 的普通方法。
Console.WriteLine(animal.Sound()); // @#$%：调用 Animal 的非虚方法。
```

`Animal animal = dog;` 没有创建第二只动物，也没有把狗变成另一种对象。这里的两个变量引用同一只狗；差别在于编译期看到的类型，以及成员是否参与虚方法重写。

| 访问 | 初始版本的结果 | 原因 |
| --- | --- | --- |
| `dog.Name` | `"Fred"` | 构造函数给 Dog 的同名字段赋值 |
| `animal.Name` | `""` | Animal 的属性没有被这次赋值修改 |
| `dog.Sound()` | `"Fred barks."` | Dog 类型的引用调用 Dog 的同名普通方法 |
| `animal.Sound()` | `"@#$%"` | Animal.Sound 是非虚方法，按 Animal 的成员调用 |

截图里的“子代盖掉父代的资料”可以理解为名字被遮住，但不要理解成父类属性消失了。这里需要把重复的 Name 声明删掉，让子类使用继承来的属性。

警告建议“如果隐藏是有意的，就使用 new 关键字”。声明成员时的 new 是明确表示隐藏，和 `new Dog(...)` 创建对象各有自己的用途；它不会让方法获得 override 的多态行为。本例的目标是共享名字、分别发声，按后面的删除重复成员和方法重写来改。

### 4 删除重复 Name 后还需要做什么

后面的 Sheep 截图已经删掉自己的 `public string Name = "";`，保留：

```csharp
namespace QuickStart;

public class Sheep : Animal
{
    public Sheep(string name)
    {
        Name = name; // 现在写入继承来的 Animal.Name 属性。
    }

    // 此时仍是普通同名方法，所以截图里的 Sound 还有警告。
    public string Sound() => $"{Name} baas.";
}
```

这一步解决了 Name 的重复，但没有解决 Sound 的调用关系。要让 `Animal[]` 循环通过 Animal 类型的引用调用各自的叫声，还需要给父类方法加 virtual，给子类方法加 override。

| 修改阶段 | Name | 从 Animal 类型引用调用 Sound() |
| --- | --- | --- |
| 子类保留重复 Name 和普通 Sound | 子类与基类有不同的同名存储成员 | 调用 Animal 的非虚方法 |
| 删除重复 Name，Sound 仍是普通方法 | 使用继承的 Animal.Name | 仍调用 Animal 的非虚方法 |
| Animal.Sound 加 virtual，子类 Sound 加 override | 使用继承的 Animal.Name | 按实际对象调用对应的重写方法 |

### 5 virtual 和 override 的配合

把 Animal.cs 的 Sound() 改成截图后面的版本：

```csharp
// 放在 Animal 类内部，替换原来的普通 Sound 方法。
public virtual string Sound() => "@#$%"; // 允许派生类提供重写实现。
```

`virtual` 表示这个方法可以被派生类重写。子类不重写时，仍然可以使用基类的实现。

Dog.cs 删除自己的 Name，再把 Sound 改成 override：

```csharp
namespace QuickStart;

public class Dog : Animal // Dog 是 Animal 的派生类。
{
    public Dog(string name)
    {
        Name = name; // 使用 Animal 中定义的 Name 属性。
    }

    // 重写继承的虚方法；调用时可以按实际对象选择此实现。
    public override string Sound() => $"{Name} barks.";
}
```

Cat 与 Sheep 按介绍页中的重写规则补齐后如下，便于运行完整的三种动物示例。这里保留教程里的名字参数和叫声文字。

**Cat.cs**：

```csharp
namespace QuickStart;

public class Cat : Animal // Cat 继承 Animal。
{
    public Cat(string name)
    {
        Name = name; // 不重复声明 Name，使用继承来的属性。
    }

    public override string Sound() => $"{Name} meows."; // 猫的叫声实现。
}
```

**Sheep.cs**：

```csharp
namespace QuickStart;

public class Sheep : Animal // Sheep 继承 Animal。
{
    public Sheep(string name)
    {
        Name = name; // 初始化这个对象继承的 Name 属性。
    }

    public override string Sound() => $"{Name} baas."; // 羊的叫声实现。
}
```

父类和子类的 Sound() 都是 public、返回 string、不带参数。这里的 override 要对应可重写的基类方法；本例的普通非虚 Sound() 不能直接被 override，所以要先把 Animal.Sound 改成 virtual。

**只写同名方法不会自动建立 C# 的重写关系。父类的 virtual 和子类的 override 在这里要配合使用。** 重写也不会自动执行父类 Sound() 的方法体；当前狗、猫、羊各自返回自己的叫声。

### 6 Animal 数组与多态

**Program.cs** 对应循环截图：

```csharp
using QuickStart; // 可以直接使用 Animal、Dog、Cat、Sheep 的类型名。

Animal[] animals = // 声明元素类型为 Animal 的数组。
{
    new Dog("Fred"),     // Dog 也是 Animal，可以放进去。
    new Cat("Luna"),     // Cat 也是 Animal。
    new Sheep("Oliver") // Sheep 也是 Animal；最后的逗号可省略。
};

foreach (var animal in animals) // 每次取一个元素；这里 var 推断为 Animal。
{
    Console.WriteLine($"Animal Name: {animal.Name}"); // 读取继承的名字属性。
    Console.WriteLine(animal.Sound()); // 根据实际对象调用重写后的叫声方法。
}
```

这里的 `Animal[]` 是数组，和第五节一样使用方括号；它不是 List<Animal>。不同派生类的对象都可以放入，是因为它们都能通过 Animal 引用来使用。

| 本次循环对应的对象 | animal 的编译期类型 | 对象的实际类型 | Sound() 的实现 |
| --- | --- | --- | --- |
| Fred | Animal | Dog | Dog.Sound() |
| Luna | Animal | Cat | Cat.Sound() |
| Oliver | Animal | Sheep | Sheep.Sound() |

虽然写的都是 `animal.Sound()`，结果会随实际对象不同而改变，这就是本例中的**多态**。声明为 Animal 不会改变对象的实际类型。

截图中先完成叫声重写、还没有在 Dog.Sound 打印 Eat 时，输出为：

```text
Animal Name: Fred
Fred barks.
Animal Name: Luna
Luna meows.
Animal Name: Oliver
Oliver baas.
```

Animal.cs 使用第 2 部分的代码并应用第 5 部分的 virtual 修改，Dog.cs、Cat.cs、Sheep.cs 使用第 5 部分的版本，Program.cs 使用上面的循环。这五个文件放在同一个 Console App 项目中。

### 7 Python 的完整对照

Python 的普通实例方法可以在子类直接重新定义，不需要 virtual 或 override 关键字。调用 `animal.Sound()` 时，会按实际对象查找对应方法；因此不能把前面 C# 非虚方法隐藏的结果照搬到 Python。

下面沿用教程的 Name、Sound 拼写。Name 用普通实例属性保存，对应本例自动实现属性的简单读写；如果要实现独立的 getter、setter，可以回看上一节的 @property。

```python
class Animal:  # 基类。
    def __init__(self, name=""):  # 默认参数支持本例的无参数和带名字初始化。
        self.Name = name  # 每个实例保存自己的名字。

    def Sound(self):  # 基类提供一个通用实现。
        return "@#$%"

    def _Eat(self):  # 单下划线约定内部使用，不能强制 protected 权限。
        return f"Animal {self.Name} ate something"


class Dog(Animal):  # Dog 继承 Animal。
    def __init__(self, name):
        super().__init__()  # 调用 Animal 的初始化逻辑，先使用空名字。
        self.Name = name  # 再保存传入名字，对照截图的 Name = name。

    def Sound(self):  # 重写基类方法，不用写 override。
        return f"{self.Name} barks."


class Cat(Animal):
    def __init__(self, name):
        super().__init__()
        self.Name = name

    def Sound(self):
        return f"{self.Name} meows."


class Sheep(Animal):
    def __init__(self, name):
        super().__init__()
        self.Name = name

    def Sound(self):
        return f"{self.Name} baas."


animals = [Dog("Fred"), Cat("Luna"), Sheep("Oliver")]  # Python 用 list。
for animal in animals:  # 对应 C# 的 foreach。
    print(f"Animal Name: {animal.Name}")
    print(animal.Sound())  # 同一处调用，使用各自对象的方法。
```

这段输出与上一部分的六行结果相同。Python 的 list 本身不限制元素必须是 Animal；本例主动放入了三个继承 Animal 的对象。

`self` 始终是当前对象。在 Dog.__init__ 里调用 `super().__init__()`，是让 Animal 的初始化代码处理当前这只狗，不是另外创建一个 Animal 对象。这里采用单继承，super() 会找到 Animal。

### 8 构造函数为什么没有写 base

截图中的构造函数是：

```csharp
// 放在 Dog 类内部。
public Dog(string name)
{
    Name = name;
}
```

虽然没有显式写 base，C# 仍会先调用基类的无参数构造函数 Animal()，再执行 Dog 构造函数的方法体。因为 Animal 提供了 `public Animal() { }`，所以这版可以这样写。删除重复 Name 后，`Name = name;` 设置的是同一个对象继承的 Animal.Name。

Animal(string name) 不会因为 Dog 接收了同名参数就自动被选中。C# 的构造函数不作为构造函数被子类继承；Dog 定义自己的构造函数，并调用一个基类构造函数。

也可以显式把名字传给基类，下面是为说明调用关系补充的替代写法：

```csharp
// 放在 Dog 类内部，用它替换前面的 Dog 构造函数。
public Dog(string name) : base(name) // 调用 Animal(string name) 完成名字初始化。
{
    // 本例不用再写 Name = name。
}
```

如果基类只定义了需要参数的构造函数，又没有可访问的无参数构造函数，子类就不能继续依赖隐式的 base()，需要选择合适的基类构造函数。

对应 Python 可以把上一部分的 Dog 替换为：

```python
# 接着第 7 部分的 Animal 定义执行。
class Dog(Animal):
    def __init__(self, name):
        super().__init__(name)  # 让 Animal 的初始化代码直接保存名字。

    def Sound(self):
        return f"{self.Name} barks."

dog = Dog("Fred")
print(dog.Name)  # Fred
print(dog.Sound())  # Fred barks.
```

C# 的 `: base(name)` 与本例的 `super().__init__(name)` 都是在给当前对象调用基类的初始化逻辑。

Python 在子类自己定义了 __init__ 后，不会额外自动执行父类 __init__，需要在初始化流程有此需求时显式调用。本例用 super() 完成这一步。如果子类没有定义 __init__，则可以继承并使用父类的初始化方法。

### 9 protected Eat 和最后一张截图

Animal 中的 Eat() 是 protected。Dog 可以在自己的实例方法中调用它；Program.cs 中的普通调用者不能直接写 `dog.Eat()`。访问级别控制“谁能调用”，不决定是否打印，也不决定是不是虚方法。

| 声明 | 在本例中的用途 |
| --- | --- |
| `public string Sound()` | Program.cs 可以调用 |
| `protected string Eat()` | Animal 和派生类内部可按访问规则使用 |
| 若改成 `private string Eat()` | Dog 不能直接调用这个基类私有方法 |

最后一张截图把 Dog.Sound() 从单表达式展开为方法体：

```csharp
// 放在 Dog 类内部，替换之前的表达式体 Sound。
public override string Sound()
{
    Console.WriteLine(Eat()); // 调用继承的 Eat，得到字符串，再立即打印。
    return $"{Name} barks."; // 将叫声字符串返回给调用处。
}
```

这里调用的 Eat() 属于 Animal，不需要在 Dog 里复制一份。它读取当前这只狗继承的 Name 属性，因此返回 `"Animal Fred ate something"`。

Program.cs 仍写 `Console.WriteLine(animal.Sound());`。到 Dog 这一轮时，先完成 Sound() 内部的打印，再把返回值交给外面的 Console.WriteLine：

1. 循环先打印 `Animal Name: Fred`。
2. 进入 Dog.Sound()，Eat() 返回一句话，内部的 Console.WriteLine 打印它。
3. Sound() 返回 `Fred barks.`，外面的 Console.WriteLine 打印返回值。

如果只按最后一张截图修改 Dog.Sound，Cat、Sheep 保持前面的版本，完整循环会输出：

```text
Animal Name: Fred
Animal Fred ate something
Fred barks.
Animal Name: Luna
Luna meows.
Animal Name: Oliver
Oliver baas.
```

Python 接着第 7 部分的 Animal、Cat、Sheep 定义使用，替换 Dog 并重新创建对象：

```python
class Dog(Animal):
    def __init__(self, name):
        super().__init__()
        self.Name = name

    def Sound(self):
        print(self._Eat())  # 复用 Animal 的方法，并在方法内部先打印。
        return f"{self.Name} barks."  # 把叫声交给调用者。


animals = [Dog("Fred"), Cat("Luna"), Sheep("Oliver")]  # 创建使用新 Dog 定义的对象。
for animal in animals:
    print(f"Animal Name: {animal.Name}")
    print(animal.Sound())  # Dog 的内部打印发生在这次 print 收到返回值之前。
```

这段也产生上面的七行输出。Python 的 `_Eat` 只是“内部使用”的命名约定，外部仍能调用；C# 的 protected 则由编译器检查，不能把两者当成完全相同的权限机制。

### 10 本节几个容易混淆的词

| 概念 | 本节例子 | 关键区别 |
| --- | --- | --- |
| 继承 Inheritance | `Dog : Animal` | 建立类型关系，复用基类成员 |
| 重写 Override | `override Sound()` | 为继承的虚方法提供派生类实现 |
| 重载 Overload | `Animal()` 与 `Animal(string name)` | 同名构造函数使用不同参数列表 |
| 隐藏 Hiding | 子类重复声明 Name 或普通 Sound() | 遮住同名基类成员，不等于虚方法重写 |
| 多态 Polymorphism | 循环中的 `animal.Sound()` | 通过共同的基类类型，调用实际对象的重写方法 |

C# 与 Python 的对应关系：

| C# | Python 在本例中的对应 |
| --- | --- |
| `class Dog : Animal` | `class Dog(Animal):` |
| 子类使用继承的 Name 属性 | 使用父类初始化的 `self.Name` |
| 基类 `virtual Sound` 与子类 `override Sound` | 子类重新定义普通 `def Sound(self)` |
| 默认调用无参数基类构造函数 | 本例显式写 `super().__init__()` |
| 显式 `: base(name)` | 本例的 `super().__init__(name)` |
| `protected Eat()` | 用 `_Eat()` 表达内部使用约定，权限检查不同 |
| `Animal[]` 和 `foreach` | 本例用 list 和 for，容器类型规则不同 |

读这一节的代码时，先找每个类继承谁，再找 Name 是否只定义在基类，最后看父类 Sound 的 virtual 与子类 Sound 的 override。沿着构造函数、循环、方法内部的 return 和输出语句，就能解释截图中的名字和叫声。

参考 [C# 继承](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/object-oriented/inheritance)、[C# 方法隐藏与重写](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords)、[C# virtual](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/virtual)、[C# override](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/override)、[C# 构造函数](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/constructors)、[C# protected](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/protected)、[Python 类与继承](https://docs.python.org/3/tutorial/classes.html)和 [Python super](https://docs.python.org/3/library/functions.html#super)。

## 第十二节 Debug 调试 F10 F11 和 Watch

调试让程序在指定位置暂停，再检查执行顺序、变量的值和对象的实际类型。F10、F11 控制下一步如何执行，Locals 和 Watch 帮助观察当前状态。

这一节继续使用动物数组。截图既展示调试操作，也给出了上一节成员隐藏问题的直接证据：Cat 同时有两个 Name，而 Sheep 的 Sound 声明仍没有 override。

### 1 Debug 菜单和常用快捷键

下面按截图中的 Visual Studio Windows 快捷键记录；这些是开发工具的操作，不是 C# 语法。

| 快捷键 | 菜单名称 | 用途 |
| --- | --- | --- |
| F5 | Start Debugging 或 Continue | 开始调试；暂停时继续运行，直到下一个断点等停止条件 |
| Ctrl + F5 | Start Without Debugging | 运行程序，不启动这次调试会话 |
| F9 | Toggle Breakpoint | 在当前可执行位置设置或取消断点 |
| F10 | Step Over | 执行当前语句，通常不进入它调用的方法内部 |
| F11 | Step Into | 执行当前语句，遇到可跟进的方法调用时进入内部 |
| Shift + F11 | Step Out | 执行完当前方法的剩余部分，返回调用处附近暂停 |

断点是预先指定的暂停位置：在可执行代码左侧边栏点击，或把光标放到相应行按 F9。按 F5 后，程序运行到断点时，会在执行该位置的代码之前暂停。

**F10 仍会执行被调用的方法。** 它省略的是跟进内部代码的过程。方法里面的赋值、输出和其他行为照常发生；如果内部另有断点或遇到异常等停止条件，也可能提前暂停。

### 2 黄色箭头和黄色高亮

截图中左边的黄色箭头、代码上的黄色高亮表示调试器当前的执行位置。普通断点或单步暂停时，可以把它理解成“接下来要执行的语句”，不要当成这条语句已经执行完的标记。

第二张图高亮的是整个数组初始化：

```csharp
Animal[] animals = // 声明数组；此时初始化这条语句还没有执行完成。
{
    new Dog("Fred"),     // 创建狗，会执行构造过程。
    new Cat("Luna"),     // 创建猫。
    new Sheep("Oliver") // 创建羊。
};
```

这些代码跨了多行，但属于同一条初始化语句。按 F10 通常会执行这一条初始化，再到后面的可停位置；按 F11 可以跟进有源码可调试的构造过程。

单步并不等于每按一次键，物理行号就增加 1。循环、分支、多行语句和方法调用都会影响下一处暂停位置。

第五张图中 Sound 声明上的蓝色 string 是被选中的文本。判断调试暂停位置要看黄色执行标记，不能把普通蓝色选区当成同一件事。

### 3 在同一处比较 F10 和 F11

第三张图暂停在：

```csharp
// foreach 循环内部，黄色箭头停在这一句。
Console.WriteLine(animal.Sound());
```

这一句包含两次方法调用：先执行 `animal.Sound()` 得到字符串，再把字符串传给外面的 `Console.WriteLine`。

| 操作 | 在这个位置的作用 |
| --- | --- |
| F10 | 执行 Sound() 和外面的输出，通常不显示它们内部的逐句过程 |
| F11 | 先跟进里面的 Sound() 调用，观察实际执行的是哪一个实现 |

假设当前对象是 Dog，并且按上一节正确使用了 virtual、override，就可以跟进 Dog.Sound()。如果方法关系还存在隐藏问题，实际进入的可能是 Animal.Sound()；这正是调试可以帮助核对的地方。

上一节最后的 Dog 方法体是：

```csharp
// 放在 Dog 类内部。
public override string Sound()
{
    Console.WriteLine(Eat()); // 先调用 Eat，取得字符串后在内部打印。
    return $"{Name} barks."; // 把叫声返回调用处。
}
```

使用 F11 跟进后，可以观察 Eat() 如何读取名字，以及 return 把什么结果交回 Program.cs。使用 F10 跨过整个调用时，里面那句“吃东西”的输出也仍然发生。

Visual Studio 通常默认启用 Just My Code，并跨过属性、运算符等代码。能否进入 Console.WriteLine 这样的库代码，还受源码、调试符号和设置影响；这里优先跟进自己的 Sound()、Eat() 和构造函数。

### 4 Locals 窗口在显示什么

Locals 自动列出当前局部作用域里的变量，通常对应当前方法或函数。可以通过 `Debug > Windows > Locals` 打开，也可以暂停时把鼠标放在变量上查看值。

截图中的三列分别是：

| 列名 | 含义 |
| --- | --- |
| Name | 变量、成员或调试器显示的返回值名称 |
| Value | 当前值；对象可以展开查看成员 |
| Type | 类型信息，部分对象会同时展示声明类型和实际类型 |

第三张图暂停在循环输出叫声之前，Locals 中可以读到：

| 项目 | 截图中的值或类型 | 含义 |
| --- | --- | --- |
| `args` | `string[0]`，类型 string[] | 控制台程序的启动参数数组，这次为空 |
| `animals` | `QuickStart.Animal[3]` | 一个元素类型为 Animal、长度为 3 的数组 |
| `animal` | 值为 `QuickStart.Dog` | 本轮拿到的是 Dog 对象 |
| `animal` 的 Type | `QuickStart.Animal {QuickStart.Dog}` | 变量声明类型为 Animal，实际对象类型为 Dog |
| `Animal.Name.get returned` | `"Fred"` | 调试器显示刚才读取名字属性时得到的返回值 |
| `string.Concat returned` | `"Animal Name: Fred"` | 截图中已完成的字符串拼接调用返回值 |

后面两项是调试器显示的调用返回值，不是自己在 Program.cs 声明的两个变量。不同编译方式和调试器版本可能显示不同的内部调用名称。

因为黄色箭头已经来到 `Console.WriteLine(animal.Sound());`，前面的名字输出语句已经执行了，而本轮叫声调用还没有开始正常执行。

如果用 F11 进入 Dog.Sound()，当前方法里可直接查看的是 `this`、Name 等；Program.cs 的局部变量 animal 属于调用处的作用域，在当前上下文中可能无法求值。可以在这个实例方法内观察 `this.Name`，或切回调用处的堆栈帧查看 animal。

### 5 Cat 的两个 Name 是什么线索

第四张图展开了本轮的 Cat 对象，出现：

| Locals 成员 | 值 | 对应什么 |
| --- | --- | --- |
| `Name (QuickStart.Animal)` | `""` | 基类 Animal 的 Name |
| `Name` | `"Luna"` | Cat 自己声明的同名成员 |

这直接说明当前版本里，Cat 仍声明了自己的 Name，隐藏了继承来的 Animal.Name。给 Cat 自己的成员赋值，并没有同时更新基类的属性。

在 `foreach (var animal in animals)` 中，animal 的编译期类型是 Animal，因此 `animal.Name` 读取的是 Animal 的这个非虚属性。截图中 getter 的返回值是空字符串，拼接结果也只剩下 `"Animal Name: "`。

这与上一节的成员隐藏问题一致。修改方向是删除 Cat 中重复的 Name 声明，让构造函数使用继承的属性：

```csharp
// 对应修正思路，放在 QuickStart 命名空间中的 Cat.cs。
public class Cat : Animal
{
    // 不再另外声明一个同名 Name。
    public Cat(string name)
    {
        Name = name; // 现在给继承的 Animal.Name 属性赋值。
    }

    public override string Sound() => $"{Name} meows.";
}
```

这是根据调试结果补充的修正示例。修改后重新运行，再检查名字读取和叫声结果；调试的价值就是用实际状态解释“为什么名字看起来已经赋值了，输出却还是空的”。

### 6 Sheep 的 Sound 为什么还需要检查

第五张图中的声明是：

```csharp
// 截图中的方法，放在 Sheep 类内部。
public string Sound() => $"{Name} baas.";
```

这里没有 override。如果 Animal.Sound() 已经声明为 virtual，这种普通同名声明仍属于隐藏；通过 Animal 引用调用时，不能依靠它实现本例需要的羊叫声重写。

对应的修改是：

```csharp
// 放在 Sheep 类内部，替换上面的普通同名方法。
public override string Sound() => $"{Name} baas.";
```

然后在循环的 `animal.Sound()` 调用处按 F11，核对是否进入 Sheep.Sound()。有无 override 影响的是方法关系；仅看 Sound 的名字相同，不足以确定通过 Animal 引用会调用哪个实现。

### 7 Watch 怎么打开和使用

Watch 用来手动指定希望持续观察的变量或表达式。Locals 主要自动展示当前作用域的局部变量，Watch 则由自己添加观察项。

暂停调试时，选择 `Debug > Windows > Watch > Watch 1`。也可以先按 `Ctrl + Alt + W`，再按 `1`，这是先后两步的组合键。

在 Watch 的空白行输入表达式并确认。例如：

| 表达式 | 用来观察什么 |
| --- | --- |
| `animal` | 当前循环拿到的对象，可以展开成员 |
| `animal.Name` | 通过当前 Animal 引用读取到的名字 |
| `animals.Length` | 数组长度，本例为 3 |
| `animals[0].Name` | 数组中第一个对象通过 Animal 引用访问的 Name |
| `animal.GetType().Name` | 当前对象的实际类型名，如 Dog、Cat、Sheep |
| `animal.Sound()` | 调用 Sound()，取得它返回的字符串 |

继续单步时，可求值的观察项会随当前状态更新。若当前变量还未初始化、已经不在作用域，或调试器不能执行这次求值，Value 列会给出相应信息；Watch 不是随时都能取得每个表达式的值。

**在 Watch 里输入调用表达式也可能执行程序代码。** 本例 `animal.Sound()` 如果进入带输出的 Dog.Sound()，求值时可能会打印 `Animal Fred ate something`。因此，观察这个方法的返回值时，要区分程序正常执行和调试器额外求值带来的输出。

也可以在循环中把正常调用拆成两句，方便观察返回值：

```csharp
// 调试时可用这两句替换原来的 Console.WriteLine(animal.Sound())。
var sound = animal.Sound(); // 正常执行一次，方法内部的输出照常发生。
Console.WriteLine(sound);   // 暂停在这里时，可以在 Watch 中看 sound。
```

这里观察 sound 这个字符串变量，就不需要为了查看结果再调用一次 Sound()。

### 8 animal.Sound 和 animal.Sound() 的区别

最后一张图在 Watch 中输入的是 `animal.Sound`，没有调用括号。窗口显示了 `System.Func<string>` 以及 Method 等信息，表示当前展示的是可调用的方法或委托信息，而不是叫声字符串。

| 写法 | 在本例中的意思 |
| --- | --- |
| `animal.Sound` | 引用方法；截图展示方法或委托信息，没有执行叫声调用 |
| `animal.Sound()` | 调用方法；返回 string，方法内部的行为也会发生 |

括号中的内容是参数；Sound 不需要传参数，所以写空括号 `()`。没有参数并不表示调用时省略括号。

截图里展开后的重要信息：

| 字段 | 截图中的内容 | 含义 |
| --- | --- | --- |
| Method | `System.String Sound()` | 当前展示的方法返回字符串、不接收参数 |
| DeclaringType | `Name = "Animal"`，`FullName = "QuickStart.Animal"` | 当前展示的方法声明在 Animal 类型中 |
| Attributes | 包含 Public、Virtual | 当前展示的方法具有公开、虚方法等元数据信息 |

DeclaringType 是“这个方法声明在哪个类型”，不是“这个对象的实际类型”。要确认对象是狗、猫还是羊，查看 Locals 中的类型信息或 `animal.GetType().Name`；要确认正常调用进入哪段代码，回到调用处按 F11。

结合前面 Sheep 的普通 Sound 声明，可以用这两种观察分别核对对象类型和方法关系，不要仅凭 DeclaringType 为 Animal，就认为这个对象一定是直接创建的 Animal。

### 9 Python 也可以这样调试

F10、F11 和 Watch 属于调试工具的功能，Python 同样可以使用调试器。下面用 Python 标准库 pdb 对照，不依赖某个编辑器的快捷键设置。

这是上一节 Dog 的简化调试例子，保留 Name、Eat 和 Sound 的执行关系；把调用和输出拆成两句，方便观察返回值：

```python
class Animal:
    def __init__(self, name):
        self.Name = name

    def _Eat(self):
        return f"Animal {self.Name} ate something"


class Dog(Animal):
    def Sound(self):
        print(self._Eat())  # 方法内部先打印吃东西的句子。
        return f"{self.Name} barks."


animal = Dog("Fred")  # 本例继承 Animal 的 __init__ 完成名字初始化。
print(f"Animal Name: {animal.Name}")

breakpoint()  # 在这里进入 Python 调试器，通常是 pdb。
sound = animal.Sound()  # 可以跨过调用，也可以进入 Sound 内部。
print(sound)  # 调用完成后，查看 sound 的值。
```

进入 pdb 后，用当前箭头确认暂停位置。当箭头来到 `sound = animal.Sound()` 时，n 可以跨过这次方法调用，s 可以进入 Sound() 内部。

| 目的 | Visual Studio 中的操作 | Python pdb 对照 |
| --- | --- | --- |
| 跨过当前方法调用 | F10 | `n` 或 `next` |
| 进入方法内部 | F11 | `s` 或 `step` |
| 运行到当前方法返回 | Shift + F11 | `r` 或 `return` |
| 继续到后面的断点等停止位置 | F5 | `c` 或 `continue` |
| 查看当前名字 | 在 Watch 输入 `animal.Name` | `p animal.Name` |
| 观察这个表达式的后续变化 | Watch 保留观察项 | `display animal.Name`，在当前帧再次暂停且值变化时显示 |

进入 Python 的实例方法后，可以看 `self.Name`；进入 C# 的实例方法后，对应看 `this.Name`。

Python 也区分方法引用和调用：`p animal.Sound` 查看绑定方法对象，`p animal.Sound()` 会调用方法并查看返回值。本例后一种写法也会先打印吃东西的句子，因此同样要留意额外求值的影响。

Python 的 display 与 Visual Studio Watch 的呈现方式不同，这里对应的是观察表达式变化的用途。它不会把 Python 普通属性的规则变成 C# 同名成员隐藏的规则。

### 10 按本节截图检查一次程序

1. 在循环中的 `Console.WriteLine(animal.Sound());` 处设置断点，按 F5 开始调试。
2. 暂停后，在 Locals 展开 animal，查看当前实际类型、名字以及是否有重复的 Name。
3. 在 Watch 加入 `animal.Name`、`animals.Length` 和 `animal.GetType().Name`。
4. 用 F10 观察调用前后的结果；想跟进内部过程时，重新运行回到同一断点，改用 F11。
5. 核对进入的是 Animal.Sound 还是相应子类的重写方法，再根据代码和变量状态检查重复 Name、缺少 override 等问题。

F10 用来观察一条语句执行后的变化，F11 用来跟进变化是如何发生的，Watch 用来保留自己关心的观察项。配合截图里的 Locals，就能把执行位置、对象类型、名字和返回值连起来理解。

参考 [Visual Studio 单步与断点](https://learn.microsoft.com/en-us/visualstudio/debugger/navigating-through-code-with-the-debugger?view=vs-2022)、[Watch 和表达式求值](https://learn.microsoft.com/en-us/visualstudio/debugger/watch-and-quickwatch-windows?view=vs-2022)、[Locals 和返回值](https://learn.microsoft.com/en-us/visualstudio/debugger/autos-and-locals-windows?view=vs-2022)、[方法的 DeclaringType](https://learn.microsoft.com/en-us/dotnet/api/system.reflection.memberinfo.declaringtype?view=net-10.0)、[C# 隐藏与重写](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords)和 [Python pdb](https://docs.python.org/3/library/pdb.html)。

---

## 第十三节 Enum 枚举和模式匹配

这一章用学生成绩练习两件事：用枚举表示成绩等级，用模式匹配把分数转成等级、再把等级转成奖励。截图中的程序分成 `Grade.cs`、`Student.cs` 和 `Program.cs` 三个文件。

### 1. 为什么把字符串等级改成 enum

最初的字段是：

```csharp
public string Grade = ""; // 现在用字符串保存等级，初始内容为空字符串。
```

截图中，`SetGrade()` 会把 70–79 分设成 `"Good"`，但 `TakeBonus()` 写的是小写的 `"good"`：

```csharp
// 节选：这是截图中字符串版本的逻辑。
Grade = Score switch
{
    >= 90 => "Excellant",
    >= 80 => "Better",
    >= 70 => "Good",    // G 是大写。
    >= 60 => "Improve",
    _ => "Retry",
};

var bonus = Grade switch
{
    "Excellant" => 5,
    "Better" => 4,
    "good" => 3,        // g 是小写，与上面的 "Good" 不同。
    _ => 0,
};
```

字符串匹配区分大小写。因此，75 分会得到 `"Good"`，却匹配不到 `"good"`，最后走 `_ => 0`。这个错误可能正常编译、正常运行，只是算出错误奖励。

枚举让等级有一个明确的类型和一组命名成员。写成 `Grade.Good` 后，成员名称拼错时，编译器就能指出不存在的名称。等级的范围和奖励规则仍然由我们正确编写。

截图用了 `Excellant`，通常的英文拼写是 `Excellent`。本节保留截图中的名称，方便对照；如果自己修正，要把枚举声明和所有引用一起改成 `Excellent`。

### 2. Grade.cs：定义成绩等级

截图先创建一个 C# 文件，再把声明改成 `enum`。选择 Class 文件模板只是创建文件的方式；真正决定类型的是代码中的 `enum` 关键字。

```csharp
namespace QuickStart; // 文件作用域命名空间：本文件的类型归入 QuickStart。

internal enum Grade   // 定义一个名叫 Grade 的枚举；internal 表示同一程序集内可访问。
{
    Excellant,        // 默认对应整数 0。
    Better,           // 默认对应整数 1。
    Good,             // 默认对应整数 2。
    Improve,          // 默认对应整数 3。
    Retry             // 默认对应整数 4。
}
```

没有显式指定数值时，C# 枚举默认以 `int` 为底层类型，成员从 0 开始依次加 1。这些数字标识等级，和学生分数、奖励数量分别是不同的概念。

例如 `Grade.Good` 的底层数值是 2，但本程序中它代表 70–79 分的等级，奖励是 3。

| 写法 | 含义 |
| --- | --- |
| `Grade` | 自己定义的枚举类型 |
| `Grade.Good` | Grade 类型的一个命名成员 |
| `"Good"` | 普通字符串 |
| `Score` | 学生的整数分数 |
| `TakeBonus()` 的返回值 | 计算得到的整数奖励 |

补充一个边界：C# 允许把整数显式转换成枚举，即使这个整数没有对应的命名成员。因此，枚举提供类型和命名检查，并不自动保证所有外部数值都是已声明的成员。

### 3. Student.cs：保存学生，并计算等级与奖励

下面把截图里的修改整理成完整示例。`SetGrade()` 的枚举分支已经出现在截图中；`TakeBonus()` 的枚举版本是根据之前的奖励规则补全的，不是声称截图已展示了它的最终实现。

```csharp
namespace QuickStart
{
    internal class Student
    {
        public string Name; // 学生姓名，类型是 string。
        public int Score;   // 学生分数，类型是 int。
        public Grade Grade; // 第一个 Grade 是类型；第二个 Grade 是字段名称。

        public Student(string name, int score) // 构造函数：创建对象时接收姓名和分数。
        {
            Name = name;   // 把参数 name 存到对象的 Name 字段。
            Score = score; // 把参数 score 存到对象的 Score 字段。
        }

        public void SetGrade() // 更新对象的等级；void 表示不返回一个结果值。
        {
            Grade = Score switch // 读取 Score，选出一个等级，再赋给 Grade 字段。
            {
                >= 90 => Grade.Excellant, // 分数至少 90，结果是 Excellant。
                >= 80 => Grade.Better,   // 前一项没匹配，且至少 80。
                >= 70 => Grade.Good,     // 前两项没匹配，且至少 70。
                >= 60 => Grade.Improve,  // 前三项没匹配，且至少 60。
                _ => Grade.Retry        // 其余情况。
            }; // switch 表达式在赋值语句中；语句用分号结束。
        }

        public int TakeBonus() // 返回 int 奖励；这里不会自己打印。
        {
            var bonus = Grade switch // 根据当前等级选择奖励。
            {
                Grade.Excellant => 5,
                Grade.Better => 4,
                Grade.Good => 3, // 使用已声明的 Good 成员，修正原字符串的大小写问题。
                _ => 0          // Improve、Retry，以及其他未匹配值，都给 0。
            };

            return bonus; // 把计算结果交给调用者。
        }
    }
}
```

`namespace QuickStart { ... }` 和前面的 `namespace QuickStart;` 都是在组织命名空间。截图中灯泡提示 “Change namespace to 'QuickStart'” 是在调整 Student 的所属命名空间，不会自动把字符串转换成枚举。

这里的 `internal` 不是“仅当前文件可访问”。`Grade.cs` 与 `Student.cs` 在同一项目构建的程序集内，可以使用这些内部类型。

### 4. public Grade Grade：为什么出现两个一样的词

按照声明的位置读：

```csharp
public Grade Grade;
//     类型  字段名称
```

它和 `public string Name;` 的结构相同，只是这里字段和类型碰巧用了同一个名称。C# 允许这种写法。

在 `Grade = Score switch { ... }` 中，左边的 `Grade` 是当前学生的字段；分支里的 `Grade.Good` 则使用枚举类型的 Good 成员。刚开始读不顺很正常，可以把左边写成 `this.Grade`，明确“当前对象的字段”。

Python 中可对应为 `self.Grade = Grade.Good`：`self.Grade` 是对象属性，`Grade.Good` 是枚举成员。

### 5. switch、=>、_ 和大括号分别做什么

```csharp
Grade = Score switch
{
    >= 90 => Grade.Excellant,
    >= 80 => Grade.Better,
    _ => Grade.Retry
};
```

这段是用来拆解语法的简化示例，省略了完整程序中的 Good 和 Improve 分支。

| 符号或结构 | 在这里的作用 | Python 联系 |
| --- | --- | --- |
| `Score switch` | 对 Score 进行模式匹配，并产生一个结果值 | 可用 `if/elif`，或 `match/case` 实现相同分支逻辑 |
| `>= 90` | 关系模式：检查输入是否至少为 90 | `if score >= 90:`；在 match 中需使用 guard |
| `=>` | 将某个匹配分支连接到该分支的结果表达式 | Python 没有这种 switch 表达式分支语法 |
| `Grade.Excellant` | 该分支选中的枚举结果 | `Grade.Excellant` |
| `_` | 丢弃模式，匹配前面未选中的输入 | `case _:` 表示兜底分支 |
| `,` | 分隔分支；最后一个分支末尾可加逗号 | Python 的 case 分支用缩进组织 |
| `{ ... }` | 包住整个 switch 表达式的分支 | Python 使用冒号和缩进 |
| `;` | 结束这条赋值语句 | Python 通常换行结束语句 |

这里的 `=>` 是 switch 表达式的分支符号。后面“箭头函数”和 Lambda 也会出现 `=>`，但要根据所在结构读含义。

分支按书写顺序选择第一个匹配项。例如 95 同时满足 `>= 90`、`>= 80`、`>= 70`、`>= 60`，最终选最前面的 Excellant。因此这里按门槛从高到低排列。

这种 switch 表达式不需要 `case` 标签或 `break`。它选出一个结果值；之前学习的 `switch (...) { case ...: ... break; }` 是 switch 语句，写法和执行方式需要分别记。

### 6. 从 string 改成 enum，要把两处规则一起改

截图里刚改成 `public Grade Grade;` 时，下面仍写 `>= 90 => "Excellant"`，所以出现红色错误提示。字段现在需要 Grade 枚举值，分支仍给字符串，类型不一致。

| 修改位置 | 原来 | 改成枚举后 |
| --- | --- | --- |
| 保存等级的字段 | `public string Grade = "";` | `public Grade Grade;` |
| SetGrade 的分支结果 | `"Excellant"`、`"Good"` | `Grade.Excellant`、`Grade.Good` |
| TakeBonus 的匹配值 | `"Excellant"`、`"good"` | `Grade.Excellant`、`Grade.Good` |

构建错误弹窗问的是：“构建失败，是否继续运行上一次成功构建的程序？”

- **Yes**：运行上一次成功构建的版本。刚改的代码可能还没有编译进去。
- **No**：不启动旧版本，回到编辑器修复当前错误。

练习时可以先选 No，再在 Error List（错误列表）里查看当前错误。截图没有展示完整错误列表，不能仅凭弹窗确定是哪一行导致失败；这个修改阶段应检查 SetGrade 和 TakeBonus 是否都已完成枚举替换。

这也解释了一种调试困惑：修改源代码后，输出却像没有变化，可能运行的是旧的成功构建版本。

### 7. Program.cs：创建、计算，再输出

```csharp
using QuickStart; // 使用 QuickStart 命名空间里的 Student 等类型。

var student = new Student("John", 90); // 创建一个学生对象，存入姓名和分数。

student.SetGrade(); // 根据 90 分更新对象的 Grade 字段。
Console.WriteLine($"{student.Name} get bonus: {student.TakeBonus()}");
// 先计算 TakeBonus() 得到 5，再把它插入字符串，最后输出整行。
```

在上面的完整枚举版本中，预期输出为：

```text
John get bonus: 5
```

调用顺序是：构造对象保存数据，SetGrade 更新等级，TakeBonus 返回奖励，WriteLine 负责显示。调用 SetGrade 本身不会打印等级。

| 输入分数示例 | SetGrade 后的等级 | TakeBonus 返回值 |
| --- | --- | --- |
| 90、95 | Excellant | 5 |
| 80、89 | Better | 4 |
| 70、79 | Good | 3 |
| 60、69 | Improve | 0 |
| 59 | Retry | 0 |

当前代码只按阈值分类，没有额外验证分数必须在 0–100 之间。例如 101 也会进入 Excellant 分支。

### 8. Python 对照：Enum、if/elif 和 match/case

Python 也有枚举，用标准库的 `Enum` 定义。下面保留相同名称，便于逐行对照。Python 的 match/case 需要 3.10 或更新版本。

```python
from enum import Enum  # 从标准库导入枚举的基类。


class Grade(Enum):
    Excellant = 0  # 显式设为 0，与本章 C# 的默认编号对应。
    Better = 1
    Good = 2
    Improve = 3
    Retry = 4


class Student:
    def __init__(self, name, score):  # 对应 C# 构造函数。
        self.Name = name
        self.Score = score
        self.Grade = Grade.Excellant
        # 这一行主动模拟 C# 本例中枚举字段默认值 0 的效果。
        # Python 不会自动初始化这个属性；它也还不是按分数算出的等级。

    def SetGrade(self):  # 更新 self.Grade，不返回一个等级值。
        if self.Score >= 90:
            self.Grade = Grade.Excellant
        elif self.Score >= 80:
            self.Grade = Grade.Better
        elif self.Score >= 70:
            self.Grade = Grade.Good
        elif self.Score >= 60:
            self.Grade = Grade.Improve
        else:
            self.Grade = Grade.Retry

    def TakeBonus(self):  # 返回奖励，不在这里打印。
        match self.Grade:
            case Grade.Excellant:
                return 5
            case Grade.Better:
                return 4
            case Grade.Good:
                return 3
            case _:
                return 0


student = Student("John", 90)
student.SetGrade()  # 先按分数算出真实等级。
print(f"{student.Name} get bonus: {student.TakeBonus()}")
# 输出：John get bonus: 5
```

Python 的 Enum 需要给成员提供值。本例显式写 0–4；如果改用普通 Enum 的 `auto()`，默认编号会从 1 开始。

`SetGrade` 使用熟悉的 if/elif 最容易读。如果也想用模式匹配，可以把该方法替换成下面的版本：

```python
def SetGrade(self):
    match self.Score:
        case score if score >= 90:  # 捕获分数，再用 if guard 检查条件。
            self.Grade = Grade.Excellant
        case score if score >= 80:
            self.Grade = Grade.Better
        case score if score >= 70:
            self.Grade = Grade.Good
        case score if score >= 60:
            self.Grade = Grade.Improve
        case _:
            self.Grade = Grade.Retry
```

这段应作为 Student 的方法放在类内部，保持方法的缩进。Python 不能直接照写成 `case >= 90:`；上面的 `if` 是 guard（守卫条件）。

Python 的 `case Grade.Good:` 是匹配该枚举值。不要把它简化成 `case Good:`：单独的普通名称通常会捕获输入并绑定变量，并不是自动查找名为 Good 的枚举成员。

Python 的 match 是语句，选中一个分支后执行它的代码；本例通过 return 返回奖励，也不需要 break。普通 Python 运行不会像 C# 编译器那样提前检查所有枚举属性引用；错误成员名称通常在执行时被发现。

### 9. 为什么必须先调用 SetGrade

C# 中，类的枚举字段如果没有初始化，默认值是该枚举的 0 值。本章刚好把 Excellant 排在第一位，编号为 0。

因此，`new Student("John", 59)` 创建后、SetGrade 调用前，Grade 也暂时是 Excellant。它不是通过 59 分计算得来的。直接调用 TakeBonus 会错误地拿到 5。

| 时刻 | Score | Grade | TakeBonus 的结果 |
| --- | --- | --- | --- |
| 刚构造对象，还没有调用 SetGrade | 59 | Excellant（字段默认值） | 5 |
| 调用 SetGrade 后 | 59 | Retry | 0 |

当前教程通过 `student.SetGrade();` 保证先计算等级。以后也可以考虑在构造函数里完成等级计算；这是额外的设计改进，截图中的构造函数还没有这样做。

本节 Python 完整示例、分数边界和 match guard 替代版本已执行核对。C# 示例按截图及官方语法文档整理，本环境未编译运行它。

本节参考：[C# 枚举](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/enum)、[switch 表达式](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/switch-expression)、[模式匹配](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/patterns)、[字段与类型同名的规则](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/expressions#12872-identical-simple-names-and-type-names)、[Python Enum](https://docs.python.org/3/library/enum.html)、[Python match 与 guard](https://docs.python.org/3/reference/compound_stmts.html#the-match-statement)及 [Visual Studio 构建与运行选项](https://learn.microsoft.com/en-us/visualstudio/ide/configure-build-run-options?view=vs-2022)。

---

## 附录 下一阶段的学习路线（待学习）

目前已学到枚举与模式匹配。下面记录之后章节的用途和练习重点，详细课堂笔记继续跟着实际进度补充。

现在的 C# Console App 已经在使用 .NET。C# 是编程语言，.NET 提供运行程序的环境、类库、构建工具和应用框架。后续“学 .NET”会逐渐扩展到用这些库和框架完成项目。

以下优先级按通用 .NET 应用开发来建议，是学习安排，不是官方排名。最值得多练的是泛型与 List、异常、Nullable、接口和 Lambda；方法、类、对象、继承、调试则是理解它们的基础。

| 视频起点 | 章节 | 主要用途 | Python 联系 | 学习建议 |
| --- | --- | --- | --- | --- |
| [03:23:54](https://www.youtube.com/watch?v=KeqUmyNsNb4&t=12234s) | 多载与箭头函数 | 同名方法根据不同参数提供不同调用方式；表达式体用 => 简写方法等成员 | Python 常用默认参数或 *args；重复定义同名函数通常会覆盖前一个。表达式体方法仍是有名字的方法 | 会用；分清重载与之前的 override 重写 |
| [03:32:57](https://www.youtube.com/watch?v=KeqUmyNsNb4&t=12777s) | Nullable 可空类型 | 表达“可能没有值”，并处理缺失数据 | null 可先联系 None；类型注解机制有所不同 | 重点实践：区分未录入成绩与 0 分 |
| [03:46:33](https://www.youtube.com/watch?v=KeqUmyNsNb4&t=13593s) | 静态类与静态成员 | 访问属于类型本身的成员，无需先创建对象，例如 Math.Abs | 可联系类属性和 @staticmethod；机制并不完全相同 | 会用；分清共享成员与每个对象自己的数据 |
| [03:55:57](https://www.youtube.com/watch?v=KeqUmyNsNb4&t=14157s) | 泛型与 List | 用 List<Student> 等可增减的集合保存同类数据；泛型让代码复用时保留类型信息 | 对应 list 的集合用途；C# 的元素类型由编译器检查 | 重点实践：增、删、查、遍历学生 |
| [04:13:24](https://www.youtube.com/watch?v=KeqUmyNsNb4&t=15204s) | Object Class | 理解普通类型共同的基类，以及 ToString、Equals 等通用方法 | Python 也有 object 基类；具体类型规则不同 | 先理解和会读，深入细节可随项目补 |
| [04:21:50](https://www.youtube.com/watch?v=KeqUmyNsNb4&t=15710s) | Exceptions 异常 | 在运行发生错误时，处理异常、提供错误信息，并完成必要清理 | try/catch/finally 对应 try/except/finally；throw 对应 raise | 重点实践：读懂异常类型和调用堆栈，处理可以恢复的失败 |
| [04:33:46](https://www.youtube.com/watch?v=KeqUmyNsNb4&t=16426s) | 命名惯例与原则 | 让代码的意图更清楚，方便阅读和团队合作 | Python 常见 snake_case；C# 类型和公开方法常用 PascalCase | 现在开始养成习惯，跟随项目约定 |
| [04:46:07](https://www.youtube.com/watch?v=KeqUmyNsNb4&t=17167s) | Interfaces 接口 | 用统一的能力约定连接不同实现，便于替换实现和测试 | 可联系 Python 的鸭子类型、ABC 或 Protocol，但检查机制不同 | 重点理解；后面做 ASP.NET Core、依赖注入时尤其有用 |
| [04:55:30](https://www.youtube.com/watch?v=KeqUmyNsNb4&t=17730s) | Tuples 元组 | 临时组合几个值，或一次返回多个结果，例如最低分与最高分 | 可联系 Python 的 tuple 和多值返回；C# 常用值元组的字段可修改 | 先会读取与解构，复杂业务数据再考虑有名字的类型 |
| [05:04:43](https://www.youtube.com/watch?v=KeqUmyNsNb4&t=18283s) | Lambda 与 Func、Action、Predicate | 把一段操作或判断作为参数传给其他代码，常见于筛选、转换和回调 | 可联系 Python 的 lambda，以及把函数传给 map/filter 等操作 | 重点实践；为 LINQ 等数据处理准备 |
| [05:28:17](https://www.youtube.com/watch?v=KeqUmyNsNb4&t=19697s) | 结语 | 回顾教程与后续方向 | — | 看过后整理疑问，进入项目练习 |

### 最值得抓住的五件事

1. **泛型与 List**：先熟练使用 List<Student>、Dictionary<string, int> 这样的现成类型。理解尖括号里填写的是类型；自己设计复杂泛型可以晚些再练。
2. **Nullable**：int? 可以保存整数或 null；string? 则表达引用可能为空，并用于编译器的空值分析。string? 本身不会自动阻止运行时错误。
3. **异常**：知道哪里可能失败，读懂错误类型与调用堆栈，处理能恢复的失败。catch 后的代码应说明如何应对问题。
4. **接口**：理解“调用方依赖一种能力约定，实现类负责具体做法”。通过替换两个实现来练习，比单记 interface 语法更容易理解。
5. **Lambda**：先记三种常用委托的用途：Func 返回结果，Action 没有返回值，Predicate<T> 接收一个 T 并返回 bool。Lambda 是可以用来提供这些操作的一种写法。

03:23:54 的表达式体成员和 05:04:43 的 Lambda 都会出现 =>，但一个可以是“简写有名字的方法”，另一个是“创建匿名函数”。当前枚举章里的 switch 分支也用了 =>；它们要根据上下文辨认。

### 接下来怎样安排

如果今晚想再学一小段，可以顺着教程完成多载与 Nullable；从提供的起点看，这两章合起来约 23 分钟，再留一点时间动手。试着说明同名方法为什么能接收不同参数，以及“尚未录入成绩”为什么不能直接用 0 分表示。

之后继续静态成员和泛型与 List。接口与 Lambda 需要留出自己改代码、观察结果的时间，不要求第一次就掌握所有写法。

可以沿用目前的学生例子做一个小成绩管理程序：保存多个学生、录入成绩、按等级发奖励、处理输入错误，再增加筛选和不同输出方式。这些基础会在一个项目里连起来。

学完这组入门内容后，再补 LINQ、async/await 与 Task，并通过一个 .NET 小项目继续练习。开始做项目不需要等到每个语言细节都背熟。

视频标题和时间点按提供的目录记录；未核对视频逐句讲解。用途说明参考：[.NET 的组成](https://learn.microsoft.com/en-us/dotnet/core/introduction)、[C# 泛型](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/generics)、[可空值类型](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/nullable-value-types)、[可空引用类型](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/null-safety/nullable-reference-types)、[异常](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/exceptions/)、[接口](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/interfaces)、[依赖注入](https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection/overview)、[Lambda](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions)、[静态成员](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members)、[元组](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-tuples)及 [命名约定](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/identifier-names)。
