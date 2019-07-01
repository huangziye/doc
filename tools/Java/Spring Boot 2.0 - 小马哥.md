
# SpringBoot易学

> 组件自动装配：规约大于配置，专注于核心业务
>
> 外部化配置：一次构建、按需调配，到处运行
>
> 嵌入式容器：内置容器、无需部署、独立运行
>
> Spring Boot Starter : 简化依赖、按需装配、自我包容
>
> Production-Ready : 一站式运维、生态无缝整合


# SpringBoot难精


> 组件自动装配：模式注解、@Enable模块、条件装配、加载机制
>
> 外部化配置：Environment抽象、生命周期、破坏性变更
>
> 嵌入式容器：Servlet Web容器、Reactive Web 容器
>
> Spring Boot Starter: 依赖管理、装配条件、装配顺序
>
> Production-Ready: 健康检查、数据指标、@Endpoint管控



# Spring Boot 与 Java EE 规范



- Web： Servlet （JSR-315、JSR-340）
- SQL：JDBC（JSR-221）
- 数据校验：Bean Validation（JSR 303、JSR-349）
- 缓存：Java Caching API（JSR-107）
- WebSockets：Java API for WebSocket（JSR-356）
- Web Services：JAX-WS（JSR-224）
- Java管理：JMX（JSR 3）
- 消息：JMS（JSR-914）



# 核心特性


## Spring Boot三大特性


- 组件自动装配：Web MVC 、Web Flux、JDBC等
- 嵌入式Web容器：Tomcat、Jetty以及Undertow
- 生产准备特性：指标、健康检查、外部化配置等


## 组件自动装配


- 激活：@EnableAutoConfiguration
- 配置：/META-INF/spring.factories
- 实现：XXXAutoConfiguration
- 代码：@EnableAutoConfiguration


```
//在SpringBootApplication中也是包含了EnableAutoConfiguration
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```


查看源码，包含EnableAutoConfiguration，因此我们直接启动DemoApplication是成功的。


```
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(
    excludeFilters = {@Filter(
    type = FilterType.CUSTOM,
    classes = {TypeExcludeFilter.class}
), @Filter(
    type = FilterType.CUSTOM,
    classes = {AutoConfigurationExcludeFilter.class}
)}
)
public @interface SpringBootApplication{}
```



而对于配置文件，在Spring中是大部分存在的。



## 嵌入式Web容器



- Web Servlet：Tomcat、Jetty和Undertow
- Web Reactive：Netty Web Server


## 生产准备特性



- 指标：/actuator/metrics
- 健康检查：/actuator/health
- 外部化配置：/actuator/configprops




# Web应用



## 传统Servlet应用


- Servlet组件：Servlet、Filter、Listener
- Servlet注册：Servlet注解、Spring Bean、RegistrationBean
- 异步非阻塞：异步Servlet、非阻塞Servlet


### 依赖


```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```


### 实现


- 添加@WebServlet注解
- 根据3.1规范继承HttpServlet
- URL映射：@WebServlet(urlPatterns = "/my/servlet")
- 在启动类上加注册：@ServletComponentScan(basePackages = "com.myself.demo.web.servlet")
- 启动SpringBoot，可以看到


```
2018-10-10 11:23:56.607 INFO 21788 --- [ost-startStop-1] o.s.b.w.servlet.ServletRegistrationBean : Servlet com.myself.demo.web.servlet.MyServlet mapped to [/my/servlet]
```



## 异步非阻塞Servlet



- 启动WebServlet支持异步处理


```
@WebServlet(urlPatterns = "/my/servlet",asyncSupported = true
```


- 启动异步操作，以新线程执行，并在执行后触发完成


```
//映射、继承HttpServlet编程规范 ,asyncSupported支持异步处理
@WebServlet(urlPatterns = "/my/servlet",asyncSupported = true)
public class MyServlet extends HttpServlet {
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        //开始异步操作
        AsyncContext asyncContext = req.startAsync();

        //启动
        asyncContext.start(()->{
            try {
                resp.getWriter().println("Hello,World!");
                //触发完成
                asyncContext.complete();
            } catch (IOException e) {
                e.printStackTrace();
            }
        });
    }
}
```


> 注意：异步较为复杂，以上只是一个简单的实现例子





## Spring Web MVC应用



