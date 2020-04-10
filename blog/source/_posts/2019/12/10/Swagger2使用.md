---
title: Swagger2使用
date: 2019-12-10 15:00:04
categories:
- [工具,插件]
tags:
- java
---

## 一、工程创建

创建一个 Spring Boot 项目，加入 web 依赖，创建成功后，加入两个 Swagger2 相关的依赖

```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.9.2</version>
</dependency>
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.9.2</version>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

## 二、Swagger2 配置

Swagger2 的配置也是比较容易的，在项目创建成功之后，只需要开发者自己提供一个 Docket 的 Bean 即可

```java
@Configuration
@EnableSwagger2
public class SwaggerConfig {
    @Bean
    public Docket createRestApi() {
        return new Docket(DocumentationType.SWAGGER_2)
                .pathMapping("/")
                .select()
                .apis(RequestHandlerSelectors.basePackage("io.longlong.controller"))
                .paths(PathSelectors.any())
                .build().apiInfo(new ApiInfoBuilder()
                        .title("项目名称")
                        .description("项目简介")
                        .version("1.0")
                        .contact(new Contact("long long","https://woilanlan.github.io","test@gmail.com"))
                        .license("The Apache License")
                        .licenseUrl("https://woilanlan.github.io")
                        .build());
    }
}
```

这里提供一个配置类，首先通过 @EnableSwagger2 注解启用 Swagger2 ，然后配置一个 Docket Bean，这个 Bean 中，配置映射路径和要扫描的接口的位置，

在 apiInfo 中，主要配置一下 Swagger2 文档网站的信息，例如网站的 title，网站的描述，联系人的信息，使用的协议等等。

启动项目，访问 <http://localhost:8080/swagger-ui.html> 进行查看

## 三、创建接口

UserController.java

```java
@RestController
@Api(tags = "用户管理相关接口")
public class UserController {

    @Autowired
    UserService userService;

    @GetMapping("/users")
    @ApiOperation("查询所有用户的接口")
    @ApiImplicitParams({
            @ApiImplicitParam(name = "page",value = "页码",defaultValue = "1"),
            @ApiImplicitParam(name = "count",value = "每页显示几条",defaultValue = "5")
    })
    public List<User> getAllUser(@RequestParam(defaultValue = "1") Integer page, @RequestParam(defaultValue = "5") Integer count){
        System.out.println("getAllUser");
        return userService.getAllUser(page,count);
    }

    @GetMapping("/user/{id}")
    @ApiOperation("根据id查询用户的接口")
    @ApiImplicitParam(name = "id", value = "用户id", required = true)
    public User getUserById(@PathVariable Integer id){
        return userService.getUserById(id);
    }

    @PostMapping("/user")
    @ApiOperation("新增用户的接口")
    public String addUser(@RequestBody User user) {
        int result = userService.addUser(user);
        return "添加成功";
    }
}
```

注解说明：

- @Api 注解可以用来标记当前 Controller 的功能。
- @ApiOperation 注解用来标记一个方法的作用。
- @ApiImplicitParam 注解用来描述一个参数，可以配置参数的中文含义，也可以给参数设置默认值，这样在接口测试的时候可以避免手动输入。
- 如果有多个参数，则需要使用多个 @ApiImplicitParam 注解来描述，多个 @ApiImplicitParam 注解需要放在一个 @ApiImplicitParams 注解中。
- 需要注意的是，@ApiImplicitParam 注解中虽然可以指定参数是必填的，但是却不能代替 @RequestParam(required = true) ，前者的必填只是在 Swagger2 框架内必填，抛弃了 Swagger2 ，这个限制就没用了，所以假如开发者需要指定一个参数必填， @RequestParam(required = true) 注解还是不能省略。
- 如果参数是一个对象（例如上文的更新接口），对于参数的描述也可以放在实体类中。

user.java

```java
@Data
@ApiModel
public class User {
    @ApiModelProperty(value = "id")
    private Long id;
    @ApiModelProperty(value = "姓名")
    private String name;
    @ApiModelProperty(value = "年龄")
    private Integer age;
    @ApiModelProperty(value = "邮箱")
    private String email;
}
```

刷新刚刚打开的页面，可以看到相关的接口描述

参数类型下面标记

- query 表示参数以 key/value 的形式传递
- body 表示参数以请求体的方式传递，例如上文的新增接口
- path 表示参数放在路径中传递，例如根据 id 查询用户的接口

## 四、在 Security 中的配置

如果我们的 Spring Boot 项目中集成了 Spring Security，那么如果不做额外配置，Swagger2 文档可能会被拦截。

需要在 Spring Security 的配置类中重写 configure 方法，添加如下过滤即可：

```java
@Override
public void configure(WebSecurity web) throws Exception {
    web.ignoring()
            .antMatchers("/swagger-ui.html")
            .antMatchers("/v2/**")
            .antMatchers("/swagger-resources/**");
}
```
