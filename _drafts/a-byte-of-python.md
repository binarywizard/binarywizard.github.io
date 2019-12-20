**A Byte of Python**

1. 单引号`'`和双引号`"`效果一样

2. 不同格式化方式，输出相同

   ```python
   print('{0} was {1} years old when he wrote this book'.format(name, age))
   print('{name} was {age} years old when he wrote this book'.format(name=name, age=age))
   print(f'{name} was {age} years old when he wrote this book')
   ```

3. 更多format技巧

   ```python
   # decimal (.) precision of 3 for float '0.333'
   print('{0:.3f}'.format(1.0/3))
   # fill with underscores (_) with the text centered
   # (^) to 11 width '___hello___'
   print('{0:_^11}'.format('hello'))
   ```

   Output:

   ```python
   0.333
   ___hello___
   ```

4. `print`默认换行（`\n`），可以指定结束符

   ```python
   print('a', end='')
   print('b')
   print('a', end=' ')
   print('b', end=' ')
   print('c')
   ```

   Output:

   ```python
   ab
   a b c
   ```

   