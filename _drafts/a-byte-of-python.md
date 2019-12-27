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


5. 变量命名区分大小写，只识别`_`，无法识别`-`

6. `while`和`for`可以有`else`语句，当判断条件为`False`时执行，除非通过`break`跳出循环。

7. 在方法定义时参数为`parameters`，在方法调用时参数为`arguments`。

8. 在方法定义时，只有结尾部分的参数能设定默认值，非结尾部分不能设定默认值。因此`def func(a, b=5)`合法，而`def func(a=5, b)`非法。

9. `list`是可变的，`tuple`是不可变的。

10. 元祖中只包含一个元素时，需要再元素后面添加逗号，否则括号会被当做运算符使用。

    ```python
    tup = (50,)
    ```

11. `list`复制时需用`slice`方式，仅变量赋值只作为引用。