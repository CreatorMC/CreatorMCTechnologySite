# Spring
> Spring框架是一个开放源代码的J2EE应用程序框架，由Rod Johnson发起，是针对bean的生命周期进行管理的轻量级容器（lightweight container）。 Spring解决了开发者在J2EE开发中遇到的许多常见的问题，提供了功能强大IOC、AOP及Web MVC等功能。Spring可以单独应用于构筑应用程序，也可以和Struts、Webwork、Tapestry等众多Web框架组合使用，并且可以与 Swing等桌面应用程序AP组合。因此， Spring不仅仅能应用于J2EE应用程序之中，也可以应用于桌面应用程序以及小应用程序之中。Spring框架主要由七部分组成，分别是 Spring Core、 Spring AOP、 Spring ORM、 Spring DAO、Spring Context、 Spring Web和 Spring Web MVC。
> <p align="right"><a href="https://baike.baidu.com/item/spring/85061">——摘自百度百科</a></p>

[Spring官网](https://spring.io/)
# IOC（控制反转）

# DI（依赖注入）

# AOP（面向切面编程）
> 作用：在不改动原始方法的基础上对功能进行**增强**

## 相关名词解释
 - 代理（Proxy）：SpringAOP的核心是用代理模式实现的
 - 连接点（JoinPoint）：在SpringAOP中，理解为任意方法的执行
 - 切入点（Pointcut）：匹配连接点的式子，也是具有功能共性的方法描述
 - 通知（Advice）：若干方法的共性功能，在切入点处执行，最终体现为一个方法
 - 切面（Aspect）：描述通知与切入点的对应关系
 - 目标对象（Target）：被代理的原始对象称为目标对象
 ![AOP概念.png](https://s2.loli.net/2022/09/12/k4mAshndYLcJVb9.png)

```
  TODO待补充代码
```