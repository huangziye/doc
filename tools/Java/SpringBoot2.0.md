

# 注解


- `@RestController`：等价于 `@Controller` 和 `@ResponseBody` 组合注解。`@RestController` 注解告知 spring 渲染结果字符串直接返回给调用者。
- `@RequestMapping`：注解提供了 `routing（路由）`信息，配置 `url` 映射。
- `@EnableAutoConfiguration`：自动引入 spring 所需要的 `bean`，它是 spring boot 核心注解。
- `@SpringBootApplication`：等价于 `@Configuration`、`@EnableAutoConfiguration` 和 `@ComponentScan` 组合注解。



# 在运行打包应用程序时开启远程调试支持

```
java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8000,suspend=n -jar target/myapplication-0.0.1-SNAPSHOT.jar
```
> IDEA 连接远程端口进行远程 debug，edit configurations -> remote -> 设置host和端口 -> 启动远程调试。其中：8000是端口

