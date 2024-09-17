---
tags:
  - learn/program/python
dg-permalink: python/for
---


如果你有些代码，是需要重复执行的，那么套用循环是最好的选择。

for循环：对序列中的每个变量都执行相同的操作，写作：

$for\quad变量\quad in\quad序列:$

如何去理解记忆for循环？我们将其英文的意思记住就好

- **for**：对于…
- **in**：在…里面

将for和in的中文带入上方的格式进行直译可以得到：对每一个在序列里面的变量-最后再加上冒号，整体意思为：对每一个在序列里面的变量，将执行以下操作……

**变量代指什么，取决于 in 后面的序列为什么**

遍历整个列表

需要对列表中的每个元素都执行相同的操作时，可使用for循环，对列表中的每个元素，都将执行循环指定的步骤，而不管列表包含多少个元素

```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians: # 使用了 for 关键字定义一个循环，让 Python 从列表 magicians 中依次取出一个个名字与变量 magician 相关联
    print(f"{magician.title()}, that was a great trick!") # 打出四个空格作为缩进（indentation），打印前面赋给变量 magician 的名字
    print(f"I can't wait to see your next trick, {magician.title()}.")
>>>
Alice, that was a great trick!
I can't wait to see your next trick, Alice.
David, that was a great trick!
I can't wait to see your next trick, David.
Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.
```

仔细看看这段循环代码，magician 是一个临时变量，临时变量的名称可以任意指定：使用单数和复数形式的名称，可帮助你判断代码段处理的是单个列表元素还是整个列表。

可以给列表中每个值相关联的临时变量指定任意名称，有助于明白for循环中将对每个元素执行的操作。

只要保持缩进，我们可以在 for 循环中放入多行语句。

在for循环结束后通常需要提供总结性输出或接着执行程序必须完成的其他任务。 

```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
		print(f"{magician.title()}, that was a great trick!")
		print(f"I can't wait to see more, {magician.title()}.\n")
print("Thank you, everyone. That was a great magic show!")
```

### for循环中的好基友len与range

**函数：`len()`**

返回对象的长度（元素个数）。作用的对象可以是序列（如 string、tuple、list、range 或 DataFrame 等）或集合（如 dictionary、set等）。

Python计算列表元素数时从1开始，因此确定列表长度时，你应该不会遇到差一错误。

```python
len([1, 2, 3, 4, 5])
```

**函数：`range([start,] end [,step])`**

生成可迭代的数值序列。

**参数start：**起始数字，默认为0

**参数end：**结束数字

**参数step：**步长，默认为1

第一个参数start（即方法/函数需要的信息，左闭右开）是可选的。range(6)将会打印数 0 ~ 5

要打印数1～5，需要使用`range(1,6)`，实际元素只有1,2,3,4,5 。不包含数字6，这是编程语言中常见的差一行为的结果，输出在指定的第二个值处停止了。我们可以用for循环逐个打印其中的元素来验证一下：

```python
for i in range(1,6):
		print(i)
>>>
1
2
3
4
5
```

例如，你在浏览B站的每周必看，但是觉得一周一周的去点击，非常的麻烦，那么此时你可以用到循环，帮助你去自动点击

```python
# 加入从第 1期 点到 第180期 开始
for week in range(1,181):
print(f'正在浏览第{week}期的每周必看...')
```

用`list()`函数将`range()`的结果创建为数字列表

```python
# 打印1~10的偶数
even_numbers = list(range(2, 11, 2))
print(even_numbers)
>>>
[2, 4, 6, 8, 10]

# 如何创建一个包含1~10整数平方的列表？
squares = []
for value in range(1,11):
		squares.append(value**2)
print(squares)
>>>
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

**为什么说len与range是好基友呢？**

实际运用中，我们经常会需要用for循环遍历一些我们不知道具体长度的序列。

```python
player =  ['537','23017',1,25,'16777215','10bfeb59','44','10bfeb59']
# 用for循环来输出demo里面的内容
for row in demo:
		print(row)
# 用range和len的组合输出demo里面的内容
for i in range(len(demo)):
		print(row[i])
