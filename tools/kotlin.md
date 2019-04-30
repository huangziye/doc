
# 常用注解


- `@JvmOverloads` ：考虑到Java并没有参数默认值的概念，当你在Java中调用带有参数默认值值的Kotlin函数时，你必须显式的指定所有参数的值。如果你经常需要从
Java中调用一个函数并想让Java调用者易于使用，你可以用 @JvmOverloads 对它进行标注。它将指示编译器以从最后一个参数开始逐个忽略每一个参数的方式产生重载的Java
函数。 举个例子，如果你用 @JvmOverloads 标注了 joinToString() ，以下的重载将会产生：


```
/* Java */
String joinToString(Collection<T> collection, String separator, String prefix, String postfix);
String joinToString(Collection<T> collection, String separator, String prefix);
String joinToString(Collection<T> collection, String separator); 
String joinToString(Collection<T> collection);
```
> 每一个重载（函数）都为忽略了签名的参数使用了默认值。














# 摆脱静态工具类：顶层(top-level)函数和属性


### 改变文件的类名

为了改变生成的包含 Kotlin 顶层函数的类的名字，你可以给文件添加 `@JvmName` 标注。把它放置在文件的开头位于包名之前的地方：


```
@file:JvmName("StringFunctions") // 1 指定类名的标注
package strings // 2 包声明跟在文件标注后面
fun joinToString(...): String { ... }
```

现在函数可以这样调用

```
/* Java */
import strings.StringFunctions;
StringFunctions.joinToString(list, ", ", "", "");
```



### 顶层属性（TOP-LEVEL PROPERTIES）


就像函数那样，属性可以放在文件的顶层。保存类外部的单独的数据块并不常用，但依然非常有用。 　举个例子，你可以使用 `var` 属性来计算某个操作被执行的次数：


```
var opCount = 0 // 1 包级别的属性声明
fun performOperation() {
    opCount++ // 2 改变属性的值
    // ...
}
fun reportOperationCount() {
    println("Operation performed $opCount times") // 3 读取属性的值
}
```

这样一个属性的值将会被存储在一个静态字段中。 顶层属性（Top-level properties）也允许你在你的代码中定义常量：

```
val UNIX_LINE_SEPARATOR = "\n"
```

默认的，顶层属性就像其他属性一样，以访问器（一个 `val` 属性的读取函数或者一对读取函数/设置函数）的形式暴露给 Java 代码。如果你想把常量暴露给 Java 代码组委一个 `public
static final` 字段来让它的用法更加自然，你可以用 `const` 修饰器标记它（原始类型属性是允许这样做的， `String` 类型也是）：

```
const val UNIX_LINE_SEPARATOR = "\n"
```

这将得到跟以下等价的Java代码：

```
/* Java */
public static final String UNIX_LINE_SEPARATOR = "\n";
```



# 扩展函数


扩展函数就是在你添加的函数的名字之前放置你需要扩展的类或者接口的名字。这个类名叫做接收器类型（receiver type），而你调用的扩展函数的值叫做接收
器对象（receiver object）。

```
fun String.lastChar(): Char = this.get(this.length - 1)
```


# 导入和扩展函数

当你定义一个扩展函数是，它并不会自动在你的整个项目中变为可用。相反的，它需要被导入，就像其他的类或者函数那样。这有助于避免意外的命名冲突。Kotlin 允许你使用你用于类
的同样单独语法来导入单独的函数：


```
import strings.lastChar
val c = "Kotlin".lastChar()
```

当然，使用通配符（ `*` ）导入也是可以的：


```
import strings.*
val c = "Kotlin".lastChar()
```

你可以使用 `as` 关键词来该改变你所导入的类或者函数的名字：


```
import strings.lastChar as last
val c = "Kotlin".last()
```


当你在不同的包中有多个同名的函数并且你想在同一个文件中使用它们时，在导入中改变一个名字是非常有用的，对于常规的类和函数，你在这种情况下有另外的选择：你可以使
用完全有效的名字来有用类或者函数。对于扩展函数，这个语法要求你使用缩写名字，因此一个导入声明中的 `as` 关键词是解决冲突的唯一方法。



# 从 Java 中调用扩展函数


调用一个扩展函数并没有涉及适配器对象的创建或者任何其他运行时开销。在底层方面，一个扩展函数是一个接受接收器对象作为第一个参数的静态方法。 这让（我们）从 Java 中使用扩展函数变得非常容易：你调用静态方法并传递接收器对象实例。就像和其他顶层函数，包含这个方法的 java 类的名字由声明这个函数的文件的名字决定。我们可以把代码声明在一个 `StringUtil.kt` 文件中：


```
/* Java */
char c = StringUtilKt.lastChar("Java");
```

这个扩展函数被声明为顶层函数，因此它被编译为一个静态方法。你从 `Java` 中静态的可以导入 `lastChar` 方法，用法简化为 " lastChar "。比起 `Kotlin` 版本来，这份代码的可读性多少有点下降了，但是从 Java 的角度来说这是符合语言习惯的。

```
fun <T> Collection<T>.joinToString(separator: String = ",", prefix: String = "", postfix: String = ""): String {
    val sb = StringBuilder(prefix)
    for ((index, element) in this.withIndex()) {
        if (index > 0) sb.append(separator)
        sb.append(element)
    }
    sb.append(postfix)
    return sb.toString()
}
```


> 扩展的静态类型也意味着扩展函数不能被子类覆盖（overridden）。



# 不可覆盖（overriding）的扩展函数


方法覆盖在 Kotlin 对平常的成员函数是有效的，但是你不能覆盖一个扩展函数。



扩展函数并不是类的一部分。它们是声明在类的外部的。尽管你可以为某个基类和它的子类用同样的名字和参数类型来定义扩展函数，被调用的函数依赖于已被声明的静态类型的变量，而不是依赖于变量值的运行时类型。 　接下来的例子展示了两个声明在 View 和 Button 类的 `showOff` 扩展函数：


```
fun View.showOff() = println("I'm a view!")
fun Button.showOff() = println("I'm a button!")
>>> val view: View = Button()
>>> view.showOff() // 1 扩展函数被静态的方式进行解析
I'm a view!
```

当你用一个 View 类型的变量调用 `showOff` 时，对应的扩展将会被调用，尽管这个值的真实类型是 Button 。 　如果你重新调用了用 Java 编译成静态函数的扩展函数，这个行为对你来说应该是很清晰的，因为 Java 以同样的方式来选择函数：


```
/* Java */
>>> View view = new Button();
>>> ExtensionsKt.showOff(view); // 1 showOff函数被声明在extensions.kt文件中
I'm a view!
```


如你所见，覆盖对于扩展函数来说是不起作用的：Kotlin以静态解析它们。


> 注意 如果类有一个成员函数跟一个扩展函数有着相同的签名，成员函数总是优先的。当
  你扩展类的API时，你应该记住这一点：如果你添加了一个跟你已定义类的客户端（调用
  者）的扩展函数具有同样的签名成员函数，同时客户端随后重新编译了他们的代码，它
  将会改变它的含义并开始指向一个新的成员函数。




# 扩展属性（Extension properties）


扩展属性提供了一种方法用能通过属性语法进行访问的API来扩展类。而不是函数的语法。尽
管它们被叫做属性，它们不能拥有任何的状态：它不可能添加额外的字段到现有的Java对象
实例。但是更简短的语法在某些时候任然是很方便的。 　在前一个章节，你定义了一个函
数 `lastChar` 。现在让我们把它转换成一个属性：

```
val String.lastChar: Char
    get() = get(length - 1)
```


