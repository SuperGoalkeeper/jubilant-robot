# Python Reference

# 词法分析

## 行结构

### 逻辑行

python程序是由一系列逻辑行组成，不同的逻辑行之间通过NEWLINE符号分割，除非语法允许，要不语句是不能跨多个物理行的，后续如非特别说明，提到行时都指逻辑行

### 物理行

对于python来说，不同的物理行之间通过“\n”符号分割；

### 注释

#开始，到物理行的结束，#并不是注释的一部分，python解释器在解析时会跳过注释

### 编码声明

如果脚本的第一行或者第二行是注释且符合正则表达式coding[=:]\s * ([-\w.]+)，那么这个注释就会被当做脚本的编码声明，并且如果位置是在第二行的话，第一行也必须是注释。如下都是合法的编码声明格式

```python
#coding= utf8
```

```python
## - * - coding: utf8 - * -
```

如果没有编码声明，那么就使用默认的utf8编码。编码名称必须是python可识别的。

### 显式行连接

在python中，反斜线“\”是转义字符，我们可以使用它把多行物理行连接为一个逻辑行（注意反斜线并不会作为内容的一部分）

```python
if 1900 < year < 2100 and 1 <= month <= 12 \
and 1 <= day <= 31 and 0 <= hour < 24 \
and 0 <= minute < 60 and 0 <= second < 60: # Looks like a valid date
return 1
```

需要注意的是反斜线后不能有注释

### 隐式行连接

1. 在()、[]、{}中的表达式，可以跨越多个物理行，并且每个物理行后都可以跟注释，缩进也被忽略，还能包含空行

```python
month_names = ['Januari', 'Februari', 'Maart', # These are the
'April', 'Mei', 'Juni', # Dutch names
'Juli', 'Augustus', 'September', # for the months
'Oktober', 'November', 'December'] # of the year
```

1. 三引号对也可以连接多个物理行，但是其中不能有注释

## 标识符与关键字

标识符由字母、数字或者下划线组成，但不能以数字开头，长度不限制，大小写敏感。对于Python3之前，字母只能是范围（U+0001..U+007F）的ASCII字符（大小写字母），Python3之后可以是非ASCII字符（PEP3131定义）

### 关键字

关键字是python保留的标识符，总共有33个

```python
False	class 	finally is 	return 	None 		continue 	for 	lambda 	try
True 	def 	from 	nonlocal 	while 	and 	del 	global 	not 	with
as 		elif 	if 		or 		yield		assert 	else 	import 	pass	break 	
except 		in 	raise

```

在使用时拼写必须与上面一模一样

### 保留标识符

除了关键字外，有一些特殊命名的标识符，也具备特别含义

- _*  ：以单下划线开始的标识符不会被import *语句导入，另外在交互模式下，单下划线表示最近一次执行结果；
- \_\_*\_\_ ：系统定义的名字，解释器或者内置库定义、使用，代表有特殊含义；
- __* ：如果类的属性名称中以双下划线开始，那么解释器在解析时会进行重命名，这一定程度上实现了“私有”

## 操作符（Operators）

```python
+ - * ** / // % @ << >> & | ^ ~ < > <= >= == !=
```

## 分隔符（Delimiters）

```python
( ) [ ] { } , : . ; @ = -> += -= *= /= //= %= @= &= |= ^= >>= <<= **=
```

# 数据模型（Data Model）

## 对象三要素：id，type，value

Python中万物皆对象，对象是Python中对数据的抽象，所有Python中的数据都通过对象或者对象之间的关系表示。所有对象都有三部分组成：

- id ：可以简单认为是对象的内存地址，对象一旦创建，id就不会再改变，可以通过id()来查看；
- type ：对象的类型决定了对象的可能值得范围，并且决定了可以支持的操作，可以通过type()查看；
- value ：对象的值，如果一个对象的值可以被改变，就成为可变对象（mutable），如果对象的值不能被改变，就成为是不可变对象（immutable），一个对象是否可变是由其type决定的，数字、字符串、元组都是不可变对象，列表、字典是常见的可变对象。

**容器：**一些对象包含到其他对象的引用，称这类对象为容器（containers），元组、列表、字典都是常见的容器类型

## Python中的内置数据类型

### 可调用类型（Callable types）

可调用类型是能够被调用的

- 用户定义函数
- 实例方法
- 生成器函数
- 协同函数（Coroutine function）
- 异步生成器函数
- 内置函数
- 内置方法
- 类
- 类实例

## 模块（Module）

模块是Python代码组织的基本单元，通过import语句或者调用importlib.import_module()或者内置的\_\_import\_\_()函数创建，模块对象有一个字典类型的命名空间(namespace)，所有的属性访问都会被转成字典查找,例如m.x 就等效于m.\_\_dict\_\_['x']；同样属性赋值也是转换为对该字典的操作：m.x = 1 == m.\_\_dict\_\_['x'] = 1。模块有一些预定义的属性，常见的有：

