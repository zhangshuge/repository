---
title: jdk8新特性
date: 2018-09-04 21:43:30
categories: java
tags: java
---


## 1、lambda表达式

​	Java8的最大变化是引入了lambda表达式——一种紧凑的、传递行为的方式。在学lambda时先了解下什么是函数式编程。函数式编程：函数式编程是种编程方式，它将电脑运算视为函数的计算。函数编程语言最重要的基础是λ演算（lambda calculus），而且λ演算的函数可以接受函数当作输入（参数）和输出（返回值）。 和指令式编程相比，函数式编程强调函数的计算比指令的执行重要。 和过程化编程相比，函数式编程里函数的计算可随时调用。 ***其核心就是：在思考问题时，使用不可变的值和函数，函数对一个值进行处理，映射成另一个值。***虽然看着很先进，其实Lambda表达式的本质只是一个"[**语法糖**](http://zh.wikipedia.org/wiki/%E8%AF%AD%E6%B3%95%E7%B3%96)",由编译器推断并帮你转换包装为常规的代码,因此你可以使用更少的代码来实现同样的功能。 看个例子：

```java
public class OperatingFunction {
    public static void main(String[] args) {
        /*
         *  现在有一个这样的数学表达式
         *  　　(1 + 2) * 3 - 4
         */

        //传统的过程式编程，可能这样写
        int a = 1 + 2;
        int b = a * 3;
        int c = b - 4;

        //函数式编程要求使用函数，我们可以把运算过程定义为不同的函数，然后写成下面这样：
        int d = subtraction(multiplication(addition(1,2),3),4);
    }

    private static int addition(int a, int b) {
        return a + b;
    }

    private static int subtraction(int a, int b) {
        return a - b;
    }
    private static int multiplication(int a,int b){
        return a * b;
    }
}
```

### 1.1 lambda表达式基本语法

==(parameters) -> expression  或者  (parameters) -> statement  或者 (parameters) -> {statements;}==

下面看几个简单的例子：

```java

//不需要参数，返回5
final IntSupplier intSupplier = () -> 5;

//接收一个参数，返回乘以2的结果
IntUnaryOperator intUnaryOperator = x -> 2 * x;

//接收两个参数，返回差值
IntBinaryOperator reduce = (x, y) -> x - y;
System.out.println(reduce.applyAsInt(4,5));

//指定接收连个int类型参数，返回和
IntBinaryOperator sum = (int x,int y) -> x + y;
System.out.println(sum.applyAsInt(2,3));

//接收一个String对象，在控制台打印
final Consumer<String> stringConsumer = (String s) -> System.out.println(s);
stringConsumer.accept("你好");
```

从上面的例子中我们可以看出`IntBinaryOperator reduce= (x, y) -> x - y;`这行代码并不是两个数相减，而是创建了一个函数，用来计算两个数相减的结果。变量reduce的类型是IntBinaryOperator,它不是两个数相减的结果，而是将这两个数相减的第9行代码。Lambda表达式的参数可以由编译器推断得出例如第九行，也可以有我们显示的声明例如第13行。

### 1.2 引用值，而不是变量

​	我们都知道在Java中匿名类中如果要访问局部变量的话，那个局部变量必须显式的声明为final。 如下代码：

```java
public class InnerFinal {
    public static void main(String[] args) {
        String version = "1.8";
        fool(new Supplier<String>() {
            @Override
            public String get() {
                return version;
            }
        });
    }
    static void fool(Supplier<String> supplier){
        System.out.println(supplier.get());
    }
}

```

这里的version变量没有显示的声明为final,并不是意味着它是可以修改的。JDK7以前版本都是需要显示的使用final修饰，而JDK8以后可以不显示的修饰了，但是该变量实际上还是final类型的，只不过不需要程序员显示声明了。那么引出一个问题，为什么内部类或者lambda表达式引用局部变量时，该变量一定要是final的呢？

在Java的经典著作《Effective Java》、《Java Concurrency in Practice》里，大神们都提到：匿名函数里的变量引用，也叫做变量引用泄露，会导致线程安全问题，因此在Java8之前，如果在匿名类内部引用函数局部变量，必须将其声明为final，即不可变对象。 网上找到这么一句话

