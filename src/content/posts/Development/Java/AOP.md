---
title: AOP
published: 2024-12-27
description: 'Aspect-Oriented Programming'
image: ''
tags: ["Spring"]
category: 'Java'
draft: false 
lang: 'zh_CN'
---

## AOP

AOP 在 JAVA 中是通过 Spring 框架实现的面向切片编程，其主要任务是分离核心业务逻辑和事务的联系，使得开发者能够专心于核心业务逻辑的开发。

AOP 的实现方法就是通过对代理的 Java 类生成其对应的子类来实现对其的事务检查。

## 自定义实现 AOP

### 定义注解

```JAVA
@Target(METHOD)
@Retention(RUNTIME)
public @interface MetricTime {
    String value() default "0";
}
```

### 实现切片类

```JAVA
@Aspect
@Component
public class MetricAspect {
    @Around("@annotation(metricTime)")
    public Object metric(ProceedingJoinPoint pjp, MetricTime metricTime) throws Throwable {
        System.err.println("[Metrics] start " + pjp.getSignature());
        String name = metricTime.value();
        long start = System.currentTimeMillis();
        try {
            return pjp.proceed();
        } finally {
            long t = System.currentTimeMillis() - start;
            System.err.println("[Metrics] " + name + ": " + t + "ms");
        }
    }
}
```

注意，在 annotation 中的 metricTime 仅表示代理方法的参数，用于获取有关注解的信息。

### 使用注解

```java
@MetricTime(value = "login")
```

在使用注解的时候，注意对开启代理功能以及使用代理对方法进行调用。

```JAVA
@EnableAspectJAutoProxy(proxyTargetClass = true)
ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
UserService userService = (UserService) context.getBean(UserService.class);
User user = userService.login("bob@example.com", "password");
```

此外，在实现使用注解时，对应方法的类不可以是切片类，即不可以使用 @Aspect 进行修饰，需要仔细进行检查。

## AOP 使用注意事项

在使用 AOP 代理的时候，是直接生成了对应代理类的子类的字节码，而并没有调用对应的超类的构造函数。

所以对于代理类的变量无法直接通过子类对象进行访问，而需要通过对于的函数，函数一般会被子类进行覆写；注意，final 修饰的函数不会被覆写。