- \_\_name\_\_：模块名字；
- \_\_file\_\_：模块文件所在的pathname；
- \_\_dict\_\_：模块的命名空间

## 自定义类（Custom class）

通过class关键字用户可以自定义类，与模块类似，类同样有一个命名空间，它也是通过字典来实现的，对类的属性的访问都会被转换成类的字典的查找：如c.x  等效于 c.\_\_dict\_\_['x']。与模块不同的是，类还可以有继承，因此当属性在字典中查找不到时，它会继续在该类的基类中查找。

## I/O object(file object)

## 特殊方法名

一些特别的方法名称能实现一些比较特别的功能，例如如果一个类定义了方法\_\_getitem\_\_()，x是该类的一个实例，那么x[i] == type(x).\_\_getitem\_\_(x,i)（就相当于该了具备了索引的功能）。如果对类进行不支持的操作，会抛出错误（典型的是TypeError或者AttributeError）。

如果把某个特殊方法设置为None，就表示该类不支持某类操作。如把\_\_iter\_\_()设置为None，就表示该类不可迭代，这个时候如果把该类的实例传给iter()，就会抛出TypeError异常；

## 描述符

**描述符的定义**

如果一个类或者其父类实现了描述符协议，那么这个类就是描述符类。所谓的描述符协议是由如下三个方法组成：

- object.\_\_get\_\_(self,instance,owner):获取owner class的类属性，或者获取owner class的实例属性。owner 是指owner class；
- object.\_\_set\_\_(self,instance,value)：设置实例属性的值为value；
- object.\_\_delete\_\_(self,instance)：删除实例属性；

如果一个对象具有上面的任意一个方法，就被称为是描述符对象，简称描述符（descriptor）

**描述符的调用**

描述符是指对象的属性具有了绑定行为（In general, a descriptor is an object attribute with "binding behavior",one whose attribute access has been overridden by methods in the descriptor protocol:\\_\_get\_\_(),\_\_set\_\_(),\_\_delete\_\_(). If any of those methods are defined for an object，it is said to be a descriptor），也就是说该对象的属性访问被描述符协议中的方法所重载。

我们先看下缺省的属性访问方式：缺省方式是对对象字典中以该属性为键值的的相关数据的get、set、delete操作，例如a.x ：

1. 查找a.\_\_dict\_\_['x'],如果找到则返回，否则继续；
2. 查找type(a).\_\_dict\_\_['x']，如果找到则返回，否则继续；
3. 在type(a)的父类中查找（但不会在元类中搜索）；

如果一个对象是一个描述符对象（定义了任意一个描述符方法），那么Python就会对缺省查找方式进行修改，会调用描述符方法，具体发生的顺序（描述符方法的调用时机）视描述符的不同而又有差异，同样以a.x为例：

1. Direct Call：这是最简单，也是最少见的一种类型，a本身就定义了\_\_get\_\_()方法，那么a.x就相当于x.\_\_get\_\_（a）；
2. 实例绑定（Instance Binding）：就是说a是一个类的实例，a.x会被转变成type(a).\_\_dict\_\_['x'].\_\_get\_\_(a,type(a))；
3. 类绑定（Class Binding）：如果a是一个类（我们用大写A表示），A.x就会被转变成A.\_\_dict\_\_['x'].\_\_get\_\_(None,A);
4. Super Binding:如果a是super的实例，那么super(B,obj).m()会通过obj.\_\_class\_\_.\_\_mro\_\_找到B的直接父类A，调用A.\_\_dict\_\_['m'].\_\_get\_\_(obj,obj.\_\_class\_\_)

如果一个描述符只定义了\_\_get\_\_()，那么就是一个非数据描述符（non-data descriptor），否则只要定义了\_\_set\_\_()或者\_\_delete\_\_()两个方法中的任意一个（或者全部）就是数据描述符（data descriptor）。对于实例绑定来说，数据描述符与非数据描述符方法的调用时机会有差异：

**数据描述符会覆盖实例字典，非数据描述符会被实例字典覆盖**（Data descriptor always override definition in an instance dictionary. In contrast, non-data descriptors can be overridden by instance)。Python方法staticmethod()、classmethod()都是非数据描述符，因此实例都可以重新定义覆盖它们，这使得同一个类的不同实例可以实现不同搞得行为；property()函数是数据描述符，因此实例无法覆盖property的行为

## 上下文管理器（Context Manager）

上下文管理器是能够在与with语句配合运行时建立上下文环境的对象，它为with语句块定义了进入（entry into）与离开（exit from）所需要的上下文环境。context manager一般来说是与with语句配合在一起使用，但是也可以直接调用其对应方法。一个上下文管理器需要定义如下方法：

- object.\_\_enter\_\_(self)：进入与该对象相关的运行时上下文环境。在与with语句配合使用时，可以通过as 语句把该方法的返回值赋值给as 参数；
- object.\_\_exit\_\_(self，exc_type, exc_value, traceback)：退出与该对象相关的上下文环境，参数可以描述该上下文环境中触发的异常，如果没有异常，那么这三个参数值都会是None；

