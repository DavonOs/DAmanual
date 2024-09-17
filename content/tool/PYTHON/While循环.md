---
tags:
  - learn/program/python
dg-permalink: python/while
---

# While循环

for 循环⽤于针对集合中的每个元素执⾏⼀个代码块，⽽ while 循环则不断地运⾏，直到指定的条件不再满⾜为⽌。

7.2.1 使⽤ while 循环
可以使⽤ while 循环来数数。例如，下⾯的 while 循环从 1 数到 5：

```python
current_number = 1
while current_number <= 5:
		print(current_number)
		current_number += 1
>>>
1
2
3
4
5

```

在第⼀⾏，将 1 赋给变量 current_number，从⽽指定从 1 开始数。接下来的 while 循环被设置成：只要current_number ⼩于或等于 5，就接着运⾏这个循环。循环中的代码打印 current_number 的值，再使⽤代码 current_number += 1（代码 current_number = current_number + 1 的简写）将其值加 1。 只要满⾜条件 current_number <= 5，Python 就接着运⾏这个循环。因
为 1 ⼩于 5，所以 Python 打印 1 并将 current_number 加 1，使其为 2； 因为 2 ⼩于 5，所以 Python 打印 2 并将 current_number 加 1，使其为3；依此类推。⼀旦current_number ⼤于 5，循环就将停⽌，整个程序也将结束。

你每天使⽤的程序⼤多包含 while 循环。例如，游戏使⽤ while 循环，确保在玩家想玩时不断运⾏，并在玩家想退出时结束运⾏。如果程序在⽤户没有让它停⽌时结束运⾏，或者在⽤户要退出时继续运⾏，那就太没意思了。因此，while 循环很有⽤。

7.2.2 让⽤户选择何时退出

可以使⽤ while 循环让程序在⽤户愿意时不断地运⾏，如下⾯的程序所⽰。我们在其中定义了⼀个退出值，只要⽤户输⼊的不是这个值，程序就将⼀直运⾏：

```python
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "

message = ""
while message != 'quit':
		message = input(prompt)
		print(message)
>>>
Tell me something, and I will repeat it back to you: Enter 'quit' to end the program. Hello everyone!
Hello everyone!
Tell me something, and I will repeat it back to you: Enter 'quit' to end the program. Hello again.
Hello again.
Tell me something, and I will repeat it back to you: Enter 'quit' to end the program. quit
quit
```

⾸先，定义⼀条提⽰消息，告诉⽤户有两个选择：要么输⼊⼀条消息，要么输⼊退出值（这⾥为 'quit'）。然后，创建变量 message，⽤于记录⽤户输⼊的值。我们将变量 message 的初始值设置为空字符串 ""，让 Python 在⾸次执⾏ while 代码⾏时有可供检查的东⻄。Python 在⾸次执⾏ while 语句时，需要将 message 的值与 'quit' 进⾏⽐较，但此时⽤户还没有输⼊。如果没有可供⽐较的东⻄，Python 将⽆法继续运⾏程序。为解决这个问题，必须给变量 message 指定初始值。虽然这个初始值只是⼀个空字符串，但符合要求，能够让 Python 执⾏ while 循环所需的⽐较。只要 message 的值不是 'quit'，这个循环就会不断运⾏。 当⾸次遇到这个循环时，message 是⼀个空字符串，因此 Python 进⼊这个循环。在执⾏到代码⾏ message = input(prompt) 时，Python 显⽰提⽰消息，并等待⽤户输⼊。不管⽤户输⼊是什么，都会被赋给变量message 并打印出来。接下来，Python 重新检查 while 语句中的条件。 只要⽤户输⼊的不是单词 'quit'，Python 就会再次显⽰提⽰消息并等待 ⽤户输⼊。等到⽤户终于输⼊'quit'后，Python 停⽌执⾏ while 循环，整个程序也到此结束。

这个程序很好，唯⼀美中不⾜的是，它将单词'quit'也作为⼀条消息打印了出来。为了修复这种问题，只需要使⽤⼀个简单的 if 测试：