- Web MVC视图：模版引擎、内容协商、异常处理等
- Web MVC REST：资源服务、资源跨域、服务发现等
- Web MVC 核心：核心架构、处理流程、核心组件



### Web MVC 视图


- ViewResolver
- View


> 模版引擎


- Thymeleaf
- Freemarker
- JSP


> 内容协商


- ContentNegotiationConfigurer
- ContentNegotiationStrategy
- ContentNegotiationViewResolver



> 异常处理



- @ExceptionHandler

HandlerExceptionResolver --> ExceptionHandlerExceptionResolver

BasicErrorController(Spring Boot 项目默认错误页)

### Web MVC REST



> 资源服务


- @RequestMapping
- @GetMapping
- @ResponseBody
- @RequestBody


> 资源跨域


- CrossOrigin
- WebMvcConfigurer#addCorsMappings
- 传统解决方案（IFrame、JSONP）


> 服务发现


- HATEOS


### Web MVC 核心


> 核心架构


//后续补充

> 处理流程


//后续补充



> 核心组件



- DispatcherServlet
- HandlerMapping
- HandlerAdapter
- ViewResolver
- ...




## Spring Web Flux应用（Spring5.0）



- Reactor基础：Java Lambda、Mono、Flux
- Web Flux核心：Web MVC注解、函数式声明、异步非阻塞
- 使用场景：Web Flux优势和限制


> Web MVC 注解兼容


- @Controller
- @RequestMapping
- @ResponseBody
- @RequestBody



> 函数式声明


- RouterFunction


> 异步非阻塞


- Servlet 3.1 +
- Netty Reactor


> 使用场景


- 页面渲染
- REST应用
- 性能测试



## Web Server应用


- 切换Web Server
- Tomcat -> Jetty（Tomcat的优先级高于Jetty，所以需要剔除Tomcat依赖）


```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <!-- Exclude the Tomcat dependency -->
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>

<!-- Use Jetty instead -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>
```


- 替换Servlet容器 -> WebFlux

//这种情况下，需要先将其他外部服务剔除依赖


```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-webflux</artifactId>
</dependency>
```


- 自定义Servlet Web Server


> Web ServerFactoryCustomizer


- 自定义Reactive Web Server


> ReactiveWebServerFactoryCustomizer


# 数据相关



- JDBC：数据源、JDBCTemplate、自动装配
- JPA：实体映射关系、实体操作、自动装配
- 事务：Spring事务抽象、JDBC事务处理、自动装配



## JDBC


> 依赖

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```



> 数据源


- javax.sql.DataSource


## JDBCTemplate


> 自动装配


- DataSourceAutoConfiguration


## JPA


> 依赖

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```


> 实体映射


- @javax.persistence.OneToOne
- @javax.persistence.OneToMany
- @javax.persistence.ManyToOne
- @javax.persistence.ManyToMany


> 实体操作


- javax.persistence.EntityManager


> 自动装配


- HibernateJpaAutoConfiguration


## 事务（Transaction）


> 依赖

```
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-tx</artifactId>
</dependency>
```


> Spring事务抽象


- PlatformTransactionManager


> JDBC事务抽象


- DataSourceTransactionManager


> 自动装配


- TransactionAutoConfiguration


# 功能扩展


## Spring Boot 应用


- SpringApplication：失败分析、应用特性、事件监听等
- Spring Boot 配置：外部化配置、Profile、配置属性
- Spring Boot Starter：Starter开发、最佳时间


### 分析报告


- FailureAnalysisReporter


### 应用特性

- SpringApplication Fluent API

```
//二者等价
new SpringApplicationBuilder(DemoApplication.class).run(args);
//SpringApplication.run(DemoApplication.class, args);
```


### Spring Boot 配置


- 外部化配合 -> ConfigurationProperty
- @Profile
- 配置属性 -> ProperySources


# 运维管理


- Spring Boot Actuator
- 端点：各类Web 和 JMX Endpoints
- 健康检查：Heath、HealthIndicator
- 指标：内建Metrics、自定义Metrics


> 依赖

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```


> 端点（Endpoints）


- web Endpoints
- JMS EndPoints


> 健康检查（Health Checks）

- Health
- HealthIndicator


> 指标（Metrics）

- 内建 Metrics -> Web Endpoint: /actuator/metrics
- 自定义Metrics