>因为实例变量存在堆中，而局部变量是在栈上分配，Lambda 表达(匿名类) 会在另一个线程中执行。如果在线程中要直接访问一个局部变量，可能线程执行时该局部变量已经被销毁了，而 final 类型的局部变量在 Lambda 表达式(匿名类) 中其实是局部变量的一个拷贝。

这句话比较好理解，但是其中内部类会在另一个线程中执行这句需要商榷，没有仔细研究的前提下对此保留疑问。



### 1.3 函数接口

​	函数式接口(Function Interface)是只有一个抽象方法的接口(除了隐藏的Object对象的公共方法)，作用Lambda表达式的类型。也可以叫做SAM类型的接口(Single Abstract Method)。

#### 1.3.1 @FunctionalInterface

​	Java 8为函数式接口引入了一个新注解@FunctionalInterface，主要用于***编译级错误检查***，加上该注解，当你写的接口不符合函数式接口定义的时候，编译器会报错。

正确的例子：

```java
@FunctionalInterface
public interface FunctionInterfaceAnnotation {
    void sayMessage(String message);
}
```

错误的例子：

```java
@FunctionalInterface
public interface FunctionInterfaceAnnotation {
    void sayMessage(String message);
    //有两个抽象方法
    void beforeSay(String message);
}
```

 ![](C:\Users\zhangchi\Pictures\f5c0b3a9a5190df479d621541f947457.png)

编译器会提示非法函数接口。

==加不加@FunctionalInterface对于接口是不是函数式接口没有影响，该注解知识提醒编译器去检查该接口是否仅包含一个抽象方法==

​	函数式接口里允许定义默认方法、静态方法、Object类里的Public方法。默认方法需要用default关键词修饰。

```java
@FunctionalInterface
public interface FunctionInterfaceAnnotation {
    /**
     * 有且只有一个抽象方法，可以声明异常。
     *
     * @param message
     */
    void sayMessage(String message) throws Exception;

    /**
     * 允许定义默认方法(可定义多个)
     */
    default void beforeSay() {
    }

    /**
     * 允许定义静态方法(可定义多个)
     */
    static void init(){
    }

    /**
     * 允许定义java.lang.Object里的public方法
     * @param o
     * @return
     */
    @Override
    boolean equals(Object o);
}
```

#### 1.3.2 JDK8之前已有的函数式接口

- java.lang.Runnable
- java.util.concurrent.Callable
- java.security.PrivilegedAction
- java.util.Comparator
- java.io.FileFilter
- java.nio.file.PathMatcher
- java.lang.reflect.InvocationHandler
- java.beans.PropertyChangeListener
- java.awt.event.ActionListener
- javax.swing.event.ChangeListener

#### 1.3.3 新定义的函数式接口

Java 8也添加了一个包，叫做 java.util.function。它包含了很多类，用来支持Java的函数式编程 .

| 接口名称          | 参数  | 返回类型 | 描述                                                         |
| ----------------- | ----- | -------- | ------------------------------------------------------------ |
| Predicate<T>      | T     | boolean  | 传入一个参数，返回一个Boolean结果，抽象方法为boolean test(T t); |
| Consumer<T>       | T     | void     | 传入一个参数，没有返回值纯消费。抽象方法为void accept(T t);  |
| Function<T,R>     | T     | R        | 传入一个参数，返回一个结果。R apply(T t);                    |
| Supplier<T>       | None  | T        | 不需要参数，返回一个结果。T get();                           |
| UnaryOperator<T>  | T     | T        | 一元操作符，继承Function,传入参数的类型和返回参数的类型相同。 |
| BinaryOperator<T> | (T,T) | T        | 传入两个参数，返回一个相同类型结果。继承BigFunction          |



### 1.4 10个案例

#### 1.4.1 实现Runnable

```java
    private static void runNable(){
        new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("Java8之前使用匿名类实现！");
            }
        }).start();


        new Thread(() -> System.out.println("Java8可以使用lambda")).start();
    }
```

#### 1.4.2 监听事件

```java
// Java 8之前：
JButton show =  new JButton("Show");
show.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
    System.out.println("Event handling without lambda expression is boring");
    }
});

// Java 8方式：
show.addActionListener((e) -> {
    System.out.println("Light, Camera, Action !! Lambda expressions Rocks");
});
```