```

遍历字典

一个Python字典可能只包含几个键值对，也可能包含数百万个键值对。鉴于字典可能包含大量数据，Python支持对字典进行遍历。字典可用于以各种方式存储信息，因此有多种遍历方式：既可遍历字典的所有键值对，也可只遍历键或值。

遍历所有的键值对

在探索各种遍历方法前，先来看一个新字典，它用于存储有关网站用户的信息。这个字典存储一个用户的用户名、名和姓，如果要获悉该用户字典中的所有信息，可使用for循环来遍历这个字典

```python
user_0 = {
'username': 'efermi',
'first': 'enrico',
'last': 'fermi', }
# 要编写遍历字典的for循环，可声明两个变量，分别用于存储键值对中的键和值。
for key, value in user_0.items():
	print(f"\nKey: {key}") # 调用print()中的'\n'，确保在输出每个键值对前插入一个空行。
	print(f"Value: {value}")
>>>

Key: username
Value: efermi

Key: first
Value: enrico

Key: last
Value: fermi
```

for语句的第二部分包含字典名和方法`items()`，这个方法返回一个键值对列表。

接下来，for循环依次将每个键值对赋给指定的两个变量。在这个示例中，使用这两个变量来打印每个键和与它关联的值。第一个函数调用print()中的"\n"确保在输出每个键值对前插入一个空行。

在6.2.6节的示例favorite_languages.py中，字典存储的是不同的人的同一种信息。对于类似这样的字典，遍历所有的键值对很合适。如果遍历字典favorite_languages，将得到其中每个人的姓名和他们喜欢的编程语言。由于该字典中的键都是人名，值都是语言，因此在循环中使用变量name和language，而不是key和value。这让人更容易明白循环的作用：

```python
favorite_languages = {
'jen': 'python',
'sarah': 'c',
'edward': 'rust',
'phil': 'python',
}
for name, language in favorite_languages.items():
print(f"{name.title()}'s favorite language is {language.title()}.")
>>>
Jen's favorite language is Python.
Sarah's favorite language is C.
Edward's favorite language is Rust.
Phil's favorite language is Python.
```

这些代码让Python遍历字典中的每个键值对，并将键赋给变量name，将值赋给变量language。这些描述性名称让人能够非常轻松地明白函数调用print()是做什么的。

即便字典存储了上千乃至上百万人的调查结果，这种循环也管用。

遍历字典中的所有键

在不需要使用字典中的值时，`keys()`方法很有用。

下面用for循环来遍历字典`favorite_languages`中的所有键，并依次将它们赋给变量name，输出打印每个被调查者的名字：

```python
favorite_languages = { 'jen': 'python', 'sarah': 'c', 'edward': 'rust', 'phil': 'python',}
for name in favorite_languages.keys():
		print(name.title())
>>>
Jen
Sarah
Edward
Phil
```

在遍历字典时，会默认遍历所有的键。因此，如果将上述代码中的`for name in favorite_languages.keys():`替换为`for name in favorite_languages:`输出将不变。如果显式地使用keys()方法能让代码更容易理解，就可以选择这样做，但如果你愿意，也可以省略它。

在这种循环中，可使用当前的键来访问与之关联的值。下面来打印两条消息，指出两个朋友喜欢的编程语言。我们像前面一样遍历字典中的名字，但在名字为指定朋友的名字时，打印一条消息，指出其喜欢的语言：

```python
'''首先创建一个列表，其中包含要收到打印消息的朋友。
在循环中，打印每个人的名字，并检查当前的名字是否在列表friends中。
如果是，就打印一句特殊的问候语，其中包含这个朋友喜欢的语言。
为获悉这个朋友喜欢的语言，这里使用了字典名，并将变量name的当前值作为键。'''
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'rust',
    'phil': 'python',
    }

friends = ['phil', 'sarah']
for name in favorite_languages.keys():
		print(f"Hi {name.title()}.")
		if name in friends:
				language = favorite_languages[name].title()
				print(f"\t{name.title()}, I see you love {language}!")
# 每个⼈的名字都会被打印出来，但只对朋友打印特殊消息

'''输出
Hi Jen.
Hi Sarah.
		Sarah, I see you love C!
Hi Edward.
Hi Phil.
		Phil, I see you love Python!
'''

