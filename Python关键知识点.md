# 序论-Python的条条框框

## 语言类型

    语言是沟通的工具，人有人言，兽有兽语，如果要与计算机进行交流，就要有计算机语言，这就是编程语言存在的原因。计算机发展到现在，编程语言也是五花八门，Python就是其中的一种，一般对于编程语言，会有几个划分的维度：

- 编译型还是解释型：Python是解释型；
- 动态还是静态：Python是动态语言；动态语言是指运行时可以改变其结构，可以对变量或函数进行修改，定义的变量不需要指定数据类型，只有第一次给变量赋值时，根据赋值的类型在内部指定该变量的类型；
- 强定义还是弱定义：Python是强定义型。强定义型是会严格区分内部的变量类型，一旦指定了类型，就必须经过转换才能存取为其他类型，类似的语言有C、Java；弱定义类型是指不严格区分内部的变量类型，一般是只要大小放得下即可转化。类似的语言有VBScript，JavaScript

## 基础规则

    使用Python编写的源代码，从粗到细可以分为模块、代码块、代码三部分：

- 模块：.py文件；
- 代码块：代码中“：”后的部分即代码块，函数、类、if语句块、循环语句块都是代码块；
- 代码：可以认为是一行或者多行代码行；

python中还有一个包的概念，包更多是从代码文件组织的角度的一个概念，如果一个文件夹中有“\_\_init\_\_.py”文件，那么这个文件夹就是一个包，一个包可以包含多个模块，也可以继续包含包。

### 模块的详细介绍

    Python模块包含了Python对象定义和Python语句，使用模块可以跟清晰的组织代码

#### 模块的作用及分类

    模块的主要作用是被导入到其他模块中。将其他模块导入到当前模块中可以实现对当前模块的增强，模块的使用避免了庞大代码量中变量名和函数名冲突的问题，将代码模块化，也提高了代码的可维护性与重用性。根据模块来源不同，python中的模块可以分为内置模块、第三方模块、自定义模块。

#### 模块的搜索路径

    当导入一个模块时，Python解释器会按照如下顺序进行查找：

1. 查找内置模块；
2. 读取sys.path，按照sys.path的内容进行查找。

sys.path的内容主要包括如下几部分：

1. 当前程序所在的目录；
2. 标准库的安装目录（lib\\site-packages）;
3. 操作系统的环境变量pythonpath所包含的目录

只要一搜到就会停止，如果把所有路径都遍历了都没查找到，则会报import error错误。

#### 模块的属性

    Python中万物皆对象，模块当然也例外不了，模块也是对象，是对象就会有属性。一些常见的属性：

- \_\_name\_\_:名字，当模块独立运行时是'\_\_main\_\_',当被其他模块导入时就是模块本身的名字；
- \_\_file\_\_:文件名，包括路径，类似于‘e:/workroom/python_sample/hello.py’
- \_\_doc\_\_:模块的注释说明，一般来说是介绍模块的功能、用途等；

#### 模块的四种导入方式

1. import _xxx_ as _yyy_ ：导入名为xxx的模块，导入后重命名为yyy；

2. from xxx import yyy ：从模块xxx中导入函数、类、变量yyy或者从xxx包中导入yyy模块；

3. from xxx import * :导入xxx中的所有名字（以下划线开头的名字除外）；

4. \_\_import\_\_ 方法：因为模块是文件，文件的命名规范是由操作系统来定的，允许出现空格或者以数字开头，但这些规则与Python语法冲突，解决方法就是使用\_\_import\_\_.例如：

   ```python
   yuyinutils = __import__("9-24 yuyinutils")
   ```

   **特别说明：**

   > “.”表示当前目录； ".."代表上级目录，
   >
   > ```python
   > from .ie.webdriver import WebDriver as Ie
   > ```
   >
   > 上面的代码表示从当前目录下的ie文件夹下的webdriver模块中导入WebDriver类，并重命名为Ie