```python
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "
message = ""
while message != 'quit':
		message = input(prompt)

		if message != 'quit':
				print(message)
>>>
Tell me something, and I will repeat it back to you: Enter 'quit' to end the program. Hello everyone!
Hello everyone!
Tell me something, and I will repeat it back to you: Enter 'quit' to end the program. Hello again.
Hello again.
Tell me something, and I will repeat it back to you: Enter 'quit' to end the program. quit
```

现在，程序在显⽰消息前将做简单的检查，仅在消息不是退出值时才打印它。

7.2.3 使⽤标志

在上⼀个⽰例中，我们让程序在满⾜指定条件时执⾏特定的任务。但在更复杂的程序中，有很多不同的事件会导致程序停⽌运⾏。在这种情况下，该怎么办呢？

例如，有多种事件可能导致游戏结束，如玩家失去所有⻜船、时间已⽤完，或者要保护的城市被摧毁。当导致程序结束的事件有很多时，如果在⼀条 while 语句中检查所有这些条件，将既复杂⼜困难。 在要求满⾜很多条件才继续运⾏的程序中，可定义⼀个变量，⽤于判断整个程序是否处于活动状态。这个变量称为标志（flag），充当程序的交通信号灯。可以让程序在标志为 True 时继续运⾏，并在任何事件导致标志的值为 False 时让程序停⽌运⾏。这样，在 while 语句中就只需检查⼀个条件：标志的当前值是否为 True。然后将所有测试（是否发⽣了应将标志设置为 False 的事件）都放在其他地⽅，从⽽让程序更整洁。 

下⾯在 7.2.2 节的程序 parrot.py 中添加⼀个标志。我们把这个标志命名为 active（可以给它指定任何名称），⽤于判断程序是否应继续运⾏：

```python
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "

active = True
while active:
		message = input(prompt)

		if message == 'quit':
				active = False
		else:
				print(message)
```

将变量 active 设置为 True，让程序最初处于活动状态。这样做简化了 while 语句，因为不需要在其中做任何⽐较——相关的逻辑由程序的其他部分处理。只要变量 active 为 True，循环就将⼀直运⾏。 在 while 循环中，在⽤户输⼊后使⽤⼀条 if 语句检查变量 message 的值。如果⽤户输⼊的是 'quit'，就将变量 active 设置为 False，这将导致 while 循环不再继续执⾏。如果⽤户输⼊的不是 'quit'，就将输⼊作为⼀条消息打印出来。

这个程序的输出与上⼀个⽰例相同。上⼀个⽰例将条件测试直接放在了while 语句中，⽽这个程序则使⽤⼀个标志来指出程序是否处于活动状态。这样，添加测试（如 elif 语句）以检查是否发⽣了其他导致 active 变为 False 的事件，就会很容易。在复杂的程序（⽐如有很多事件会导致程序停⽌运⾏的游戏）中，标志很有⽤：在任意⼀个事件导致活动标志变成 False 时，主游戏循环将退出。此时可显⽰⼀条游戏结束的消息，并让⽤户选择是否要重玩。

7.2.4 使⽤ break 退出循环

如果不管条件测试的结果如何，想⽴即退出 while 循环，不再运⾏循环中余下的代码，可使⽤ break 语句。break 语句⽤于控制程序流程，可⽤来控制哪些代码⾏将执⾏、哪些代码⾏不执⾏，从⽽让程序按你的要求执⾏你要执⾏的代码。
例如，来看⼀个让⽤户指出他到过哪些地⽅的程序。在这个程序中，可在⽤户输⼊'quit'后使⽤ break 语句⽴即退出 while 循环：

```python
prompt = "\nPlease enter the name of a city you have visited:"
prompt += "\n(Enter 'quit' when you are finished.) "
while True:
		city = input(prompt)
		if city == 'quit':
				break
		else:
				print(f"I'd love to go to {city.title()}!")
>>>
Please enter the name of a city you have visited: (Enter 'quit' when you are finished.) New York
I'd love to go to New York!
Please enter the name of a city you have visited: (Enter 'quit' when you are finished.) San Francisco
I'd love to go to San Francisco!
Please enter the name of a city you have visited: (Enter 'quit' when you are finished.) quit
```