#### 1.4.3 迭代集合

```java
    private static void iterationCollection(){
        //java8之前写法
        List<String> features = Arrays.asList("Lambdas", "Default Method", "Stream API", "Date and Time API");
        for (String f : features){
            System.out.println(f);
        }

        //java8之后写法
        features.forEach(n -> System.out.println(n));
        //使用Java 8的方法引用更方便，方法引用由::双冒号操作符标示
        features.forEach(System.out::println);
    }
```

#### 1.4.4 使用lambda表达式和函数式接口Predicate

​	使用 java.util.function.Predicate 函数式接口以及lambda表达式，可以向API方法添加逻辑，用更少的代码支持更多的动态行为。下面是Java 8 Predicate 的例子，展示了过滤集合数据的多种常用方法。==Predicate接口非常适用于做过滤。==

```java
    private static void predicateEg(){
        List languages = Arrays.asList("Java", "Scala", "C++", "Haskell", "Lisp");

        System.out.println("Languages which starts with J :");
        filter(languages, (str)->str.toString().startsWith("J"));
        System.out.println("Languages which ends with a ");
        filter(languages, (str)->str.toString().endsWith("a"));

        System.out.println("Print all languages :");
        filter(languages, (str)->true);

        System.out.println("Print no language : ");
        filter(languages, (str)->false);

        System.out.println("Print language whose length greater than 4:");
        filter(languages, (str)->str.toString().length() > 4);
    }

    private static void filter(List languages, Predicate condition){
        languages.stream().filter((la) -> (condition.test(la))).forEach((la) -> {
            System.out.println(la);
        });
    }
```

可以看到，Stream API的过滤方法也接受一个Predicate，这意味着可以将我们定制的 filter() 方法替换成写在里面的内联代码，这就是lambda表达式的魔力。

#### 1.4.5 如何在lambda表达式中加入Predicate

​	java.util.function.Predicate 允许将两个或更多的 Predicate 合成一个。它提供类似于逻辑操作符AND和OR的方法，名字叫做and()、or()，用于将传入 filter() 方法的条件合并起来。

```java
Predicate<String> startsWithJ = (n) -> n.startsWith("J");
Predicate<String> fourLetterLong = (n) -> n.length() == 4;

System.out.println("找到所有以J开始，长度为四个字母的名字");
filter(languages,startsWithJ.and(fourLetterLong));
System.out.println("找到所有以J开始或者长度为四个字母的名字");
filter(languages,startsWithJ.or(fourLetterLong));
```

#### 1.4.6 使用lambda表达式的Map和Reduce示例

