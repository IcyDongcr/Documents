PEP 8 -- Python编码风格指南
===

|PEP编号:|8|
|:----|:----|
|标题:|Python编码风格指南|
|作者:|Guido van Rossum <guido at python.org>, Barry Warsaw <barry at python.org>, Nick Coghlan <ncoghlan at gmail.com>|
|状态:|Active|
|类型:|Process|
|创建时间:|05-Jul-2001|
|上传历史|05-Jul-2001, 01-Aug-2013
---
内容

*   [介绍](#介绍)
*   [无脑的一致性就是恶鬼](#无脑的一致性就是恶鬼)
*   [代码布局](#代码布局)
    *   [缩进](#缩进)
    *   [制表符TAB还是空格?](#制表符TAB还是空格)
    *   [行的长度限制](#行的长度限制)
    *   [如何对二元运算换行?](#如何对二元运算换行)
    *   [空行](#空行)
    *   [源文件编码](#源文件编码)
    *   [Imports 导入](#Imports导入)
    *   [模块等级名称修饰duders](#模块等级名称修饰duders)
*   [字符串的引号](字符串的引号)
*   [语句、表达式中的空格](#语句、表达式中的空格)
    *   [空格的小烦恼](#空格的小烦恼)
    *   [其他建议](#其他建议)
*   [何时使用尾随逗号](#何时使用尾随逗号)
*   [注释](#注释)
    *   [注释块](#注释块)
    *   [行内注释](#行内注释)
    *   [文档字符串](#文档字符串)
*   [命名规范](#命名规范)
    *   [最高原则](#最高原则)
    *   [描述:命名规范](#描述命名规范)
    *   [规范:命名规范](#规范命名规范)
        *   [需要避免使用的](#需要避免使用的)
        *   [ASCII兼容性](#ASCII兼容性)
        *   [包及模块的命名](#包及模块的命名)
        *   [类的命名](#类的命名)
        *   [类型变量命名](#类型变量命名)
        *   [异常命名](#异常命名)
        *   [全局变量命名](#全局变量命名)
        *   [方法及变量名](#方法及变量名)
        *   [方法及函数的参数](#方法及函数的参数)
        *   [函数名与实例变量](#函数名与实例变量)
        *   [常量](#常量)
        *   [继承的设计](#继承的设计)
    *   [Public and Internal Interfaces](#public-and-internal-interfaces)
*   [Programming Recommendations](#programming-recommendations)
    *   [函数注释](#函数注释)
    *   [Variable Annotations](#variable-annotations)
*   [References](#references)
*   [Copyright](#copyright)

[介绍](#介绍)
=====================

本文基于Python主版本中的代码给出了一些编码规定。请参考[Style Guide for C Code PEP-7](https://www.python.org/dev/peps/pep-0007)(译者：这篇文章也是Guido写的)

本文以及[文档字符串规范 PEP-257](https://www.python.org/dev/peps/pep-0257/) 都是来自于Guido所写的 Python风格指南，以及[巴里的风格指南](https://barry.warsaw.us/software/STYLEGUIDE.txt)的补充。

时间的变迁，本指南与Python一样，会不断的推陈出新。

许多项目有着自己的编码风格，冲突的时候，请不要因本文，禁锢自己的想法。

[无脑的一致性就是恶鬼](#无脑的一致性就是恶鬼)
===============================================================

Guido有一个重要的观点是：一段代码更多是被阅读，而不是编写。这篇指南的目的于此一致，通过保持Python代码风格的一致，提高它的可读性。就如同[Python之禅](https://www.python.org/dev/peps/pep-0020/)中说的一样“可读性应当被重视”。

风格指南，其实就是一致性的指南。编码风格的一致性很重要，一个项目中的编码风格一致性更加重要，但是，一个模块或者方法中的一致性是最重要的。

但是，千万不要墨守成规。知道何时需要违背这篇文章的内容，是重点。当犹豫不决的时候，根据自己的需要和想法，做出你的决断。也可以看看其他人的例子，并不耻下问。

特别注意：不要为了遵守本指南，影响了向后的兼容性。

在以下的情况，也可以舍弃一些成规：
1. 当遵守风格会降低代码可读性的时候，即使是这边指南所推荐的风格。
2. 风格和项目其他部分的代码风格相冲突的时候。（有可能是因为某个历史原因）---当然，这也是纠正这些错误的机会（真正的极限编程）。
3. 风格诡异的旧代码已经无法挽救的时候。
4. 需要兼容旧版本Python不支持相关特性，而你的代码需要兼容旧版本Python的时候。

[代码布局](#代码布局)
=====================

[缩进](#缩进)
--------------------

使用4个空格为一次缩进。

续行的时候，元素需要与被圆括号、方括号、花括号内的其他元素对齐，也可以使用悬挂式缩进。在使用悬挂式缩进的时候，需要增加一个缩进的级别。

Yes:
推荐的：
```python
# 与括号中的元素对齐
foo = long_function_name(var_one, var_two,
                          var_three, var_four)

# 可以使用更多级的缩进，来和其他内容区分开
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

# 悬挂式的换行代码，最好增加一级缩进
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)
```
不推荐的:
```python
#没使用垂直对齐的情况下，不要把参数放在第一行
foo = long_function_name(var_one, var_two,
    var_three, var_four)

# 需要增加缩进的级别来和其他内容区分开
def long_function_name(
    var_one, var_two, var_three,
    var_four):
    print(var_one)
```
续行的时候，一级缩进并不一定需要是4个空格

可选的:
```python
# 悬挂式缩进时，缩进*可以*不是4个空格
foo = long_function_name(
  var_one, var_two,
  var_three, var_four)
```

[](#多行IF语句的缩进)当if语句中的条件足够长的时候，需要写到多行里时，值得注意的是，假如是两个字符（比如:if）再加上一个空格，和一个左括号的时候，会自然的产生4个空格的缩进。这种情况下，if的条件内容，会和if语句的内容看上去在同级别内。本文并不明确 要不要区分他们，也不明确如何区分这些内容。可以选择的情况包含但不限于以下：
```python
# 没有手动增加缩进
if (this_is_one_thing and
    that_is_another_thing):
    do_something()

# 增加一段注释，在某些编辑器中会有比较明显的
# 特别是有高亮功能的编辑器
if (this_is_one_thing and
    that_is_another_thing):
    # Since both conditions are true, we can frobnicate.
    do_something()

# 对续行的条件手动增加一级缩进
if (this_is_one_thing
        and that_is_another_thing):
    do_something()
```

(另请参看，下文关于二元运算相关的内容)

多行结构中，可以将 ）、]、} 另起一行,并与内容对齐，如：
```python
my_list = [
    1, 2, 3,
    4, 5, 6,
    ]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
    )
```

或者让它们比内容少一个缩进级别, 如:
```python
my_list = [
    1, 2, 3,
    4, 5, 6,
]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
)
```

[制表符TAB还是空格?](#制表符TAB还是空格)
------------------------

空格是首选。
当已经有代码使用制表符时，首选使用制表符。
Python3里不能同时使用空格和制表符。
在Python2中，如果二者都存在，最好统一转为空格。
Python2的解释器中，设置-t时，空格和制表符混用会报警，设置-tt时，则会报错。强烈推荐！

[行的长度限制](#行的长度限制)
----------------------------

行的最大长度限制是79个字符。

对于结构化限制少的长文本（文档字符串或者注释），每行的长度限制是72个字符。

限制编辑器窗口的宽度，可以使多个文件并排。在使用代码检查工具的时候，这种方式，可以让相同行代码现实在同一个高度，得到很高的用户体验。

很多工具的默认封装会破坏代码的结构，降低代码的可读性。这些限制是为了避免代码在宽度设置为80的编辑器中换行，即使是进行了换行，也会添加一个标志符号。一些基于Web的工具也可能不支持动态换行。

一些团队希望可以增加行的长度限制。对于内部的项目和代码，在意见统一的情况下，可以将行的长度限制从80提升到100（最大有效字符长度为99），但是注释和文档字符串的长度限制仍然为72个字符。

Python标准库使用79个字符长度的限制（注释和文档字符串的长度限制为72个字符）。

对于过长的代码，首先应该考虑在改行的各种括号处进行续行的操作。在实在不行的情况下，才使用反斜杠的方式续行。

但是有些时候，反斜杠更加适用。比如：过长或者多个with的语句。在括号处续行会降低可读性，但是使用反斜杠效果却很好：

```python
with open('/path/to/some/file/you/want/to/read') as file_1, \
     open('/path/to/some/file/being/written', 'w') as file_2:
    file_2.write(file_1.read())
```
（请参看之前关于[多行IF语句的缩进](#多行IF语句的缩进),进一步了解多行语句的缩进）

使用断言的时候也需要适当的进行手动换行与缩进。

[如何对二元运算换行?](#如何对二元运算换行)
---------------------------------------------------------------
一直以来，都是推荐在运算符之后进行换行。但是会有两个问题：运算符不在同一列，运算符和操作数被分割在不同的行。下面的例子中，``哪些变量``做了``哪些操作``就比较难分辨:

```python
# 不推荐: 运算符和操作数不在同一行
income = (gross_wages +
          taxable_interest +
          (dividends - qualified_dividends) -
          ira_deduction -
          student_loan_interest)
```
为了解决这个问题，数学家以及出版商使用了另一套约定。Donald Knuth再他的[《Computers and Typesetting》](https://www-cs-faculty.stanford.edu/~knuth/abcde.html)中介绍到：虽然运算是在运算符之后中断，但是显示的时候，总是在运算符之前中断。[\[3\]](#id10)

遵循数学家的这个原则，通常可以让代码变得更加容易读懂：

```python
# 推荐: 更容易的将运算符和操作数匹配起来
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)
```

在Python中，只要保持同一种风格，不论是在之前还是之后打断语句都是可以的。但是，还是推荐数学家的原则。

[空行](#空行)
--------------------
在定义顶级方法(Function)和类(Class)之前，使用两行空行作为分隔。

在定义类中的函数(Method)的时候，使用单行空行作为分隔。

可以(谨慎的)使用额外的空行来分隔相关联的功能模块。也可以在相关联的功能模块中，定义方法时，不用空行隔开。（例如：几个方法组成的一个虚拟功能）。

在一个方法中请谨慎使用空格来分隔代码逻辑。

Python可以用control-L(^L)表示为空行；很多工具将其视为分页符，所以你可以使用它来分隔文件内容。(译者:control-L应该是某个控制符，没找到明确的相关文档说明)。注意，有些编辑器和基于WEB的代码阅读器并不识别control-L，在提交表单的时候，会用其他符号替代它。

[源文件编码](#源文件编)
-----------------------------
Python发布版中的代码，使用使用UTF-8作为编码格式（Python2使用ASCII）

文件内容使用ASCII编码（Python2）或者UTF-8（Python 3），并不再另外声明。

在标准库中，除了是测试代码以及注释和作者名称内含有非ASCII字符的情况下，都应该使用默认编码格式；否则，均应该使用\\x,\\u,\\U或者\\U转义非ASCII字符。

对于Python3.0及以上版本，标准库遵循以下规则([参见 PEP 3131](https://www.python.org/dev/peps/pep-3131/#id17)):所有标准库只可以使用ASCII标识符，尽量使用英文单词（在很多案例中，缩写及专业词语并没有使用英文）。此外，注释以及字符串也必须是ASCII。例外情况又：(a)测试非ASCII的代码，(b)作者名。名字不基于拉丁文字母表(latin-1, ISO/IEC 8859-1 character set)的，需要提供名字的音译。

希望全球的所有开源项目的用户都使用相类似的策略。

[Imports 导入](#Imports导入)
----------------

*   导入通常需要放在不同行:
    *   推荐的:
        ```python
            import os
            import sys
        ```
    * 不推荐的:
        ```python
            import sys, os
        ```
    
    * 也可以这样:
        ```python
            from subprocess import Popen, PIPE
        ```
    
*   导入通常在文件的顶部，模块说明及文档之后，变量、常量之前。
    
    导入应该按照以下顺序进行分组:
    1.  标准库
    2.  第三方库
    3.  本地相关库
    
    最好使用空行来分隔这三组Import.
    
*   强烈建议使用绝对路径导入，因为如果没有配置好的话（比如包中的某个目录在sys.path之后）,绝对路径的可读性更好并且性能也更好（至少报错信息更清晰）：
    ```python    
        import mypkg.sibling
        from mypkg import sibling
        from mypkg.sibling import example
    ```
    
    无论如何，显式的相对导入的方式是可以替代绝对路径导入的。特别是在导入路径过于冗长及复杂的情况是：
    ```python
    from . import sibling
    from .sibling import example
    ```
    标准库中的包结构应该简单，并且使用绝对路径导入。
    
    隐式的相对路径导入已经在Python3中删除了，不要使用它。
    
*   当从一个模块中导入某个类的时候，一般这样写:
    ```python
    from myclass import MyClass
    from foo.bar.yourclass import YourClass
    ```
    
    如果上面的做法存在名字冲突的时候，可以这样做:
    ```python
    import myclass
    import foo.bar.yourclass
    ```
    然后使用"myclass.MyClass"和"foo.bar.yourclass.YourClass".
    
*   应该避免使用通配符导入(from \<module\> import *),因为这样的方式，无法知道导入了什么，也即不知道命名空间中到底添加了什么。使读者和很多自动化工具产生困扰。对于通配符导入，有一种合理的使用方式，将内部API，重新定义为公共API的一部分（例如，用纯Python重写某个模块，但是事先不清楚模块哪些内容需要被重写）。使用这种方式的时候，以下关于API的指南同样适用。
    

[模块等级 名称修饰duders](#模块等级名称修饰duders)
----------------------------------
"duders"(也就是用两个下划线开头，两个下划线结尾) 例如：\_\_all\_\_,\_\_author\_\_, \_\_version\_\_ .... 定义它们的地方，应该放在模块的备注文档之后，但是在导入语句之前（除了from \_\_future\_\_ import ）。Python要求future-import需要在置顶的注释段之后，在其他任何代码之前。

例如
```python
"""This is the example module.

This module does stuff.
"""

from __future__ import barry_as_FLUFL

__all__ = ['a', 'b', 'c']
__version__ = '0.1'
__author__ = 'Cardinal Biggles'

import os
import sys
```
（译者：duders 的用处主要在使变量私有，以及避免方法与父类重名。经常出现在内建变量中）

[字符串的引号](#字符串的引号)
======================
Python中，双引号和单引号的字符串是一样的。但是本文是不建议混用的。确定一种习惯的规则，统一使用一种方式。但是，当字符串中包含单引号或者双引号的时候，可是直接使用反斜杠来转译，为了提高可读性（只包含单引号或者只包含双引号时），也可以使用一种来包含另一种，这样就不需要反斜杠转译了。

三引号的使用规范与双引号的约定一致。相关文档字符串规定参见[Python文档字符串约定PEP257](https://www.python.org/dev/peps/pep-0257/)

[语句、表达式中的空格](#语句、表达式中的空格)
=================================================

[空格的小烦恼](#id27)
-------------------

在以下情况中，空格的使用需要格外注意:

*   在各种括号的相邻位置。
    * 推荐的：
        ```python
        spam(ham[1], {eggs: 2})
        ```
    * 不推荐的：
        ```python
        spam( ham[ 1 ], { eggs: 2 } )
        ```
    
    
*   逗号和又括号之间.（译者：其实是上面的一种特殊情况）
    * 推荐的：
        ```python
        foo = (0,)
        ```
    * 不推荐的：
        ```python
        bar = (0, )
        ```
    
*   逗号、冒号、分号的左侧:
    * 推荐的：
        ```python
        if x == 4: print x, y; x, y = y, x
        ```
    * 不推荐的：
        ```python
        if x == 4 : print x , y ; x , y = y , x
        ```
* 在切片中，冒号应该被当作一个运算符（最低优先级运算符）来看待。冒号左右的空格，应该与其他运算符保持一致。在扩展切片中（使用两个冒号的情况），两个冒号左右的空格规则应该保持一致。除非：缺少一个参数的时，该参数左右的冒号之间，空格应该被省略。
    * 推荐的：
        ```python
        ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
        ham[lower:upper], ham[lower:upper:], ham[lower::step]
        ham[lower+offset : upper+offset]
        ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
        ham[lower + offset : upper + offset]
        ```
    * 不推荐的：
        ```python
        ham[lower + offset:upper + offset]
        ham[1: 9], ham[1 :9], ham[1:9 :3]
        ham[lower : : upper]
        ham[ : upper]
        ```
*   调用函数及方法的左括号的左侧:
    * 推荐的：
        ```python
        spam(1)
        ```
    * 不推荐的：
        ```python
        spam (1)
        ```

    
*   索引和切片的左括号的左侧(译者：这里并没有举出切片的例子，但是之前专门的切片说明中有相关例子):
    * 推荐的：
        ```python
        dct['key'] = lst[index]
        ```
    * 不推荐的：
        ```python
        sdct ['key'] = lst [index]
        ```
    
*   不要使用多个空格让多个表达式或赋值语句的左右内容在列上保持一致.
    * 推荐的：
        ```python
        x = 1
        y = 2
        long_variable = 3
        ```
    * 不推荐的：
        ```python
        x             = 1
        y             = 2
        long_variable = 3
        ```

[其他建议](#其他建议)
------------------------------
* 不要在语句的尾部使用空格。因为他们是不可见的，而且容易被混淆。比如：反斜杠之后的空格，换行时相关内容是不被承认的。有的编辑器都不承认他们（比如CPython）

* 在运算符的左右，使用一个空格：赋值（=），增广赋值(+=,-=...),比较(=、<、>、!=、<>、<=、>=、in、not in、is、is not),布尔运算符(and, or, not)

* 如果使用不同优先级的运算符，根据情况在低优先级的表达式左右添加空格。主要靠自己的判断，但是，不要使用多个空格，而且要保证语句运算符左右的空格是一致的。
    * 推荐的：
        ```python
        i = i + 1
        submitted += 1
        x = x*2 - 1
        hypot2 = x*x + y*y
        c = (a+b) * (a-b)
        ```
    * 不推荐的：
        ```python
        i=i+1
        submitted +=1
        x = x * 2 - 1
        hypot2 = x * x + y * y
        c = (a + b) * (a - b)
        ```
* 函数、方法的注释，应该遵循冒号的一般规则。并且在箭头左右留有空格。（更多内容参见[函数注释](#函数注释)）(译者：以下的内容均是注释语句，并不是Python的代码)
    * 推荐的：
        ```python
        方法注释
        def munge(input: AnyStr): ...
        def munge() -> AnyStr: ...
        ```
    * 不推荐的：
        ```python
        def munge(input:AnyStr): ...
        def munge()->PosInt: ...
        ```
* 当使用kwargs的时候，（例如:def func(key=value)），不要在等号两边留空，或者在有默认值的入参(例如:def func(value=0.0))，等号两边也不要留空。
    * 推荐的：
        ```python
        def complex(real, imag=0.0):
            return magic(r=real, i=imag)
        ```
    * 不推荐的：
        ```python
        def complex(real, imag = 0.0):
            return magic(r = real, i = imag)
        ```
    注释中，有默认值的入参，需要在等号的两边留空（译者：以下都是注释，不是Python代码,limit=100的空格使用原文如此）：
    * 推荐的：
        ```python
        def munge(sep: AnyStr = None): ...
        def munge(input: AnyStr, sep: AnyStr = None, limit=1000): ...
        ```
    * 不推荐的：
        ```python
        def munge(input: AnyStr=None): ...
        def munge(input: AnyStr, limit = 1000): ...
        ```
*   不推荐使用复合语句（同一行存在多条语句）.
    * 推荐的：
        ```python
        if foo == 'blah':
        do_blah_thing()
        do_one()
        do_two()
        do_three()
        ```
    * 不推荐的：
        ```python
        if foo == 'blah': do_blah_thing()
        do_one(); do_two(); do_three()
        ```
* 虽然有时候将if/for/while和之后的执行语句放在同一行是可以的。但是如果语句过多，千万不要这样。折叠语句的时候会让显示的语句过长。
    
    * 不推荐的：
        ```python
        if foo == 'blah': do_blah_thing()
        for x in lst: total += x
        while t < 10: t = delay()
        ```
    * 绝对不要：
        ```python
        if foo == 'blah': do_blah_thing()
        else: do_non_blah_thing()
        
        try: something()
        finally: cleanup()
        
        do_one(); do_two(); do_three(long, argument,
                                     list, like, this)
        
        if foo == 'blah': one(); two(); three()
        ```
[何时使用尾随逗号](#何时使用尾随逗号)
====================================

尾随逗号一般都是可用可不用的。也有一些情况尾随逗号是语句的元素之一（在python2中，print中尾随逗号是具有实际意义的）。为了区分这些情况，建议将后者写在括号中（为了增加可读性，添加的冗余代码）。

* 推荐的:
    ```python
    FILES = ('setup.cfg',)
    ```
* 不推荐的，容易产生歧义:
    ```python
    FILES = 'setup.cfg',
    ```

当用来进行版本的配置控制时，当相关参数会跟随时间而拓展的时候。虽然这种情况下尾随逗号是多余的，但是很有用。比较好的方式是，每个参数单独写在一行中，在末尾添加一个尾随逗号，右括号也单独写一行。这样最后一个尾随逗号是没有意义的，但是在添加的时候会很方便，而且格式统一，不容易产生失误。（只有一个元素的配置除外）
* 推荐的:
    ```python
    FILES = [
        'setup.cfg',
        'tox.ini',
        ]
    initialize(FILES,
               error=True,
               )
    ```
* 不推荐的:
    ```python
    FILES = ['setup.cfg', 'tox.ini',]
    initialize(FILES, error=True,)
    ```

[注释](#注释)
=================
与代码意义相矛盾的注释是最糟的注释。所以当代码变更的时候，注释一定要更新。

注释应该是完整的句子。英文注释的第一个单词应该是大写（当然，不要更改标识符的大小写，以免造成对代码的误解）。

注释段应该是由一个或者多个完整的句子组成的，每个句子需要以句号结尾。

注释段中。每个完整的句子结束后，需要使用两个空格与下语句隔开。当然，最后一句话不需要。

当使用英文编写注释的时候，请跟随“斯特伦克和怀特”(即特伦克的《风格指南》)

注释编写人员如果来自于一个英语不是常用语的国家：除非你120%确定，读你注释的人绝大部分都看得懂你的语言，不然，请用英语编写注释。

[注释块](#注释块)
-----------------------

注释块通常用来解释之后的部分（或者全部）的代码内容。需要将注释块缩进到与相关代码同一个级别。注释块的每一行都以一个#加一个空格开头（当然，注释中包含缩进的情况除外）。

注释块内的段落分隔应该是用一个空行来表示。（译者：这个空号也要包含一个#）

[行内注释](#行内注释)
------------------------
谨慎使用行内注释。

行内注释和要说明的语句应该在同一行。注释和语句之间至少相隔两个空格。注释语句应该与#相隔一个空格。

行内注释如果不是必要的情况，是会分散读者的注意力。

* 不推荐的:
    ```python
    x = x + 1                 # x增加
    ```
* 推荐的:
    ```python
    x = x + 1                 # 补偿边界值
    ```
[文档字符串](#文档字符串)
------------------------------
编写文档字符串（即，“docstrings”）的约定，[PEP 257](https://www.python.org/dev/peps/pep-0257/)已经写的很好，也很经典。

* 所有的公共（public）模块，方法，类和函数都需要写docstrings。非public的函数不需要。但也应该编写注释来解释函数的功能。这段注释可以在函数定义(def 语句)之后。
* [PEP 257](https://www.python.org/dev/peps/pep-0257/)叙述了编写docstrings的相关约定。需要注意的重点是，结束整个docstrings的三个引号，应该单独在一行。如下：
    ```python
    """Return a foobang
        
    Optional plotz says to frobnicate the bizbaz first.
    """
    ```
    
*   如果docstrings只有一行，则不需要遵守以上规定。建议将截止的引号与内容，防止在同一行。
    
[命名规范](#命名规范)
===========================

Python库的命名规范比较混乱。所以我们没有办法得到一个统一的规范 -- 尽管如此，这里仍然推荐目前的命名标准。希望大家按照相关标准编写新的库和包（以及第三方框架），当然，如果已经有了自己的风格规范，还是以保证协作团队内部的风格为主。


[最高原则](#最高原则)
-----------------------------

展示给用户看的公共部分，名称反应的应该是API的用法，而不是实现。

[描述:命名规范](#描述命名规范)
-----------------------------------

命名的风格是有多种的，不同的命名风格，应该有不同的用途。这样会更加方便的识别相关内容。

以下是不同的命名风格:

*   b (一个小写字母)
    
*   B (一个大写字母)
    
*   纯小写的字母组合
    
*   lower\_case\_with_underscores （下划线分割的小写）
    
*   UPPERCASE （纯大写的字母组合）
    
*   UPPER\_CASE\_WITH_UNDERSCORES （下划线分割的大写）
    
*   CapitalizedWords (或者 CapWords, 或者 CamelCase -- 单词的首字母大写). 称之为大驼峰式命名法.
    
    注意：当使用缩写的时候，需要每个字母都大写。比如：HTTPServerError 比 HttpServerError 更好。
    
*   mixedCase (从第二个单次开始，首字母大写。称之为小驼峰式命名法)
    
*   Capitalized\_Words\_With_Underscores (非常丑的命名风格。)
    
有一种使用简短且唯一的前缀讲相关名称进行分组的风格。这种用法在Python很少，但是为了规定的完整性，所以在这里提到。例如：os.stat()方法返回的是一个元组。这个元组的内容，被命名为st_mode,st_size,st_mtime等等。（这里的做法，是为了强调POSIX系统与相关字段的对应关系，便于程序员更好的理解它们。）

X11库中的所有公共方法，也以x开头。但是在Python中，这种做法并不是必要的。因为属性、函数、方法都是以对象或者模块名为前缀的。

此外，还有使用前置，后置下划线的特殊风格（这些内容通常可以和其他所有风格相结合使用）：

*   \_single\_leading_underscore: 前置单下划线，非强制的私有标识。例如：from M import * 不会导入这种类型的对象。

*   single\_trailing\_underscore_: 后置单下划线，用于与Python关键字冲突的地方。例如：Tkinter.Toplevel(master, class_='ClassName')
    
*   \_\_double\_leading_underscore: 前置双下划线，类的私有变量 (在执行的之后，这类变量的名称将会被重新整理，比如class FooBar中的 __boo 会被整理为  \_FooBar\_\_boo; 详见下文).
    
*   \_\_double\_leading\_and\_trailing\_underscore\_\_: 前后均双下划线，"magic"对象或者属性。更多的存在在用户可以可以操作的命名空间中。例如： \_\_init\_\_, \_\_import\_\_ or \_\_file\_\_. 不要自己编造此风格的名称，只使用官方提供。
    

[规范:命名规范](#规范命名规范)
-----------------------------------------

### [需要避免使用的](#需要避免使用的)
切勿使用字符"l"(小写的L),"O"(大写的O)，或者"I"(大写的eye)单个字符来命名变量。

在某些字体中，以上字符与数字1和0并不容易区分开。而且当需要使用小写L的时候，使用大写L代替。

### [ASCII兼容性](#id39)

标准库中的标识符，必须与ASCII兼容。详见 [PEP 3131](https://www.python.org/dev/peps/pep-3131/)中的[policy section](https://www.python.org/dev/peps/pep-3131/#policy-specification)

### [包及模块的命名](#id40)

模块名应该简短，且全小写。为了增加可读性，可以使用下划线分隔单词。Python的包名也应该是简短、全小写。但是不建议使用下划线分隔。

在使用C或者C++编写的Pyhon拓展模块中，提供的更高级别接口（例如：更加面向对象）：C/C\+\+的模块会增加一个前置下划线(例如:_socket)。

### [类的命名](#类的命名)

类的命名应该使用大驼峰式命名法（例如CapWords）。

如果方法是可以被调用的，方法的命名可以用它的主要作用来命名。

需要注意的是，对于内建方法的命名有个单独的约定：大多数内建方法的名称是单个单词（或两个无下划线分隔的全小写单词），驼峰类的命名规则，只在异常名或者内建常量时使用。

### [类型变量命名](#类型变量命名)

类型变量的命名在 [PEP 484](https://www.python.org/dev/peps/pep-0484/)中提到，使用缩写单词的大驼峰命名法，例如： T, AnyStr, Num。类型变量如果具有协变或者逆变的行为（译者：其实就是强类型语言中泛型的上下边界，比如java的extends和super），建议在结尾加上_co和_contra以作区分:
```python
from typing import TypeVar

VT_co = TypeVar('VT_co', covariant=True)
KT_contra = TypeVar('KT_contra', contravariant=True)
```
### [异常命名](#异常命名)

因为异常应该是类，所以异常的命名也使用类的命名规定。但是，需要在类名之后加上"Error"以作区分(如果异常是一个错误的话)。

### [全局变量命名](#全局变量命名)
（希望这些全局变量只在一个模块中使用到。）全局变量的命名规则与方法名的约定基本一致。

从 from M import * 的导入机制中使用到 \_\_all\_\_可以看出，它本身是不建议导出模块中的全局变量的。也有使用者习惯使用下划线作为某个模块中私有的全局变量标识（表明这个全局变量其他模块不要导入或使用）。

### [方法及变量名](#方法及变量名)

方法名应该是全小写，可以使用下划线分隔单词来提高可读性。

变量名与方法名遵循同一规则。

类似于mixedCase的小驼峰式命名只建议在，为了保证旧有项目的向下兼容性时使用（例如 threading.py）。

### [方法及函数的参数](#方法及函数的参数)

使用self作为实例方法的第一个参数。

使用cls作为类方法的第一个参数。

如果方法的参数与关键字冲突，通常使用后置下划线以作区分，而不建议使用缩写或者通假字,比如参数名是class时，可以使用class_,而不建议使用clss。(如果能使用近义词或者其他方式来避免这种冲突是最好的。)

### [函数名与实例变量](#函数名与实例变量)

使用方法名的规则：全小写，可以使用下划线分隔单词来提高可读性。

非公有的函数及实例变量使用一个前置下划线与其他内容区分。

为了避免与子类中的名称冲突，或者不希望被子类所调用。也可以当做私有的函数或者变量。可以使用前置的双下划线进行命名。

Python使用类名对这种名称进行了重新整理：比如在类Foo中，有一个属性为\_\_a，这个属性是私有的，它的实例或者子类是不同通过Foo.\_\_a的方式来调用它的。(较真的话，其实还是可以通过Foo._Foo\_\_a的方式调用到它的。)通常前置的双下划线只用于避免名称冲突和设计中用来避免与子类的冲突。

注意：关于前置双下划线的使用还是存在一些争议的（详见下文）。

### [常量](#常量)

常见一般在模块级别中定义，使用全大写字母命名，使用下划线分隔单词。比如：MAX_OVERFLOW、TOTAL。

### [继承的设计](#继承的设计)

首先需要确定的是，类的函数和实例变量（二者统称："属性"）是否是公共的，即``public or non-public``。如果不是很确定，那就使用非公共。因为将一个非公共属性设置为公共属性是比较简单的，反之则相对麻烦。

公共属性是预期中会被第三方使用的属性，可以使用委托机制来解决向后兼容的问题（译者：就是使用\_\_getattr\_\_）。非公开属性是预期中不会被第三方使用的；当然，非公开属性被强行更改或删除的情况也是存在的。

在这里，我们没有使用“私有”这个词，是因为在Python中没有真正意义上的私有属性。（为了减少大量非必须的常规工作量）

另一种属性是属于"subclass API"(在其他语言中一般称之为"protected")。一些类设计为需要被继承，用来拓展和修改类的属性或行为。当设计这样一个类的时候，需要注意哪些属性是公共的，哪些属性是给集成它的子类使用的，哪些是基类使用的。

关于这一点，以下是Python的指南：

*   公共属性不要使用前置下划线。

*   如果公共属性的名字与保留的关键字冲突了，使用后置单下划线以示区分。尽量不要使用缩写或者使用变种的拼写方式。(虽然有着不建议使用缩写的规定，但是类方法的第一个参数，任然是"cls"虽然它是一个缩写。同时，也首选使用"cls"代表''类'，不论是变量或参数时。)
    
     注 1：类方法命名参见上面的函数命名规则

*   对于简单的公共数据属性，最好只公开它的属性名，而不提供复杂的访问器/修改器方法。请记住，如果有简单的数据属性需要拓展方法操作，Python提供了很简单的实现途径。可以使用property函数（装饰器）来进行隐式的属性操作拓展。
    
    注 1：property只在新式类中才有效。（译者：新式类是python2.2引入的特性，现在一般都是新式类了，如果还不放心，type(class的实例),如果不是<type 'instance'>，那就是新式类。因为新式类需要解决的就是class与type概念的统一）
    
    注 2：尽量不要增加附加功能（译者：原文中是side-effect，但是在Python中指的是附作用，而不是一般语义中的副作用），尽管这些附加功能对资源损耗很小。
    
    注 3：由于类的函数经过property装饰器，会让用户在调用相关函数的时候，会有一种调用实例变量的感觉。会造成，调用这些属性没有什么资源消耗的错觉。所以，使用property装饰器的时候，需要避免进行过于过于复杂的操作。

*   如果预期中，你的类需要被子类继承。但是基类中有一些属性，不希望被子类访问到。可以使用前置双下划线（形如\_\_funciton,千万不要\_\_funciton\_\_）。这样可以做到貌似私有属性的效果，但是它的实际做法是：将类名加一个前置下划线，变更为属性名的方式来避免子类通过常规的方式来调用它，虽然它仍然可以被调用到。这也可以用来避免子类与基类的属性同名。

    注 1：只有简单的类名才使这个机制成功，如果子类的类名和属性名都相同的话，你仍然会收到名称冲突的提示。
    
    注 2：这种伪私有的实现机制可以被使用在 调试 和 \_\_getattr\_\_()中，虽然不是非常方便，但是有很详尽的文档，容易实现。

    注 3：Python的这种伪私有实现机制，并不是所有人都喜欢。尝试着调整需求，避免因为意外造成名称冲突的潜在问题。
    
[公共接口与内部接口](#id50)
---------------------------------------

任何向后兼容性的保证只针对于公共接口。所以，让用户可以简单清晰的区分公共接口和内部接口是很重要。

所有被文档化的接口默认都是公共的，除非是文档里明确说明了它是临时的或者内部接口，不受向后兼容性的约束。所有未文档化的接口都默认为是内部接口。

为了更好的内省，模块最好将所有公共API都使用\_\_all\_\_ 暴露出来。如果\_\_all\_\_ 是空数组的话，那模块就没有公共API。

及时是很好的使用了\_\_all\_\_，内部接口（包，模块，类，方法，属性及其他）都应该使用前置下划线以作区分。

如果接口在任何命名空间（包，模块，类）中被确定为内部的，那它就是内部接口。

如何被导入应该被重视起来。任何模块不应该间接访问被导入的内容。除非它们是被模块的API文档明确记录的，比如 os.path 或者 包的\_\_init\_\_模块，这些可以暴露子模块的方式。

[Programming Recommendations](#id51)
====================================

* 代码的编写不应该使用损害其他Python方式。（PyPy, Jython, IronPython, Cython, Psyco,等等）
    例如，不要依赖CPython中对字符串连接的高效实现功能，比如 a += b 或者  a = a + b。这个功能在CPython本身中也不是非常完善（只适用于部分类型），并且实际实现的时候都是要使用到引用计数的机制的。在库中，对性能要求高的地方，使用''.join()的方式来处理。这样能保证在不同的环境运行的时候，执行时间差异少。

*  对类似None这样的单例进行比较的时候，应该使用is或者is not,而不是使用等号运算符进行比较。

    另外，如果你想表达的意思为 x不是None 的时候，需要格外注意。比如：当要验证一个默认值是None的变量或者参数是否被设置为其他值（比如某个容器类型）的时候，被赋的值的布尔值可能是False！


*  使用 is not 比使用　not...is 更好。虽然二者在使用时是一样的，但是第一种更便于阅读。

    推荐的：
    ```python
    if foo is not None:
    ```
    不推荐的
    ```python
    if not foo is None:
    ```
*  当需要实现复杂的排序操作的时候，最好将六个基础功能全部实现（\_\_eq\_\_, \_\_ne\_\_, \_\_lt\_\_, \_\_le\_\_, \_\_gt\_\_, \_\_ge\_\_）(译者:其实用运算符表示就是 =,!=,<,<=,>,>=)。而不是只写自己需要的特定比较功能。
    
    为了最小化影响面，装饰器functools.total_ordering()提供了简单的方式来重写比较功能。
    [PEP 207](/dev/peps/pep-0207)中提出在Python中的自反性规则。例如，解释器会将 y > x 和 x < y,y >= x 和 x <=y , x == y 和 x!= y 进行交换。sort()和min()方法会使用到<，max()方法会使用到>。所以，最好实现全部留个基础功能，避免缺少基础功能造成的问题。

*  使用def来定义标识符相关方法，而不是使用lambda函数
    推荐的：
    ```python
    def f(x): return 2*x
    ```
    不推荐的
    ```python
    f = lambda x: 2*x
    ```
    
    第一种形式意味着获得的是方法'f'而不是通用的`lambda`。这在一般的追溯和字符串表示中会更加方便。将lambda语句进行赋值的方式，将lambda语句相较于显示def方法的优势磨灭了（lambda语句可以被更大的语句所嵌套。）

*  自定义异常的时候继承Exception比继承BaseException更好。BaseException是为那些不应该被用户手动捕捉的异常所继承的。

    在设计异常的时候，应该基于需要被处理的异常，而不是异常产生的位置。目的是通过编程回答“出了什么问题？”，而不是“出现了问题”。（参见[PEP 3151](/dev/peps/pep-3151)内建的异常层级结构中学到的教训。）
    
    异常的命名规则与类名的规则一致，如果异常是一个错误的话，需要在结尾加上"Error"来表示这是一个异常类。非错误类的异常比如用作非本地数据流控制或其他的非错误类异常，则不需要加上"Error"。

*  适当的使用异常关联。在Python3中,"raise X from Y"被用来进行显式的异常替换，且不会丢失原来的异常。

    当替换内部异常时（Python2:raise X ;Python3:raise X from None），需要确保原有异常的相关细节都被新异常所保留。（比如使用AttributeError替换KeyError时,要保留找不到的对象属性名，或者将所有原异常的错误信息都嵌入到新异常中。）

*  当在Python2中抛出异常时，使用 raise ValueError('message')的方式来替换旧有的 raise ValueError,'message'方式。
    
    后一种在Python3中并不支持。
    
    使用第一种参数的方式，意味着当参数过长或者包含的字符串格式的话，因为有括号的存在，所以用户不需要使用行连接符。

*  当捕捉异常的时候，尽量提及具体的异常内容，而不是使用简单的 except：子句。

    ```python    
    try:
        import platform_specific_module
    except ImportError:
        platform_specific_module = None
    ```

    不指定异常类进行捕捉的except语句：将捕捉SystemExit和KeyboardInterrupt的异常，会使通过组合键（Control-C）中断程序的方式出现问题。也可能会掩盖住其他问题。如果你想捕捉所有程序发出的异常信号，使用except Exception：（不指定捕捉异常类的except语句相当于except BaseException：）。
    
    经验之谈，只有两种情况下使用使用空'except'语句：
    
    1. 如果异常处理程序用来打印错误内容或用来记录相关日志；或者只是为了让用户知道发生了什么错误。
    2. 如果代码需要做清理的工作，让异常通过语句传递给上一层处理。try...finally很适合处理这样的案例。


*   当将异常绑定到某个异常子类的时候，使用Python2.6新增加的显示方式:
    ```python
        try:
            process_data()
        except Exception as exc:
            raise DataProcessingFailedError(str(exc))
    ```
    Python3只支持这样的语法，为了避免与旧版的逗号语法想冲突，请使用该语法。

*  当捕捉到系统错误的时候，首选使用Python3.3新增的显示异常结构，而不是使用内省的errno值。

* 此外，在所有使用到try/except语句的地方，语句所捕捉异常的区域应该是尽可能小，避免会将其他BUG遮盖住。
    推荐的：
    ```python
     try:
        value = collection[key]
    except KeyError:
        return key_not_found(key)
    else:
        return handle_value(value)
    ```
    不推荐的
    ```python
    try:
        # 覆盖范围过大!
        return handle_value(collection[key])
    except KeyError:
        # 除了collection的key异常，同样会捕捉handle_value()的入参异常。
        return key_not_found(key)
    ```

*  当资源只使用在代码中特定的某一段时，请尽量使用with语句来确保资源在被使用后及时被关闭。也可以使用try/finally语句才进行资源的使用及关闭。
    
*  当使用上下文管理器（译者：可以简单理解为就是with语句。Python2.5加入的新关键字）时它应该获取或者释放某些资源，如果没有这样的操作，使用其他单独的方法和函数来操作。
     推荐的：
    ```python
    with conn.begin_transaction():
        do\_stuff\_in_transaction(conn)
    ```
    不推荐的
    ```python
    with conn:
        do\_stuff\_in_transaction(conn)
    ```   

    
    The latter example doesn't provide any information to indicate that the \_\_enter\_\_ and \_\_exit\_\_ methods are doing something other than closing the connection after a transaction. Being explicit is important in this case.
    
*   Be consistent in return statements. Either all return statements in a function should return an expression, or none of them should. If any return statement returns an expression, any return statements where no value is returned should explicitly state this as return None, and an explicit return statement should be present at the end of the function (if reachable).
    
    Yes:
    
    def foo(x):
        if x >= 0:
            return math.sqrt(x)
        else:
            return None
    
    def bar(x):
        if x < 0:
            return None
        return math.sqrt(x)
    
    No:
    
    def foo(x):
        if x >= 0:
            return math.sqrt(x)
    
    def bar(x):
        if x < 0:
            return
        return math.sqrt(x)
    
*   Use string methods instead of the string module.
    
    String methods are always much faster and share the same API with unicode strings. Override this rule if backwards compatibility with Pythons older than 2.0 is required.
    
*   Use ''.startswith() and ''.endswith() instead of string slicing to check for prefixes or suffixes.
    
    startswith() and endswith() are cleaner and less error prone:
    
    Yes: if foo.startswith('bar'):
    No:  if foo\[:3\] == 'bar':
    
*   Object type comparisons should always use isinstance() instead of comparing types directly.
    
    Yes: if isinstance(obj, int):
    
    No:  if type(obj) is type(1):
    
    When checking if an object is a string, keep in mind that it might be a unicode string too! In Python 2, str and unicode have a common base class, basestring, so you can do:
    
    if isinstance(obj, basestring):
    
    Note that in Python 3, unicode and basestring no longer exist (there is only str) and a bytes object is no longer a kind of string (it is a sequence of integers instead).
    
*   For sequences, (strings, lists, tuples), use the fact that empty sequences are false.
    
    Yes: if not seq:
         if seq:
    
    No:  if len(seq):
         if not len(seq):
    
*   Don't write string literals that rely on significant trailing whitespace. Such trailing whitespace is visually indistinguishable and some editors (or more recently, reindent.py) will trim them.
    
*   Don't compare boolean values to True or False using ==.
    
    Yes:   if greeting:
    No:    if greeting == True:
    Worse: if greeting is True:
    

[函数注释](#函数注释)
-----------------------------

With the acceptance of [PEP 484](/dev/peps/pep-0484), the style rules for function annotations are changing.

*   In order to be forward compatible, function annotations in Python 3 code should preferably use [PEP 484](/dev/peps/pep-0484) syntax. (There are some formatting recommendations for annotations in the previous section.)
    
*   The experimentation with annotation styles that was recommended previously in this PEP is no longer encouraged.
    
*   However, outside the stdlib, experiments within the rules of [PEP 484](/dev/peps/pep-0484) are now encouraged. For example, marking up a large third party library or application with [PEP 484](/dev/peps/pep-0484) style type annotations, reviewing how easy it was to add those annotations, and observing whether their presence increases code understandability.
    
*   The Python standard library should be conservative in adopting such annotations, but their use is allowed for new code and for big refactorings.
    
*   For code that wants to make a different use of function annotations it is recommended to put a comment of the form:
    
    \# type: ignore
    
    near the top of the file; this tells type checker to ignore all annotations. (More fine-grained ways of disabling complaints from type checkers can be found in [PEP 484](/dev/peps/pep-0484).)
    
*   Like linters, type checkers are optional, separate tools. Python interpreters by default should not issue any messages due to type checking and should not alter their behavior based on annotations.
    
*   Users who don't want to use type checkers are free to ignore them. However, it is expected that users of third party library packages may want to run type checkers over those packages. For this purpose [PEP 484](/dev/peps/pep-0484) recommends the use of stub files: .pyi files that are read by the type checker in preference of the corresponding .py files. Stub files can be distributed with a library, or separately (with the library author's permission) through the typeshed repo [\[5\]](#id12).
    
*   For code that needs to be backwards compatible, type annotations can be added in the form of comments. See the relevant section of [PEP 484](/dev/peps/pep-0484) [\[6\]](#id13).
    

[Variable Annotations](#id53)
-----------------------------

[PEP 526](/dev/peps/pep-0526) introduced variable annotations. The style recommendations for them are similar to those on function annotations described above:

*   Annotations for module level variables, class and instance variables, and local variables should have a single space after the colon.
    
*   There should be no space before the colon.
    
*   If an assignment has a right hand side, then the equality sign should have exactly one space on both sides.
    
*   Yes:
    
    code: int
    
    class Point:
        coords: Tuple\[int, int\]
        label: str = '<unknown>'
    
*   No:
    
    code:int  # No space after colon
    code : int  # Space before colon
    
    class Test:
        result: int=0  # No spaces around equality sign
    
*   Although the [PEP 526](/dev/peps/pep-0526) is accepted for Python 3.6, the variable annotation syntax is the preferred syntax for stub files on all versions of Python (see [PEP 484](/dev/peps/pep-0484) for details).
    

Footnotes

[\[7\]](#id3)

_Hanging indentation_ is a type-setting style where all the lines in a paragraph are indented except the first line. In the context of Python, the term is used to describe a style where the opening parenthesis of a parenthesized statement is the last non-whitespace character of the line, with subsequent lines being indented until the closing parenthesis.

[References](#id54)
===================

[\[1\]](#id1)

[PEP 7](/dev/peps/pep-0007), Style Guide for C Code, van Rossum

[\[2\]](#id2)

Barry's GNU Mailman style guide [http://barry.warsaw.us/software/STYLEGUIDE.txt](http://barry.warsaw.us/software/STYLEGUIDE.txt)

[\[3\]](#id4)

Donald Knuth's _The TeXBook_, pages 195 and 196.

[\[4\]](#id5)

[http://www.wikipedia.com/wiki/CamelCase](http://www.wikipedia.com/wiki/CamelCase)

[\[5\]](#id6)

Typeshed repo [https://github.com/python/typeshed](https://github.com/python/typeshed)

[\[6\]](#id7)

Suggested syntax for Python 2.7 and straddling code [https://www.python.org/dev/peps/pep-0484/#suggested-syntax-for-python-2-7-and-straddling-code](https://www.python.org/dev/peps/pep-0484/#suggested-syntax-for-python-2-7-and-straddling-code)

[Copyright](#id55)
==================

This document has been placed in the public domain.

Source: [https://github.com/python/peps/blob/master/pep-0008.txt](https://github.com/python/peps/blob/master/pep-0008.txt)