以 while True 打头的循环将不断运⾏，直到遇到 break 语 句。这个程序中的循环不断地让⽤户输⼊他到过的城市的名字，直到⽤户输⼊'quit'为⽌。在⽤户输⼊'quit'后，将执⾏ break 语句，导致Python 退出循环。

注意：在所有 Python 循环中都可使⽤ break 语句。例如，可使⽤ break 语句来退出遍历列表或字典的 for 循环。

7.2.5 在循环中使⽤ continue

要返回循环开头，并根据条件测试的结果决定是否继续执⾏循环，可使⽤continue 语句，它不像 break 语句那样不再执⾏余下的代码并退出整个循环。例如，来看⼀个从1数到10，只打印其中奇数的循环：

```python
current_number = 0
while current_number < 10:
		current_number += 1
		if current_number % 2 == 0:
				continue

		print(current_number)
>>>
1
3
5
7
9
```

⾸先将 current_number 设置为0，由于它⼩于10，Python 进⼊ while循环。进⼊循环后，以步⻓为1的⽅式往上数，因此current_number为1。接下来，if 语句检查 current_number 与 2 的求模运算结果。如果结果为0（意味着 current_number 可被 2 整除）， 就执⾏ continue 语句，让 Python 忽略余下的代码，并返回循环的开头。 如果当前的数不能被 2 整除，就执⾏循环中余下的代码，将这个数打印出来。

7.2.6 避免⽆限循环

每个while循环都必须有结束运⾏的途径，这样才不会没完没了地执⾏下去。例如，下⾯的循环从1数到5：

```python
x = 1
while x <= 5:
		print(x)
		x += 1
```

如果像下⾯这样不⼩⼼遗漏了代码⾏`x += 1`，这个循环将没完没了地运⾏：

```python
x = 1
while x <= 5:
		print(x)
>>>
1
1
1
1
--snip--
```

在这⾥，x 的初始值为 1，但根本不会变。因此条件测试 x <= 5 始终为 True，导致 while 循环没完没了地打印 1。

每个程序员都会偶尔不⼩⼼地编写出⽆限循环，在循环的退出条件⽐较微妙时尤其如此。如果程序陷⼊⽆限循环，既可按 Ctrl + C，也可关闭显⽰程 序输出的终端窗⼝。

要避免编写⽆限循环，务必对每个 while 循环进⾏测试，确保它们按预期那样结束。如果希望程序在⽤户输⼊特定值时结束，可运⾏程序并输⼊该值。如果程序在这种情况下没有结束，请检查程序处理这个值的⽅式，确认程序⾄少有⼀个地⽅导致循环条件为 False 或导致 break 语句得以执⾏。

注意：与众多其他的编辑器⼀样，VS Code 也在内嵌的终端窗⼝中显⽰输出。要结束⽆限循环，可在输出区域中单击⿏标，再按 Ctrl + C。

7.3 使⽤ while 循环处理列表和字典

到⽬前为⽌，我们每次都只处理了⼀项⽤户信息：获取⽤户的输⼊，再将输⼊打印出来或做出响应；循环再次运⾏时，获取另⼀个输⼊值并做出响应。然⽽，要记录⼤量的⽤户和信息，需要在 while 循环中使⽤列表和字典。

for 循环是⼀种遍历列表的有效⽅式，但不应该在 for 循环中修改列表，否则将导致 Python 难以跟踪其中的元素。要在遍历列表的同时修改它，可使⽤ while 循环。通过将 while 循环与列表和字典结合起来使⽤，可收集、存储并组织⼤量的输⼊，供以后查看和使⽤。

7.3.1在列表之间移动元素

假设有⼀个列表包含新注册但还未验证的⽹站⽤户。验证这些⽤户后，如何将他们移到已验证⽤户列表中呢？⼀种办法是使⽤⼀个 while 循环，在 验证⽤户的同时将其从未验证⽤户列表中提取出来，再将其加⼊已验证⽤户列表。代码可能类似于下⾯这样：

```python
unconfirmed_users = ['alice', 'brian', 'candace']
confirmed_users = []
while unconfirmed_users:
		current_user = unconfirmed_users.pop()

		print(f"Verifying user: {current_user.title()}")
		confirmed_users.append(current_user)

print("\nThe following users have been confirmed:")
for confirmed_user in confirmed_users:
		print(confirmed_user.title())
>>>
Verifying user: Candace
Verifying user: Brian
Verifying user: Alice

The following users have been confirmed:
Candace
Brian
Alice
```