```java
public class MapAndReduce {
    public static void main(String[] args) {
        List<Integer> costBeforeTax = Arrays.asList(100, 200, 300, 400, 500);

        // 不使用lambda表达式为每个订单加上12%的税
        for (Integer cost : costBeforeTax) {
            double price = cost + 0.12 * cost;
            System.out.println(price);
        }

        //使用lambda表达式
        costBeforeTax.stream().map(c -> c + c * .12).forEach(System.out::println);
    }
}
```

 ![mapreduce](http://oy48q6kwm.bkt.clouddn.com/8bb3e29bb5ca4b00cc7ca7351aa92194.png)

​	在上个例子中，可以看到map将集合类（例如列表）元素进行转换的。还有一个 reduce() 函数可以将所有值合并成一个。Map和Reduce操作是函数式编程的核心操作，因为其功能，reduce 又被称为折叠操作。另外，reduce 并不是一个新的操作，你有可能已经在使用它。SQL中类似 sum()、avg() 或者 count() 的聚集函数，实际上就是 reduce 操作，因为它们接收多个值并返回一个值。流API定义的 reduceh() 函数可以接受lambda表达式，并对所有值进行合并。IntStream这样的类有类似 average()、count()、sum() 的内建方法来做 reduce 操作，也有mapToLong()、mapToDouble() 方法来做转换。这并不会限制你，你可以用内建方法，也可以自己定义。在这个Java 8的Map Reduce示例里，我们首先对所有价格应用 12% 的VAT，然后用 reduce() 方法计算总和。

```java
public class MapAndReduce {
    public static void main(String[] args) {
        List<Integer> costBeforeTax = Arrays.asList(100, 200, 300, 400, 500);

        // 不使用lambda表达式为每个订单加上12%的税，再计算总和
        double toatl = 0;
        for (Integer cost : costBeforeTax) {
            double price = cost + 0.12 * cost;
            toatl += price;
        }
        System.out.println("oldTotal:" + toatl);

        //使用lambda表达式
        double newTotal = costBeforeTax.stream().map(c -> c + c * .12).reduce((sum,c)->sum + c).get();
        System.out.println("newTotal:" + newTotal);
    }
}

```

 ![reduce](http://oy48q6kwm.bkt.clouddn.com/2763ff047c9e32bc3d9c5475ca3d9bef.png)

#### 1.4.7 通过过滤创建一个String列表

```java
        List<String> strList = Arrays.asList("abc", "", "bcd", "", "defg", "jk");
        // 创建一个字符串列表，每个字符串长度大于2
        List<String> filtered = strList.stream().filter(x -> x.length() > 2).collect(Collectors.toList());
        System.out.printf("Original List : %s, filtered list : %s %n", strList, filtered);
```

#### 1.4.8 对列表的每个元素应用函数

```java
        // 将字符串换成大写并用逗号链接起来
        List<String> G7 = Arrays.asList("USA", "Japan", "France", "Germany", "Italy", "U.K.","Canada");
        System.out.println(G7.stream().map(x -> x.toUpperCase()).collect(Collectors.joining(",")));
```

#### 1.4.9复制不同的值，创建一个子列表

​	本例展示了如何利用流的 distinct() 方法来对集合进行去重。

```java
        // 用所有不同的数字创建一个正方形列表
        List<Integer> numbers = Arrays.asList(9, 10, 3, 4, 7, 3, 4);
        List<Integer> distinct = numbers.stream().distinct().map(i -> i*i).collect(Collectors.toList());
        System.out.printf("Original List : %s,  Square Without duplicates : %s %n", numbers, distinct);
```

####1.4.10 计算集合元素的最大值、最小值、总和以及平均值

​	IntStream、LongStream 和 DoubleStream 等流的类中，有个非常有用的方法叫做 summaryStatistics() 。可以返回 IntSummaryStatistics、LongSummaryStatistics 或者 DoubleSummaryStatistic s，描述流中元素的各种摘要数据。在本例中，我们用这个方法来计算列表的最大值和最小值。它也有 getSum() 和 getAverage() 方法来获得列表的所有元素的总和及平均值。

```java
       //获取数字的个数、最小值、最大值、总和以及平均值
        List<Integer> primes = Arrays.asList(2, 3, 5, 7, 11, 13, 17, 19, 23, 29);
        IntSummaryStatistics stats = primes.stream().mapToInt(x -> x).summaryStatistics();
        System.out.println("Highest prime number in List : " + stats.getMax());
        System.out.println("Lowest prime number in List : " + stats.getMin());
        System.out.println("Sum of all prime numbers : " + stats.getSum());
        System.out.println("Average of all prime numbers : " + stats.getAverage());
```

### 1.5 Lambda表达式 vs 匿名类

​	既然lambda表达式即将正式取代Java代码中的匿名内部类，那么有必要对二者做一个比较分析。一个关键的不同点就是关键字 this。匿名类的 this 关键字指向匿名类，而lambda表达式的 this 关键字指向包围lambda表达式的类(外层类域)。另一个不同点是二者的编译方式。Java编译器将lambda表达式编译成类的私有方法。使用了Java 7的 invokedynamic 字节码指令来动态绑定这个方法。





## 2、Stream流

```java
List<String> threeHighCaloricDishNames =
                menu.stream()
                    .filter(d -> d.getCalories() > 300)
                    .map(Dish::getName)
                    .limit(3)
                    .collect(Collectors.toList());
```

![1508374379](https://github.com/zhangshuge/learn/blob/master/imgs/1508374379.jpg?raw=true)
集合注重的是数据，而流注重的是计算。和迭代器类似流也只能遍历一次，遍历完之后我们可以将这个流视为已被消费掉了



## ::
