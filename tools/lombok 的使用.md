
`Lombok` 能以简单的注解形式来简化 java 代码，提高开发人员的开发效率。例如开发中经常需要写的 `javabean`，都需要花时间去添加相应的 `getter/setter`，也许还要去写`构造器`、`equals`等方法，而且需要维护，当属性多时会出现大量的 `getter/setter`方法，这些显得很冗长也没有太多技术含量，一旦修改属性，就容易出现忘记修改对应方法的失误。

`Lombok` 能通过注解的方式，在编译时自动为属性生成`构造器`、`getter/setter`、`equals`、`hashcode`、`toString`方法。出现的神奇就是在源码中没有 `getter` 和 `setter` 方法，但是在编译生成的字节码文件中有 `getter` 和 `setter`方法。这样就省去了手动重建这些代码的麻烦，使代码看起来更简洁些。


# 1. 安装 `lombok` 插件

使用前需要安装 `lombok` 插件


[IDEA插件安装地址](https://jingyan.baidu.com/article/0a52e3f4e53ca1bf63ed725c.html)

[Eclipse插件安装地址](https://jingyan.baidu.com/article/b7001fe1aaa0c30e7282dd8a.html)



# 2. 插件配置

[查看最新版本](https://projectlombok.org/setup/maven)

```
<dependencies>
	<dependency>
		<groupId>org.projectlombok</groupId>
		<artifactId>lombok</artifactId>
		<version>1.18.6</version>
		<scope>provided</scope>
	</dependency>
</dependencies>
```


# 3. 常用的注解

- `@Setter` `@Getter` ：可以为相应的属性自动生成 `Getter/Setter` 方法。

```
import lombok.Getter;
import lombok.Setter;
import lombok.ToString;
import java.util.Date;
 
@Setter
@Getter
@ToString
public class User {
    private Integer id;
    private String name;
    private Integer age;
    private String sex; 
    private Date birthday;
}
```

- `@NonNull` ：该注解用在属性或构造器上，`Lombok` 会生成一个非空的声明，可用于校验参数，能帮助避免空指针。

```
import lombok.NonNull;
 
public class NonNullExample extends Something {
    private String name;
    
    public NonNullExample(@NonNull Person person) {
        super("Hello");
        this.name = person.getName();
    }
}
```

- `@Cleanup` ：该注解能帮助我们自动调用 `close()` 方法，很大的简化了代码。

```
import lombok.Cleanup;
import java.io.*;
 
public class CleanupExample {
    public static void main(String[] args) throws IOException {
        @Cleanup InputStream in = new FileInputStream(args[0]);
        @Cleanup OutputStream out = new FileOutputStream(args[1]);
        byte[] b = new byte[10000];
        while (true) {
            int r = in.read(b);
            if (r == -1) break;
            out.write(b, 0, r);
        }
    }
}
```


- `@EqualsAndHashCode` ：默认情况下，会使用所有非静态（`non-static`）和非瞬态（`non-transient`）属性来生成 `equals` 和 `hasCode`，也能通过 `exclude` 注解来排除一些属性。


```
import lombok.EqualsAndHashCode;
 
@EqualsAndHashCode(exclude={"id", "shape"})
public class EqualsAndHashCodeExample {
    private transient int transientVar = 10;
    private String name;
    private double score;
    private Shape shape = new Square(5, 10);
    private String[] tags;
    private int id;
    
    public String getName() {
        return this.name;
    }
    
    @EqualsAndHashCode(callSuper=true)
    public static class Square extends Shape {
        private final int width, height;
        
        public Square(int width, int height) {
            this.width = width;
            this.height = height;
        }
    }
}
```


- `@ToString` ：类使用 `@ToString` 注解，`Lombok` 会生成一个 `toString()` 方法，默认情况下，会输出类名、所有属性（会按照属性定义顺序），用逗号来分割。

代替效果为：

```
@Override 
public String toString() {
    return "Square(super=" + super.toString() + ", width=" + this.width + ", height=" + this.height + ")";
}
```


- `@Data` ：注解在类上，会为类的所有属性自动生成 `setter/getter`、`equals`、`canEqual`、`hashCode`、`toString` 方法，如为 `final` 属性，则不会为该属性生成 `setter` 方法。这个注解可是说是非常强大。




# lombok的工作原理：


`Lombok` 本质上就是一个实现了“JSR 269 API”的程序。在使用 javac 的过程中，它产生作用的具体流程如下：

1. javac 对源代码进行分析，生成了一棵抽象语法树（AST）
2. 运行过程中调用实现了“JSR 269 API”的 Lombok 程序
3. 此时 Lombok 就对第一步骤得到的AST进行处理，找到 @Data 注解所在类对应的语法树（AST），然后修改该语法树（AST），增加 getter 和 setter 方法定义的相应树节点
4. javac 使用修改后的抽象语法树（AST）生成字节码文件，即给 class 增加新的节点（代码块）




