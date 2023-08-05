# Spring
> Spring框架是一个开放源代码的J2EE应用程序框架，由Rod Johnson发起，是针对bean的生命周期进行管理的轻量级容器（lightweight container）。 Spring解决了开发者在J2EE开发中遇到的许多常见的问题，提供了功能强大IOC、AOP及Web MVC等功能。Spring可以单独应用于构筑应用程序，也可以和Struts、Webwork、Tapestry等众多Web框架组合使用，并且可以与 Swing等桌面应用程序AP组合。因此， Spring不仅仅能应用于J2EE应用程序之中，也可以应用于桌面应用程序以及小应用程序之中。Spring框架主要由七部分组成，分别是 Spring Core、 Spring AOP、 Spring ORM、 Spring DAO、Spring Context、 Spring Web和 Spring Web MVC。
> <p align="right"><a href="https://baike.baidu.com/item/spring/85061">——摘自百度百科</a></p>

[Spring官网](https://spring.io/)
# Spring 中的 Bean
&emsp;&emsp;在我个人的理解中，这里所谓的 Bean 就是在符合 Java Bean 规范的基础上由 Spring 管理的对象，这也是 Spring 的核心。
# IOC（控制反转）

&emsp;&emsp;控制反转，之前对象的控制权在类手上，现在反转后到了 Spring 手上。

# DI（依赖注入）

&emsp;&emsp;依赖注入可以理解为 IOC 的一种应用场景，反转的是对象间依赖关系的维护权。

例子：

&emsp;&emsp;现在有一个 UserServiceImpl 类，这个类实现了 UserService 接口。现在通过 Spring 获取到了 UserService 的对象。然后调用此对象的 userInfo 方法。userInfo 方法内需要调用 UserDAO 的对象去查询数据库，但此时 UserServiceImpl 的对象中还没有 UserDAO 的对象，于是程序报空指针异常。DI 正是要解决这样的问题。

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

```java
package com.zyh.lightquestionserver.aop;

import com.zyh.lightquestionserver.annotation.EncryptField;
import lombok.extern.slf4j.Slf4j;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Pointcut;
import org.jasypt.encryption.pbe.StandardPBEStringEncryptor;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import java.lang.reflect.Field;
import java.util.Objects;

@Slf4j
@Aspect
@Component
public class EncryptAspect {

    @Autowired
    private StandardPBEStringEncryptor standardPBEStringEncryptor;

    @Pointcut("@annotation(com.zyh.lightquestionserver.annotation.NeedEncrypt)")
    public void pointCut() {}                   //AOP切点

    @Around("pointCut()")                       //环绕通知
    public Object around(ProceedingJoinPoint joinPoint) throws Throwable {
        encrypt(joinPoint);
        return joinPoint.proceed();             //执行原方法
    }

    public void encrypt(ProceedingJoinPoint joinPoint)  {
        Object[] objects;
        try {
            objects = joinPoint.getArgs();
            if (objects.length != 0) {
                for (Object object : objects) {
                    encryptObject(object);
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * 加密对象
     * @param obj
     * @throws IllegalAccessException
     */
    private void encryptObject(Object obj) throws IllegalAccessException {

        if (Objects.isNull(obj)) {
            log.info("当前需要加密的object为null");
            return;
        }
        Field[] fields = obj.getClass().getDeclaredFields();
        for (Field field : fields) {
            //检测到当前是需要加密的字段
            boolean containEncryptField = field.isAnnotationPresent(EncryptField.class);
            //获取访问权
            field.setAccessible(true);
            Object ready = field.get(obj);
            //此字段不为null才加密
            if (containEncryptField && !Objects.isNull(ready)) {
                String value = standardPBEStringEncryptor.encrypt(String.valueOf(ready));
                field.set(obj, value);
            }
        }
    }

}

```