# 使用keys()确定某个人是否接受了调查
if 'erin' not in favorite_languages.keys():
		print("Erin, please take our poll!")
```

keys()方法并非只能用于遍历：实际上，它会返回一个列表，其中包含字典中的所有键。因此if语句只核实‘erin’是否在这个列表中。因为她并不在这个列表中，所以打印一条消息，邀请她参加调查。

按特定的顺序遍历字典中的所有键

遍历字典时将按插入元素的顺序返回其中的元素，但是在一些情况下，你可能要按与此不同的顺序遍历字典。

要以特定的顺序返回元素，一种办法是在for循环中对返回的键进行排序。为此，可使用sorted()函数来获得按特定顺序排列的键列表的副本：

```python
favorite_languages = {
'jen': 'python',
'sarah': 'c',
'edward': 'rust', 'phil': 'python', }
for name in sorted(favorite_languages.keys()):
		print(f"{name.title()}, thank you for taking the poll.")
>>>
Edward, thank you for taking the poll.
Jen, thank you for taking the poll.
Phil, thank you for taking the poll.
Sarah, thank you for taking the poll.
```

这条for语句类似于其他for语句，但对方法`dictionary.keys()`的结果调用了sorted()函数。这让Python获取字典中的所有键，并在遍历前对这个列表进行排序。输出表明，按字母顺序显示了所有被调查者的名字。

遍历字典中的所有值

如果你感兴趣的是字典包含的值，可使用values()方法。它会返回一个值列表，不包含任何键。如果想获得一个只包含被调查者选择的各种语言，而不包含被调查者名字的列表，可以这样做：

```python
favorite_languages = {
'jen': 'python',
'sarah': 'c',
'edward': 'rust',
'phil': 'python',
}
print("The following languages have been mentioned:")
for language in favorite_languages.values():
		print(language.title())
'''>>>
The following languages have been mentioned:
Python
C
Rust
Python
'''
print("The following languages have been mentioned:")
for language in set(favorite_languages.values()):
		print(language.title())
>>>
The following languages have been mentioned:
Python
C
Rust
```

这条for语句提取字典中的每个值，并将它们依次赋给变量language。通过打印这些值，就获得了一个包含被调查者选择的各种语言的列表：

这种做法提取字典中所有的值，而没有考虑值是否有重复。当涉及的值很少时，这也许不是问题，但如果被调查者很多，最终的列表可能包含大量的重复项。为剔除重复项，可使用集合(set)。集合中的每个元素都必须是独一无二的：

通过将包含重复元素的列表传入set(),可让Python找出列表中独一无二的元素，并使用这些元素来创建一个集合。这里使用set()来提取favorite_languages.values()中不同的语言。

结果是一个没有重复元素的列表，其中列出了被调查者提及的所有语言。

随着学习的深入，你会经常发现Python内置的功能可帮助你以希望的方式处理数据。

注意：可以使用一对花括号直接创建集合，并在其中用逗号分隔元素：

```python
>>> languages = {'python', 'rust', 'python', 'c'}
>>> languages
{'rust', 'python', 'c'}
```

集合和字典很容易混淆，因为它们都是用一对花括号定义的。当花括号内没有键值对时，定义的很可能是集合。不同于列表和字典，集合不会以特定的顺序存储元素。

## 避免缩进错误

Python要求你使用缩进让代码结构清晰，整洁易读。

对于我们撰写文档来说，是每句话前面加若干个空格。对于其他编程语言（例如C）来说，每行代码前面加若干个空格。但对于python来说有非常重要的含义：在使用循环、函数或者类等等的时候，通过使用缩进，才能让python知道哪些代码将作为它们内部运行的一部分。

开始编写必须正确缩进的代码时，需要注意一些常见的缩进错误：

1. 忘记缩进
2. 不必要的缩进
3. 遗漏了冒号
4. 忘记缩进额外的代码行
5. 循环后不必要的缩进

后两种大多数情况语法上不会报错，但会导致现实逻辑的错误。

没有正确的缩进（缩进错误）
忘记缩进额外的代码行（逻辑错误）
循环后不必要的缩进（逻辑错误）
循环的末尾漏掉了冒号（语法错误）