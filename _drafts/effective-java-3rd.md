- 引言
- 创建和销毁对象
  - 第1条：用静态工厂方法代替构造器

# 引言

1. Java基本类库使用
   - java.lang
   - java.util
   - java.io
   - java.util.concurrent
   - java.util.function
2. Java特性
   - Lambda表达式
   - Stream流
   - Optional类
   - 接口中的默认方法
   - try-with-resource
   - @SafeVarargs注解
   - Module模块化
3. Java语言支持四种类型
   - 接口（包括注释）
   - 类（包括enum）
   - 数组
   - 基本类型
4. 方法的**签名**（signature）由它的名称和所有参数类型组成；签名**不包括**方法的返回类型。
5. API元素：类、接口、构造器、成员和序列化形式
6. 使用API编写程序的程序员被称为该API的用户，在类的实现中使用了API的类被称为该API的客户端。

# 创建和销毁对象

## 第1条：用静态工厂方法代替构造器

1. 静态工厂方法与设计模式中的工厂方法模式不同。

2. 提供静态工厂方法代替共有构造器的优劣势

   - 优势

     - 有名称。当一个类需要多个带有相同签名的构造器时，就用静态工厂方法，通过名称突出方法之间的区别

     - 不必在每次调用的时候创建一个新对象。可以使用预先构建好的实例，或者将构建好的实例缓存起来，进行重复利用。类似于享元（Flyweight）模式。

       > 编写实例受控的类原因：使类可以确保是一个Singleton或者是不可实例化的。还使得不可变的值类可以确保不会存在两个相等的实例，即当且仅当a==b时，a.equals(b)才为true。这是享元模式的基础。枚举类型保证了这一点。

     - 可以返回原返回类型的任何子类型的对象。API可以返回对象，同时又不会使对象的类变成公有的。

       > Java8之前，接口不能有静态方法，因此接口Type的静态工厂方法被放在一个名为Types的**不可实例化的伴生类**中。

     - 所返回的对象的类可以随着每次调用而发生变化，这取决于静态工厂方法的参数值。用户永远不知道也不关心它们从工厂方法中得到的对象的类，它们只关心它是EnumSet的某个子类。

       > EnumSet没有共有的构造器，只有静态工厂方法。返回两种子类之一的一个实例。RegalarEnumSet和JumboEnumSet。

     - 方法返回的对象所属的类，在编写包含该静态工厂方法的类时可以不存在

       > 这种灵活的静态工厂构成方法构成了服务提供者框架（Service Provider Framework）的基础，例如JDBC API。

       > 服务提供者框架有三个重要组件：**服务接口**，这是提供者实现的；**提供者注册API**，这是提供者用来注册实现的；**服务访问API**，这是客户端用来获取服务的实例。服务访问API是『灵活的静态工厂』，它构成了服务提供者框架的基础。第四个组件**服务提供者接口**是可选的，它表示产生服务接口之实例的工厂对象。如果没有服务提供者接口，实现就通过反射方式进行实例化。对于JDBC，Connection是服务接口的一部分，DriverManager.registerDriver是提供者注册API，DriverManager.getConnection是服务访问API，Driver是服务提供者接口。

       > 服务访问API可以返回比提供者需要的更丰富的服务接口，这就是**桥接（Bridge）模式**。Java6开始，Java提供了通用的服务提供者框架java.util.ServiceLoader,因此不需要自己编写了。

   - 缺点

     - 类如果不包含共有的或者被保护的构造器，就不能被子类化。例如，要想将Collections Framework中的任何便利的实现类子类话，这是不可能的。鼓励程序员使用复合（composition），而不是集成。
     - 程序员很难发现它们。

3. 静态工厂方发的一些惯用名称。

   * `from`——类型转换方法，只有单个参数，返回该类型的一个相对应的实例，例如：

     ```java
     Date d = Date.from(instant);
     ```

   * `of`——聚合方法，带有多个参数，返回该类型的一个实例，把它们合并起来，例如：

     ```java
      Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING);
     ```

   * `valueOf`——比`from`和`of`更繁琐的一种替代方法，例如：

     ```java
     BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);
     ```

   *  `instance`或者`getInstance`——返回的实例是通过方法的（如有）参数来描述的，但是不能说与参数具有相同的值，例如

     ```
     StackWalker luke = StackWalker.getInstance(options);
     ```

   * `create`或者`newInstance`——能够确保每次调用都返回一个新的实例，例如：

     ```java
      Object newArray = Array.newInstance(classObject, arrayLen);
     ```

   * `get{Type}`——像`getInstance`一样，但是在工厂方法处于不同的类中的时候使用。*Type*表示工厂方法所返回的对象类型，例如：

     ```java
     FileStore fs = File.getFileStore(path);
     ```

   *  `new{Type}`——像`newInstance`一样，但是在工厂方法处于不同的类中的时候使用，例如：

     ```java
     BufferedReader br = Files.newBufferedReader(path);
     ```

   * `{type}`——`get{Type}`和`new{Type}`的简版，例如：

     ```java
     List<Complaint> litany = Collections.list(legacyLitany);
     ```