⾸先，创建⼀个待验证⽤户列表，其中包含⽤户 Alice、Brian 和 Candace，以及⼀个⽤于存储已验证⽤户的空列表。验证每个⽤户，直到没有未验证⽤户为⽌，将每个经过验证的⽤户都移到已验证⽤户列表中，while 循环将不断地运⾏，直到列表unconfirmed_users 变成空的。在这个循环中，⽅法 pop() 每次从列表 unconfirmed_users 末尾删除⼀个未验证的⽤户。由于 Candace 位于列表 unconfirmed_users 末尾，其名字将⾸先被删除、赋给变量 current_user 并加⼊列表confirmed_users。接下来是 Brian，然后是 Alice。 为了模拟⽤户验证过程，我们打印⼀条验证消息并将⽤户加⼊已验证⽤户列表。未验证⽤户列表越来越短，⽽已验证⽤户列表越来越⻓。未验证⽤户列表为空后结束循环，再打印已验证⽤户列表。

7.3.2 删除为特定值的所有列表元素

在第 3 章中，我们使⽤remove()函数来删除列表中的特定值。这之所以可⾏，是因为要删除的值在列表中只出现了⼀次。如果要删除列表中所有为特定值的元素，该怎么办呢？

假设有⼀个宠物列表，其中包含多个值为 'cat' 的元素。要删除所有这些元素，可不断运⾏⼀个 while 循环，直到列表中不再包含值 'cat'，如下所⽰：

```python
pets = ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
print(pets)

while 'cat' in pets:
		pets.remove('cat')

print(pets)
>>>
['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
['dog', 'dog', 'goldfish', 'rabbit']
```

⾸先创建⼀个列表，其中包含多个值为 'cat' 的元素。打印这个列表后， Python 进⼊ while 循环，因为它发现'cat' 在列表中⾄少出现了⼀次。 进⼊这个循环后，Python删除第⼀个 'cat' 并返回 while 代码⾏，然后发现 'cat' 还在列表中，因此再次进⼊循环。它不断删除 'cat'，直到在列表中不再包含这个值，然后退出循环并再次打印列表。

7.3.3 使⽤⽤户输⼊填充字典

⽤ while 循环提⽰⽤户输⼊任意多的信息。

创建⼀个调查程序，其中的循环在每次执⾏时都提⽰输⼊被调查者的名字和回答。我们将收集到的数据存储在⼀个字典中，以便将回答与被调查者关联起来：

设置⼀个标志，指出调查是否继续，提⽰输⼊被调查者的名字和回答，将回答存储在字典中，看看是否还有⼈要参与调查，调查结束，显⽰结果

```python
responses = {}
polling_active = True

while polling_active:
		name = input("\nWhat is your name? ")
		response = input("Which mountain would you like to climb someday? ")
		responses[name] = response
		repeat = input("Would you like to let another person respond? (yes/no) ")
		if repeat == 'no':
				polling_active = False
print("\n--- Poll Results ---")
for name, response in responses.items():
		print(f"{name} would like to climb {response}.")
>>>
What is your name? Eric
Which mountain would you like to climb someday? Denali
Would you like to let another person respond? (yes/no) yes
What is your name? Lynn
Which mountain would you like to climb someday? Devil's Thumb
Would you like to let another person respond? (yes/no) no

--- Poll Results ---
Eric would like to climb Denali.
Lynn would like to climb Devil's Thumb.
```

这个程序⾸先定义了⼀个空字典（responses），并设置了⼀个标志（polling_active）⽤于指出调查是否继续。只要 polling_active为 True，Python 就运⾏ while 循环中的代码。 在这个循环中，⾸先提⽰⽤户输⼊名字以及喜欢爬哪座⼭。然后将这些信息存储在字典 responses 中，并询问⽤户调查是否继续。如果⽤户输⼊ yes，程序将再次进⼊ while 循环；如果⽤户输⼊ no，标志 polling_active 将被设置为 False，while 循环就此结束。最后⼀个代码块显⽰调查结果。