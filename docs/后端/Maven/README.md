# Maven
[Maven 公共仓库地址](https://mvnrepository.com/)

# 排除依赖
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
  <!-- 从SpringBoot中剔除jackson -->
  <exclusions>
      <exclusion>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-json</artifactId>
      </exclusion>
  </exclusions>
</dependency>
```

# 阻止传递依赖（配置可选依赖）
```xml
<dependency>
  <groupId>xxx</groupId>
  <artifactId>xxx</groupId>
  <version>xxx</version>
  <optional>true</optional>
</dependency>
```

# 归类依赖
```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.juven.mvnbook.account</groupId>
  <artifactId>accout-email</artifactId>
  <version>1.0.0-SNAPSHOT</version>
  <properties>
    <springframework.version>1.5.6</springframework.version>
  </properties>
  <dependencies>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>${springframework.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>${springframework.version}</version>
    </dependency>
  </dependencies>
</project>
```

# 生命周期
![生命周期](https://www.runoob.com/wp-content/uploads/2018/09/maven-package-build-phase.png)

|  阶段   |  处理   |  描述   |
|  ----   |  ----   |  ----   |
| 清理 clean | 清理 | 表示运行清理操作（会默认把 target 文件夹中的数据清理） |
| 验证 validate  | 验证项目 | 验证项目是否正确且所有必须信息是可用的 |
| 编译 compile  | 执行编译 | 源代码编译在此阶段完成 |
| 测试 Test     | 测试     | 使用适当的单元测试框架（例如 JUnit）运行测试 |
| 包装 package | 打包 | 创建 JAR/WAR 包如在 pom.xml 中定义提及的包 |
| 检查 verify | 检查 | 对集成测试的结果进行检查，以保证质量达标 |
| 安装 install | 安装 | 安装打包的项目到本地仓库，以供其他项目使用 |
| 部署 deploy | 部署 | 拷贝最终的工程包到远程仓库中，以共享给其他开发人员和工程 |
| 生成站点 site | 生成站点 | 生成项目相关信息的网站并且可以在浏览器中查看项目的站点 |

# 常用依赖
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
<!--		MySQL -->
    <dependency>
        <groupId>com.mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
        <scope>runtime</scope>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>

<!--		配置注解处理器-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-configuration-processor</artifactId>
        <optional>true</optional>
    </dependency>

<!--		连接池-->
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid-spring-boot-starter</artifactId>
        <version>1.1.16</version>
    </dependency>
<!--		MybatisPlus-->
    <dependency>
        <groupId>com.baomidou</groupId>
        <artifactId>mybatis-plus-boot-starter</artifactId>
        <version>3.5.2</version>
    </dependency>
<!--		MybatisPlusJoin-->
    <dependency>
        <groupId>com.github.yulichang</groupId>
        <artifactId>mybatis-plus-join-boot-starter</artifactId>
        <version>1.4.5</version>
    </dependency>
<!--		jackson 解析JSON-->
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
    </dependency>
<!--		fastjson 解析JSON-->
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>2.0.32</version>
    </dependency>
<!--		日志和@Data-->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
    </dependency>
<!--        redis-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-redis</artifactId>
    </dependency>
<!--        Json web token 用于验证-->
    <dependency>
        <groupId>io.jsonwebtoken</groupId>
        <artifactId>jjwt</artifactId>
        <version>0.9.1</version>
    </dependency>
<!--        阿里云短信服务-->
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>dysmsapi20170525</artifactId>
        <version>2.0.22</version>
    </dependency>
<!--        邮件服务-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-mail</artifactId>
    </dependency>
<!--        Thymeleaf 模版，用于发送模版邮件-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-thymeleaf</artifactId>
    </dependency>
<!--        加密的依赖-->
    <dependency>
        <groupId>com.github.ulisesbocchio</groupId>
        <artifactId>jasypt-spring-boot-starter</artifactId>
        <version>2.1.0</version>
    </dependency>
<!--        AOP-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-aop</artifactId>
    </dependency>
<!--        SpringBoot集成SpringSecurity -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.security</groupId>
        <artifactId>spring-security-test</artifactId>
        <scope>test</scope>
    </dependency>
<!--        SpringBoot集成rabbitmq-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-amqp</artifactId>
    </dependency>
</dependencies>
```