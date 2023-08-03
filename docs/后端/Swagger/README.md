# Swagger

## 简介

> Swagger 是一款可以根据 Resutful 风格生成接口开发文档的工具，并且支持做测试的一款中间件。

## SpringBoot 整合 Swagger2

1. 导入依赖

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
```

2. 修改配置文件

> spring.mvc.pathmatch.matching-strategy: ant_path_matcher 的作用<br>
解决 SpringBoot 2.6.0 与 swagger 冲突问题<br>
原因是在 Spripgboot 2.6.0 中将 SpringMVC 默认路径匹配策略从AntPathMatcher 更改为 PathPatternParser，导致出错，
解决办法是切换回原先的 AntPathMatchen。

```yml
spring:
  # 将mvc的路径策略改为 ant_path_matcher 以适配 Swagger，不改的话会报空指针异常
  mvc:
    pathmatch:
      matching-strategy: ant_path_matcher
```

3. 在启动类上方添加注解，开启 Swagger2

```java
@SpringBootApplication
//开启Swagger2
@EnableSwagger2
public class CreatorMCBlogApplication {

    public static void main(String[] args) {
        SpringApplication.run(CreatorMCBlogApplication.class);
    }
}
```

> 现在启动项目后，已经可以访问 Swagger 生成的接口文档了<br>
文档地址示例：http://localhost:8080/swagger-ui.html

## Controller 配置

```java
@RestController
@RequestMapping("/comment")
@Api(tags = "评论", description = "评论相关接口")
public class CommentController {
    ...
}
```

效果：
![Swagger演示1.png](https://s2.loli.net/2023/08/03/yR7ZIuq1EOcaV2i.png)

## 接口配置

### 接口描述配置

```java
@ApiOperation(value = "评论列表", notes = "获取评论列表")
public ResponseResult linkCommentList(@PathVariable Integer pageNum, @PathVariable Integer pageSize) {
    return commentService.commentList(SystemConstants.LINK_COMMENT, null, pageNum, pageSize);
}
```

效果：
![Swagger演示2.png](https://s2.loli.net/2023/08/03/4Cl8Z92tNdKik3x.png)

### 接口参数配置

```java
@ApiImplicitParams({
        @ApiImplicitParam(name = "pageNum", value = "第几页"),
        @ApiImplicitParam(name = "pageSize", value = "每页几条记录")
})
public ResponseResult linkCommentList(@PathVariable Integer pageNum, @PathVariable Integer pageSize) {
    return commentService.commentList(SystemConstants.LINK_COMMENT, null, pageNum, pageSize);
}
```

效果：
![Swagger演示3.png](https://s2.loli.net/2023/08/03/LvBNYi1dcmlVEk8.png)

## 实体类配置

### 实体的描述配置