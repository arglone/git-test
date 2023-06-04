> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/hancoder/article/details/109063671)

写在前面

*   官方代码地址：https://github.com/zzyybs/atguigu_spirngcloud2020
*   本文地址：https://blog.csdn.net/hancoder/article/details/109063671
*   本文下载方式：见博客中谷粒商城的下载方式（记得备注是 cloud 笔记，否则默认发的是谷粒的笔记）

集中什么是微服务架构：

![](https://img-blog.csdnimg.cn/img_convert/cd4957eee96b1eb47276c47f88111fab.png)

SpringCloud 是微服务一站式服务解决方案，微服务全家桶。它是微服务开发的主流技术栈。它采用了名称，而非数字版本号。

SpringCloud 和 springCloud Alibaba 目前是最主流的微服务框架组合。

版本选择：

> 选用 springboot 和 springCloud 版本有约束，不按照它的约束会有冲突。

### 版本问题

本次学习的各种软件的版本：

*   boot 使用的是数字作为版本。官网强烈建议升级到 2.0 以上
*   cloud 使用的是字母作为版本，伦敦地铁站站名

<table><thead><tr><th align="left">Cloud Release Train</th><th align="left">Boot Version</th></tr></thead><tbody><tr><td align="left"><a href="https://github.com/spring-projects/spring-cloud/wiki/Spring-Cloud-Hoxton-Release-Notes">Hoxton</a></td><td align="left">2.2.x, 2.3.x (Starting with SR5)</td></tr><tr><td align="left"><a href="https://github.com/spring-projects/spring-cloud/wiki/Spring-Cloud-Greenwich-Release-Notes">Greenwich</a></td><td align="left">2.1.x</td></tr><tr><td align="left"><a href="https://github.com/spring-projects/spring-cloud/wiki/Spring-Cloud-Finchley-Release-Notes">Finchley</a></td><td align="left">2.0.x</td></tr><tr><td align="left"><a href="https://github.com/spring-projects/spring-cloud/wiki/Spring-Cloud-Edgware-Release-Notes">Edgware</a></td><td align="left">1.5.x</td></tr><tr><td align="left"><a href="https://github.com/spring-projects/spring-cloud/wiki/Spring-Cloud-Dalston-Release-Notes">Dalston</a></td><td align="left">1.5.x</td></tr></tbody></table>

查看版本对应关系：https://start.spring.io/actuator/info

```
"spring-cloud": {
    "Finchley.M2": "Spring Boot >=2.0.0.M3 and <2.0.0.M5",
    "Finchley.M3": "Spring Boot >=2.0.0.M5 and <=2.0.0.M5",
    "Finchley.M4": "Spring Boot >=2.0.0.M6 and <=2.0.0.M6",
    "Finchley.M5": "Spring Boot >=2.0.0.M7 and <=2.0.0.M7",
    "Finchley.M6": "Spring Boot >=2.0.0.RC1 and <=2.0.0.RC1",
    "Finchley.M7": "Spring Boot >=2.0.0.RC2 and <=2.0.0.RC2",
    "Finchley.M9": "Spring Boot >=2.0.0.RELEASE and <=2.0.0.RELEASE",
    "Finchley.RC1": "Spring Boot >=2.0.1.RELEASE and <2.0.2.RELEASE",
    "Finchley.RC2": "Spring Boot >=2.0.2.RELEASE and <2.0.3.RELEASE",
    "Finchley.SR4": "Spring Boot >=2.0.3.RELEASE and <2.0.999.BUILD-SNAPSHOT",
    "Finchley.BUILD-SNAPSHOT": "Spring Boot >=2.0.999.BUILD-SNAPSHOT and <2.1.0.M3",
    "Greenwich.M1": "Spring Boot >=2.1.0.M3 and <2.1.0.RELEASE",
    "Greenwich.SR6": "Spring Boot >=2.1.0.RELEASE and <2.1.18.BUILD-SNAPSHOT",
    "Greenwich.BUILD-SNAPSHOT": "Spring Boot >=2.1.18.BUILD-SNAPSHOT and <2.2.0.M4",
    "Hoxton.SR8": "Spring Boot >=2.2.0.M4 and <2.3.5.BUILD-SNAPSHOT",
    "Hoxton.BUILD-SNAPSHOT": "Spring Boot >=2.3.5.BUILD-SNAPSHOT and <2.4.0.M1",
    "2020.0.0-M3": "Spring Boot >=2.4.0.M1 and <=2.4.0.M1",
    "2020.0.0-SNAPSHOT": "Spring Boot >=2.4.0.M2"
},

```

尚硅谷阳哥教程版本：

<table><thead><tr><th></th><th></th></tr></thead><tbody><tr><td>cloud</td><td>Hoxton.SR1</td></tr><tr><td>boot</td><td>2.2.2.RELEASE</td></tr><tr><td>cloud alibaba</td><td>2.1.0.RELEASE</td></tr><tr><td>java</td><td>java8</td></tr><tr><td>maven</td><td>3.5 及以上</td></tr><tr><td>mysql</td><td>5.7 及以上</td></tr></tbody></table>

cloud 版本决定了 boot 版本

#### 微服务停更说明

1,Eureka 停用, 可以使用 zk 作为服务注册中心

2, 服务调用, Ribbon 准备停更, 代替为 LoadBalance

3,Feign 改为 OpenFeign

4,Hystrix 停更, 改为 resilence4j

​ 或者阿里巴巴的 sentienl

5.Zuul 改为 gateway

6, 服务配置 Config 改为 Nacos

7, 服务总线 Bus 改为 Nacos

![](https://img-blog.csdnimg.cn/img_convert/0665bd7da429fdb4c32683d44175999e.png)

Cloud 简介
--------

参考资料，尽量去官网

https://cloud.spring.io/spring-cloud-static/Hoxton.SR1/reference/htmlsingle/

工程建造
====

写一个下图的 Hello World

![](https://img-blog.csdnimg.cn/img_convert/ccb7be6d952b97faef635efc5b736929.png)

构建父工程，后面的项目模块都在此工程中：

![](https://img-blog.csdnimg.cn/img_convert/efded375e5b85fa7d08d6867d1f82660.png)

设置编码：Settings -> File Encodings

注解激活：

![](https://img-blog.csdnimg.cn/img_convert/b7491135be83c1053747fd7806d4dc9c.png)

Java 版本确定：

![](https://img-blog.csdnimg.cn/img_convert/a3b6ab1f1ce38fa1f4fda834cfd1121a.png)

父工程 pom 配置
----------

```
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.dkf.cloud</groupId>
    <artifactId>cloud2020</artifactId>
    <version>1.0-SNAPSHOT</version>
    <!-- 第一步 打包方式pom-->
    <packaging>pom</packaging>

    <!-- 统一管理 jar 包版本 -->
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
        <junit.version>4.12</junit.version>
        <log4j.version>1.2.17</log4j.version>
        <lombok.version>1.16.18</lombok.version>
        <mysql.version>5.1.47</mysql.version>
        <druid.version>1.1.16</druid.version>
        <mybatis.spring.boot.version>1.3.0</mybatis.spring.boot.version>
    </properties>

    <!-- 子块基础之后，提供作用：锁定版本 + 子module不用写 groupId 和 version -->
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-project-info-reports-plugin</artifactId>
                <version>3.0.0</version>
            </dependency>

            <!-- 下面三个基本是微服务架构的标配 -->
            <!--spring boot 2.2.2-->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.2.2.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <!--spring cloud Hoxton.SR1-->
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>Hoxton.SR1</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <!--spring cloud 阿里巴巴-->
            <dependency>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>2.1.0.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>

            <!--mysql-->
            <dependency>
                <groupId>mysql</groupId>
                <artifactId>mysql-connector-java</artifactId>
                <version>${mysql.version}</version>
                <scope>runtime</scope>
            </dependency>
            <!-- druid-->
            <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>druid</artifactId>
                <version>${druid.version}</version>
            </dependency>
            <dependency>
                <groupId>org.mybatis.spring.boot</groupId>
                <artifactId>mybatis-spring-boot-starter</artifactId>
                <version>${mybatis.spring.boot.version}</version>
            </dependency>
            <!--junit-->
            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>${junit.version}</version>
            </dependency>
            <!--log4j-->
            <dependency>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
                <version>${log4j.version}</version>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <fork>true</fork>
                    <addResources>true</addResources>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>

```

上面配置的解释：

> 首先要加 `<packaging>pom</packaging>` 这个。
> 
> 为了让项目顺利的运行，我们必须使用统一的版本号；  
> **1、dependencyManagement**  
> (1) 在我们项目中，我们会发现在父模块的 pom 文件中常常会出现 dependencyManagement 元素，这是因为我们可以通过其来管理子模块的版本号，也就是说我们在父模块中**声明号依赖的版本，但是并不实现引入**；  
> **2、dependencies**  
> (1) 上面说到 dependencyManagement 只是声明一个依赖，而不实现引入，故我们在子模块中也需要对依赖进行声明，倘若不声明子模块自己的依赖，是不会从父模块中继承的；只有子模块中也声明了依赖。并且没有写对应的版本号它才会从父类中继承；并且 version 和 scope 都是取自父类；此外要是子模块中自己定义了自己的版本号，是不会继承自父类的。  
> **3、总结**  
> dependencyManagement 只是用来管理依赖，规定未添加版本号的子模块依赖继承自它，dependencies 是用来声明子模块自己的依赖，可以在其中来写自己需要的版本号
> 
> 聚合版本依赖，dependencyManagement 只声明依赖，并不实现引入，所以子项目还需要写要引入的依赖。

可以统一版本

父工程创建完成执行 mvn:install 将父工程发布到仓库方便子工程继承

第一个微服务架构
--------

创建一个 module 后 (只能改 a)，在父工程的 pom 里多了个`<modules>`，

在模块的 pom 里没有 gv，只有 a。

模块里的`<dependencies>`里的依赖只有 ga，没有 v

### 提供者

cloud-provider-payment8001 子工程的 pom 文件：

> 这里面的 lombok 这个包，引入以后，实体类不用再写 set 和 get
> 
> 可以如下写实体类：
> 
> ```
> import lombok.AllArgsConstructor;
> import lombok.Data;
> import lombok.NoArgsConstructor;
> import java.io.Serializable;
> 
> @Data
> @AllArgsConstructor
> @NoArgsConstructor
> public class Payment implements Serializable {
>   private Integer id;
>   private String serial;
> }
> 
> ```

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>cloud2020</artifactId>
        <groupId>com.dkf.cloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-provider-payment8001</artifactId>
    <dependencies>
        <!--eureka-client-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <!--这个和web要写到一块-->
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <!--mysql-connector-java-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
        <!--jdbc-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>

```

cloud-provider-payment8001 子工程的 yml 文件：

```
server:
  port: 8001

spring:
  application:
    name: cloud-provider-payment8001
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource
    driver-class-name: org.gjt.mm.mysql.Driver
    url: jdbc:mysql://localhost:3306/cloud2020?useUnicode=true&characterEncoding=utf-8&useSSL=false
    username: root
    password: 123456
mybatis:
  mapper-locations: classpath:mapper/*.xml
  type-aliases-package: com.dkf.springcloud.entities  # 所有Entity 别名类所在包

```

cloud-provider-payment8001 子工程的主启动类：

```
package com.dkf.springcloud;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class PaymentMain8001 {
    public static void main(String[] args){
        SpringApplication.run(PaymentMain8001.class, args);
    }
}

```

下面的常规操作：

*   ①建表 SQL
    
    ```
    create table `payment`(
        `id` bigint(20) not null auto_increment comment 'ID',
        `serial` varchar(200) default '',
        PRIMARY KEY (`id`)
    
    )ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8
    
    select * from payment;
    
    ```
    

##### entities

```
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.io.Serializable;

@Data   //set/get方法
@AllArgsConstructor //有参构造器
@NoArgsConstructor  //无参构造器
public class Payment implements Serializable {
  private long id;//数据库是bigint
  private String serial;
}

```

```
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

//返回给前端的通用json数据串
@Data   //set/get方法
@AllArgsConstructor //有参构造器
@NoArgsConstructor  //无参构造器
public class CommonResult<T> {
  private Integer code;
  private String message;
  private T data; //泛型，对应类型的json数据

  //自定义两个参数的构造方法
  public CommonResult(Integer code, String message){
      this(code, message, null);
  }
}

```

##### dao

```
@Mapper // 是ibatis下面的注解 //@Repositoty有时候会有问题
public interface PaymentDao {
  
  int create(Payment payment);

  Payment getPaymentById(@Param("id") Long id);
}

```

resource 下创建 mapper 文件夹，新建 PaymentMapper.xml。在 yml 里有所有 entity 别名类所在包，所有 payment 不用写全类名

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="com.xzq.springcloud.dao.PaymentDao">
  <resultMap id="BaseResultMap" type="com.xzq.springcloud.entities.Payment">
      <id column="id" property="id" jdbcType="BIGINT"/>
      <id column="serial" property="serial" jdbcType="VARCHAR"/>
  </resultMap>

  <insert id="create" parameterType="Payment" useGeneratedKeys="true" keyProperty="id">
      insert into payment(serial) values (#{serial})
  </insert>

  <select id="getPaymentById" parameterType="Long" resultMap="BaseResultMap">
      select * from payment where id = #{id}
  </select>
</mapper>

```

@Param 注解：https://blog.csdn.net/qq_39505065/article/details/90550705

##### service

```
public interface PaymentService {
  int create(Payment payment);

  Payment getPaymentById(@Param("id") Long id);
}

```

```
@Service
public class PaymentServiceImpl implements PaymentService {

  @Autowired
  private PaymentDao paymentDao;

  @Override
  public int create(Payment payment) {
      return paymentDao.create(payment);
  }

  @Override
  public Payment getPaymentById(Long id) {
      return paymentDao.getPaymentById(id);
  }
}

```

##### controller

```
@RestController   //必须是这个注解，因为是模拟前后端分离的restful风格的请求，要求每个方法返回 json
@Slf4j
public class PaymentController {

  @Resource
  private PaymentService paymentService;

  @PostMapping(value = "/payment/create")
  //	    注意这里的 @RequestBody  是必须要写的，虽然 MVC可以自动封装参数成为对象，
  //      但是当消费者项目调用，它传参是 payment 整个实例对象传过来的， 即Json数据，因此需要写这个注解
  // https://blog.csdn.net/weixin_38004638/article/details/99655322
  public CommonResult create(@RequestBody Payment payment){
      int result = paymentService.create(payment);
      log.info("****插入结果：" + result);
      if(result > 0){
          return new CommonResult(200, "插入数据库成功", result);
      }
      return new CommonResult(444, "插入数据库失败", null);
  }

  @GetMapping(value = "/payment/{id}")
  public CommonResult getPaymentById(@PathVariable("id")Long id){
      Payment result = paymentService.getPaymentById(id);
      log.info("****查询结果：" + result);
      if(result != null){
          return new CommonResult(200, "查询成功", result);
      }
      return new CommonResult(444, "没有对应id的记录", null);
  }
}

```

对应 POST 方式的请求，要学会用`POSTMAN`工具

微服务多了之后就使用 run dashboard

不但编译有个别地方会报错，启动也会报错，但是测试两个接口都是没问题的，推测启动报错是因为引入了下面才会引入的 jar 包，目前不影响。

### 热部署配置 devtools

代码改动后希望自动生效

1.  具体模块里添加 Jar 包到工程中，上面的 pom 文件已经添加上了

```
<dependency>    
    <groupId>org.springframework.boot</groupId>    
    <artifactId>spring-boot-devtools</artifactId>    
    <scope>runtime</scope>    
    <optional>true</optional>
</dependency>

```

2.  添加 plugin 到父工程的 pom 文件中：上面也已经添加好了

```
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <fork>true</fork>
                <addResources>true</addResources>
            </configuration>
        </plugin>
    </plugins>
</build>

```

3.  ![](https://img-blog.csdnimg.cn/img_convert/c404c28eb0f6fa9cf728f42a86cd55c5.png)
    
4.  shift + ctrl + alt + / 四个按键一块按，选择 Reg 项：
    

![](https://img-blog.csdnimg.cn/img_convert/2b0cb48b2baf37d8bf7fc59986ad4def.png)

重启 IDEA

热部署只允许在开发阶段使用

### 消费者

新建模块 cloud-consumer-order80

> 消费者现在只模拟调用提供者的 Controller 方法，没有持久层配置，只有 Controller 和实体类
> 
> 当然也要配置主启动类和启动端口

pom 文件：

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>cloud2020</artifactId>
        <groupId>com.dkf.cloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-customer-order80</artifactId>

    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <!--<dependency><!– 引入自己定义的api通用包，可以使用Payment支付Entity –>-->
        <!--<groupId>com.atguigu.springcloud</groupId>-->
        <!--<artifactId>cloud-api-commons</artifactId>-->
        <!--<version>${project.version}</version>-->
        <!--</dependency>-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>

```

把 CommonResult 和 Payment 两个 实体类也创建出来

*   config/ApplicationContextCOnfig.java
*   controller/OrderController.java
*   entities/CommonResult.java
*   entities/Payment.java
*   OrderMain80.java

application.yml

```
server:
	port:80 # 80端口就可以省略了

```

OrderMain80.java

```
@SpringbootApplication
public class OrderMain80{
    public static void main(String[] args){
        SpringApplication.run(OrderMain80.class,args);
    }
}

```

entites 包中的类也拷贝到本项目中

*   entities/CommonResult.java
*   entities/Payment.java

##### 配置 RestTemplate

ApplicationContextConfig 内容：

```
package com.dkf.springcloud.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.client.RestTemplate;//网络客户端

@Configuration
public class ApplicationContextConfig {

    @Bean
    public RestTemplate getRestTemplate(){
        return new RestTemplate();
        /*
        RestTemplate提供了多种便捷访问远程http服务的方法，
        是一种简单便捷的访问restful服务模板类，是spring提供的用于rest服务的客户端模板工具集
        */
    }
}

```

##### Controller

```
@RestController
@Slf4j
public class OrderController {

    //远程调用的 地址
    public static final String PAYMENY_URL = "http://localhost:8001";

    @Resource
    private RestTemplate restTemplate;

    @PostMapping("customer/payment/create")
    public CommonResult<Payment> create (Payment payment){

        return restTemplate.postForObject(PAYMENY_URL + "/payment/create",//请求地址
                                          payment,//请求参数
                                          CommonResult.class);//返回类型
    }

    @GetMapping("customer/payment/{id}")
    public CommonResult<Payment> getPaymentById(@PathVariable("id")Long id){
        return restTemplate.getForObject(PAYMENY_URL + "/payment/" + id,//请求地址
                                         CommonResult.class);//返回类型
    }
}

```

如果 runDashboard 控制台没有出来，右上角搜索 即可

运用 spring cloud 框架基于 spring boot 构建微服务，一般需要启动多个应用程序，在 idea 开发工具中，多个同时启动的应用

需要在 RunDashboard 运行仪表盘中可以更好的管理，但有时候 idea 中的 RunDashboard 窗口没有显示出来，也找不到直接的开启按钮

idea 中打开 Run Dashboard 的方法如下

view > Tool Windows > Run Dashboard

如果上述列表找不到 Run Dashboard, 则可以在工程目录下找到. idea 文件夹下的 workspace.xml，在其中相应位置加入以下代码（替换）即可：

```
<component >
    <option >
        <set>
            <option value="SpringBootApplicationConfigurationType"/>
        </set>
    </option>
    <option >
        <list>
            <RuleState>
                <option />
            </RuleState>
            <RuleState>
                <option />
            </RuleState>
        </list>
    </option>
</component>

```

### 工程重构

> 上面 两个子项目，有多次重复的 导入 jar，和重复的 Entity 实体类。可以把 多余的部分，加入到一个独立的模块中，将这个模块打包，并提供给需要使用的 module

1.  新建一个 cloud-api-commons 子模块
2.  将 entities 包里面的实体类放到这个子模块中，也将 pom 文件中，重复导入的 jar 包放到这个新建的 模块的 pom 文件中。如下：

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>cloud2020</artifactId>
        <groupId>com.dkf.cloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-api-commons</artifactId>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>

        <!-- 这个是新添加的，之前没用到，后面会用到。关于这个hutool 是个功能强大的工具包，官网：https://hutool.cn/ -->
        <dependency>
            <groupId>cn.hutool</groupId>
            <artifactId>hutool-all</artifactId>
            <version>5.1.0</version>
        </dependency>
    </dependencies>

</project>

```

mvn 跳过 test，mvc clean，mvn install

将此项目打包 install 到 maven 仓库。

3.  将 提供者 和 消费者 两个项目中的 entities 包删除，并删除掉加入到 cloud-api-commons 模块的 依赖配置。
4.  将 打包到 maven 仓库的 cloud-api-commons 模块，引入到 提供者 和 消费者的 pom 文件中，如下所示

```
<dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
    <groupId>com.dkf.cloud</groupId>
    <artifactId>cloud-api-commons</artifactId>
    <version>${project.version}</version>
</dependency>

```

服务注册中心
======

> 如果是上面只有两个微服务，通过 RestTemplate ，是可以相互调用的，但是当微服务项目的数量增大，就需要服务注册中心。目前没有学习服务调用相关技术，使用 SpringCloud 自带的 RestTemplate 来实现 RPC

![](https://img-blog.csdnimg.cn/img_convert/0665bd7da429fdb4c32683d44175999e.png)

Eureka
------

**什么是服务治理**：

SpringCloud 封装了 Netflix 公司开发的 Eureka 模块来实现服务治理

在传统的 rpc 远程调用框架中，管理每个服务与服务之间依赖关系比较复杂，管理比较复杂，所以需要使用服务治理，管理服务于服务之间依赖关系，可以实现服务调用、负载均衡、容错等，实现服务发现与注册。

**什么是服务注册与发现**：

Eureka 采用了 CS 的设计结构，Eureka Server 服务注册功能的服务器，它是服务注册中心。而系统中的其他微服务，使用 Eureka 的客户端连接到 Eureka Server 并维持心跳连接。这样系统的维护人员就可以通过 Eureka Server 来监控系统中各个微服务是否正常运行。这点和 zookeeper 很相似

在服务注册与发现中，有一个注册中心。当服务器启动时候，会把当前自己服务器的信息 比如服务地址 通讯地址等以别名方式注册到注册中心上。另一方（消费者服务提供者），以该别名的方式去注册中心上获取到实际的服务通讯地址，然后再实现本地 RPC 调用。RPC 远程调用框架核心设计思想：在于注册中心，因为便用注册中心管理每个服务与服务之间的一个依赖关系（服务治理概念)。在任何 rpc 远程框架中，都会有一个注册中心（存放服务地址相关信息（接口地址））

![](https://img-blog.csdnimg.cn/img_convert/8da648937c52bff1a3690b6520c3f540.png)

> Eureka 官方停更不停用，以后可能用的越来越少。
> 
> [Eureka](https://github.com/Netflix/Eureka) 是 [Netflix](https://github.com/Netflix) 开发的，一个基于 REST 服务的，服务注册与发现的组件，以实现中间层服务器的负载平衡和故障转移。
> 
> Eureka 分为 Eureka Server 和 Eureka Client 及服务端和客户端。**Eureka Server 为注册中心，是服务端，而服务提供者和消费者即为客户端，消费者也可以是服务者，服务者也可以是消费者**。同时 Eureka Server 在启动时默认会注册自己，成为一个服务，所以 Eureka Server 也是一个客户端，这是搭建 Eureka 集群的基础。
> 
> *   Eureka Client：一个 Java 客户端，用于简化与 Eureka Server 的交互（通常就是微服务中的客户端和服务端）。通过注册中心进行访问。是一个 Java 客户端，用于简化 Eureka Server 的交互，客户端同时也具备一个内置的、使用轮询（roundrobin）负载算氵去的负载均衡器  
>     在应用启动后，将会向 Eureka Server 发送心跳（默认周期为 30 秒）。如果 Eureka Server 在多个心跳周期内没有接收到某个节点的心跳，Eureka Server 将会从服务注册表中把这个服务节点移除（默认 90 秒）
> *   Eureka Server：提供服务注册服务，各个微服务节，通过配置启动后，会在 Eureka Serverc 中进行注册，这样 Eureka Server 中的服务注册表中将会存储所有可用服务节点信息，服务节点的信息可以在界面中直观看到。
> 
> 服务在 Eureka 上注册，然后每隔 30 秒发送心跳来更新它们的租约。如果客户端不能多次续订租约，那么它将在大约 90 秒内从服务器注册表中剔除。注册信息和更新被复制到集群中的所有 eureka 节点。来自任何区域的客户端都可以查找注册表信息（每 30 秒发生一次）来定位它们的服务（可能在任何区域）并进行远程调用
> 
> 服务**提供者**向注册中心注册服务，并**每隔 30 秒发送一次心跳**，就如同人还活着存在的信号一样，如果 Eureka 在 90 秒后还未收到服务提供者发来的心跳时，那么它就会认定该服务已经死亡就会注销这个服务。这里注销并不是立即注销，而是会在 60 秒以后对在这个之间段内 “死亡” 的服务集中注销，如果立即注销，势必会对 Eureka 造成极大的负担。这些时间参数都可以人为配置。
> 
> Eureka 还有自我保护机制，如果在 15 分钟内超过 85% 的节点都没有正常的心跳，那么 Eureka 就认为客户端与注册中心出现了网络故障，所以不会再接收心跳，也不会删除服务。
> 
> 客户端消费者会向注册中心拉取服务列表，因为一个服务器的承载量是有限的，所以同一个服务会部署在多个服务器上，每个服务器上的服务都会去注册中心注册服务，他们会有相同的服务名称但有不同的实例 id，所以**拉取的是服务列表**。我们最终通过负载均衡来获取一个服务，这样可以均衡各个服务器上的服务。

![](https://img-blog.csdnimg.cn/20190816202635152.png)

### 单机版 Eureka 构建：

消费者端口 80，提供者端口 8001。

Eureka 端口 7001

#### 1) Server 模块

pom

版本说明：

```
<!--新版本2020.02-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>


<!--旧版本2018-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-eureka</artifactId>
</dependency>

```

```
	<artifactId>cloud-eureka-server7001</artifactId>

<dependencies>
  <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
  </dependency>
    
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-actuator</artifactId>
  </dependency>
  <dependency>
      <groupId>org.mybatis.spring.boot</groupId>
      <artifactId>mybatis-spring-boot-starter</artifactId>
  </dependency>
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-devtools</artifactId>
      <scope>runtime</scope>
      <optional>true</optional>
  </dependency>
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-test</artifactId>
      <scope>test</scope>
  </dependency>
  <dependency>
      <groupId>com.dkf.cloud</groupId>
      <artifactId>cloud-api-commons</artifactId>
      <version>${project.version}</version>
  </dependency>
</dependencies>

```

application.yml

```
server:
	port: 7001

eureka:
	instance:
		hostname: localhost  # eureka 服务端的实例名称

	client:
		# false 代表不向服务注册中心注册自己，因为它本身就是服务中心
		register-with-eureka: false
		# false 代表自己就是服务注册中心，自己的作用就是维护服务实例，并不需要去检索服务
		fetch-registry: false
		service-url:
			# 设置与 Eureka Server 交互的地址，查询服务 和 注册服务都依赖这个地址
			defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/

```

###### `@EnableEurekaServer`

最后写主启动类，如果启动报错，说没有配置 DataSource ，就在 主启动类的注解加上 这样的配置：

```
// exclude ：启动时不启用 DataSource的自动配置检查
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)
@EnableEurekaServer   // 表示它是服务注册中心
public class EurekaServerMain7001 {
    public static void main(String[] args){
        SpringApplication.run(EurekaServerMain7001.class, args);
    }
}

```

启动测试，访问 7001 端口

#### 2) 提供者

> 这里的提供者，还是使用 上面的 cloud-provider-payment8001 模块，做如下修改：

1.  在 pom 文件的基础上引入 eureka 的 client 包，pom 的全部依赖如下所示：

```
<artifactId>cloud-provider-payment8001</artifactId>
<dependencies>
    <!--eureka-client-->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter</artifactId>
    </dependency>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid-spring-boot-starter</artifactId>
        <version>1.1.10</version>
    </dependency>
    <!--mysql-connector-java-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
    </dependency>
    <!--jdbc-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-jdbc</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>com.dkf.cloud</groupId>
        <artifactId>cloud-api-commons</artifactId>
        <version>${project.version}</version>
    </dependency>
</dependencies>

```

###### `@EnableEurekaClient`

2.  主启动类 加上注解 ：`@EnableEurekaClient`
3.  yml 文件添加关于 Eureka 的配置：

```
spring:
  application:
    name: cloud-payment-service # 项目名,也是注册的名字

eureka:
  client:
	# 注册进 Eureka 的服务中心
    register-with-eureka: true
    # 检索 服务中心 的其它服务
    fetch-registry: true
    service-url:
      # 设置与 Eureka Server 交互的地址
      defaultZone: http://localhost:7001/eureka/

```

#### 3) 消费者

> 这里的消费者 也是上面 的 cloud-customer-order80 模块

1.  修改 pom 文件，加入 Eureka 的有关依赖， 全部 pom 依赖如下：

```
<artifactId>cloud-customer-order80</artifactId>

<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>
    <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <groupId>com.dkf.cloud</groupId>
        <artifactId>cloud-api-commons</artifactId>
        <version>${project.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>

```

###### `@EnableEurekaClient`

2.  主启动类 加上注解 ： @EnableEurekaClient
3.  yml 文件必须添加的内容：

```
eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://localhost:7001/eureka/
spring:
  application:
    name: cloud-order-service

```

### Eureka 集群 700X

*   1 先启动 eureka 注册中心
*   2 启动服务提供者 payment 支付服务
*   3 支付服务启动后会把自身信息化 服务以别名方式注册进 eureka
*   4 消费者 order 服务在要调用接囗时，**使用服务别名去注册中心取实际的 RPC 远程调用地址**
*   5 **消费者获得调用地址后，底层实际是利用`HttpClient`技术实现远程调用**
*   6 **消费者获得服务地址后会存`jvm内存`中，默认每间隔 30s 更新一次服务调用地址**

Eureka Server 在设计的时候就考虑了高可用设计，在 Eureka 服务治理设计中，**所有节点既是服务的提供方，也是服务的消费方**，服务注册中心也不例外。

Eureka Server 的高可用实际上就是将自己做为服务向其他服务注册中心注册自己，这样就可以形成一组互相注册的服务注册中心，以实现服务清单的互相同步，达到高可用的效果。

Eureka Server 的同步遵循着一个非常简单的原则：只要有一条边将节点连接，就可以进行信息传播与同步。可以采用两两注册的方式实现集群中节点完全对等的效果，实现最高可用性集群，任何一台注册中心故障都不会影响服务的注册与发现。

问题：微服务 RPC 远程服务调用最核心的是什么：

高可用，试想你的注册中心只有一个。onlyone, 它出故障了那就呵呵了，会导致整个为服务环境不可用，所以要搭建 Eureka 注册中心集群，实现负载均衡 + 故障容错

Eureka 集群的原理：相互注册，互相守望。每台 Eureka 服务器都有集群里其他 Eureka 服务器地址的信息

开始构建 Eureka 集群：

现在创建 cloud-eureka-server7002 ，也就是第二个 Eureka 服务注册中心，pom 文件和 主启动类，与第一个 Server 一致。

> 模拟多个 为了不用输出 C:\Windows\System32\drivers\etc\hosts 添加如下：
> 
> 127.0.0.1 eureka7001.com
> 
> 127.0.0.1 eureka7002.com

现在修改这两个 Server 的 yml 配置：

7001 端口的 Server yml 文件：

```
server:
  port: 7001

eureka:
  instance:
    hostname: eureka7001.com  # eureka 服务器的实例地址

  client:
    register-with-eureka: false
    fetch-registry: false
    service-url:
    ## 一定要注意这里的地址，这是搭建集群的关键。反过来写，写的是集群中其他Eureka服务器的地址
      defaultZone: http://eureka7002.com:7002/eureka/

```

7002 端口的 Server yml 文件：

```
server:
  port: 7002

eureka:
  instance:
    hostname: eureka7002.com  # eureka 服务器的实例地址

  client:
    register-with-eureka: false
    fetch-registry: false
    service-url:
    ## 一定要注意这里的地址 这是搭建集群的关键
      defaultZone: http://eureka7001.com:7001/eureka/

```

> eureka.instance.hostname 才是启动以后 本 Server 的注册地址，而 service-url 是 map 类型，只要保证 key:value 格式就行，它代表 本 Server 指向了那些 其它 Server 。利用这个，就可以实现 Eureka Server 相互之间的注册，从而实现集群的搭建。

### 提供者集群 800X

上面配置了多个 Eureka 作为集群，接下来要配置的是提供者集群，让提供者高可用

为提供者`cloud-provider-payment8001` 模块创建集群，新建模块名为 `cloud-provider-payment8002`

即两个提供者 8001 和 8002

其余配置都一致，需要配置集群的配置如下：

配置区别要点：

*   集群中多个提供者的`spring:application:name:`要一致
*   启动类添加`@EnableDiscoveryClient`或者`@EnableEurekaClient`  
    1，`@EnableDiscoveryClient`注解是基于`spring-cloud-commons`依赖，并且在 classpath 中实现；  
    2，`@EnableEurekaClient`注解是基于`spring-cloud-netflix`依赖，只能为 eureka 作用；  
    如果你的 classpath 中添加了 eureka，则它们的作用是一样的。

> 消费者（一般需要连接其他微服务的服务或者 gateway/zuul）

```
# 提供者
server:
  port: 8001  # 端口号不一样

spring:
  application:
    name: cloud-provider-service  # 这次重点是这里，两个要写的一样，这是这个集群的关键
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource
    driver-class-name: org.gjt.mm.mysql.Driver
    url: jdbc:mysql://localhost:3306/cloud2020?useUnicode=true&characterEncoding=utf-8&useSSL=false
    username: root
    password: 123456

mybatis:
  mapper-locations: classpath:mapper/*.xml
  type-aliases-package: com.dkf.springcloud.entities  

eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url: # 提供者注册到多个eureka中
      defaultZone: http://eureka7001.com:7001/eureka/,http://eureka7002.com:7002/eureka/

```

注意在 Controller 返回不同的消息，从而区分者两个提供者的工作状态。（只是为了学习测试才这么做，生产环境直接复制即可）

在提供者的 controller 中

```
@Value("${server.port}")
private String serverPort;

```

##### 消费者 80

此时消费者一旦消费完之后，他以后访问的还是那台提供者。明显不对，原因在于消费者并没有去 Rureka 里找服务，而是自己找的

> 就是消费者如何访问 由这两个提供者组成的集群？

Eureka Server 上的提供者的服务名称如下：

```
@RestController
@Slf4j
public class OrderController {
    
    // 重点是这里，改成 提供者在Eureka 上的名称，而且无需写端口号	
    public static final String PAYMENY_URL = "http://CLOUD-PROVIDER-SERVICE";//取决于我们在提供者出配置的name，CLOUD-PAYMENY-SERVICE，//同时要注意使用@LoadBalanced注解赋予RestTemplate负载均衡能力

    @Resource
    private RestTemplate restTemplate;

    @PostMapping("customer/payment/create")
    public CommonResult<Payment> create (Payment payment){
        return restTemplate.postForObject(PAYMENY_URL + "/payment/create", payment, CommonResult.class);
    }

    @GetMapping("customer/payment/{id}")
    public CommonResult<Payment> getPaymentById(@PathVariable("id")Long id){
        return restTemplate.getForObject(PAYMENY_URL + "/payment/" + id, CommonResult.class);
    }
}

```

```
server:
  port: 80

spring:
    application:
        name: cloud-order-service
    zipkin:
      base-url: http://localhost:9411
    sleuth:
      sampler:
        probability: 1

eureka:
  client:
    #表示是否将自己注册进EurekaServer默认为true。
    register-with-eureka: false
    #是否从EurekaServer抓取已有的注册信息，默认为true。单节点无所谓，集群必须设置为true才能配合ribbon使用负载均衡
    fetchRegistry: true
    service-url:
      #单机
      #defaultZone: http://localhost:7001/eureka
      # 集群
      defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka  # 集群版

```

##### `@LoadBalanced`

还有，消费者里面对 RestTemplate 配置的 config 文件，需要更改成如下：（就是加一个注解 `@LoadBalanced`）

```
@Configuration
public class ApplicationContextConfig {

    @Bean
    @LoadBalanced  //这个注解，就赋予了RestTemplate 负载均衡的能力
    public RestTemplate getRestTemplate(){
        return new RestTemplate();
    }
}

```

这时候，消费者消费的提供者多次访问就会变化了（这就是 Ribbon 的负载平衡功能）

### actuator 让 Eureka 显示 ip

为了在微服务 Eureka 控制台能看到我们的某个具体服务是在哪台服务器上部署的，我们需要配置一些内容。

修改 提供者在 Eureka 注册中心显示的 主机名：即修改`eureka:instance:instance-id:`和`eureka:instance:prefer-ip-address:`

```
# 提供者
server:
  port: 8001  # 端口号不一样

eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/,http://eureka7002.com:7002/eureka/
  instance: #重点，和client平行
    instance-id: payment8001 # 每个提供者的id不同，显示的不再是默认的项目名
    prefer-ip-address: true # 可以显示ip地址

```

![](https://img-blog.csdnimg.cn/img_convert/f907d99327f08f2ed8573619d77ac536.png)

![](https://img-blog.csdnimg.cn/img_convert/fa6a208eb9fc7d51f2356384ac400dac.png)

### 服务发现 Discovery`@EnableDiscoveryClient`

对于注册进 eureka 里面的微服务，可以通过服务发现来获得该服务的信息。（即我们前面可视化页面的信息）

1.  在主启动类上添加注解：`@EnableDiscoveryClient`
2.  在 Controller 里面打印信息：

```
@Resource // 自动注入
private DiscoveryClient discoveryClient;

@GetMapping("/customer/discovery")
public Object discovery(){
    //获得服务清单列表
    List<String> services = discoveryClient.getServices();
    for(String service: services){
        log.info("*****service: " + service);
    }
    // 根据具体服务进一步获得该微服务的信息
    List<ServiceInstance> instances = discoveryClient.getInstances("CLOUD-ORDER-SERVICE");
    for(ServiceInstance serviceInstance:instances){
        log.info(serviceInstance.getServiceId() + "\t" + serviceInstance.getHost()
                 + "\t" + serviceInstance.getPort() + "\t" + serviceInstance.getUri());
    }
    return this.discoveryClient;
}

```

### Eureka 自我保护机制

某时刻某一个微服务不可用了，Eureka 不会立即清理，依旧会对该微服务的信息进行保存。属于 CAP 里的 AP（高可用）分支

保护模式主要用于一组客户和 Eureka Server 之间存在网络分区场景下保护。一旦进入保护模式，Eureka Server 将会尝试保护其服务注册表中的信息，不再删除服务注册表中固定信息，也就是不会注销任何微服务。

如果在 Eureka Server 的首页看到以下这段提示，则说明 Eureka 讲入了保护模式：

> EMERGENCY!EUREKA MAY BE INCORRECTLY CLAIMING INSTANCES ARE UP WHEN THEY’RE NOT.  
> RENEWALS ARE LESSER THAN THRESHOLD AND HENCE THE INSTANCES ARE NOT BEING EXPIRED JUST TO BE SAFE

为什么会产生 Eureka 自我保护机制？

为了防止 Eureka Client 可以正常运行但是与 Eureka Server 网络不通情况下，Eureka Server 不会立刻将 Eureka Client 服务剔除

什么是自我保护模式？

默认情况下，如果 Eureka Server 在一定时间内没有接收到某个微服务实例的心跳，Eureka Server 将会注销该实例（默认 90 秒）。但是当网络分区故障发生时、卡顿、拥挤）时，微服务与 Eureka Server 之间无法正常通信，以上行为可能变得非常危险了—因为微服务本身其实是健康的，此时本不应该注销这个微服务。Eureka 通过 "自我保护模式" 来解决这个问题—当 Eureka Server 节点在短时间内丢失过多客户端时（可能发生了网络分区故障），那么这个节点就会进入自我保护模式。

自我保护机制：默认情况下 Eureka CIient 定时向 Eureka Server 端发送心跳包。

如果 Eureka 在 server 端在一定时间内（默认 90 秒）没有收到 Eureka Client 发送心跳包，便会直接从服务注册列表中剔除该服务，但是在短时间（90 秒内）内丢失了大量的服务实例心跳，这时 Eureka Server 会开启自我保护机制，不会剔除该服务（该现象可能出现如果网络不通但是 Eureka Client 出现宕机，此时如果别的注册中心如果一定时间内没有收到心跳会将剔除该服务这样就出现了严重失误，因为客户端还能正常发送心跳，只是网络延迟问题，而保护机制是为了解决此问题而产生的

在自我保护模式中，Eureka Server 会保护服务注册表中的信息，不再注册任何服务实例。

它的设计哲学就是宁可保留错误的服务注册信息，也不盲目注销任何可能健康的服务实例。一句话讲解：好死不如赖活着

综上，自我保护模式是一种应对网络异常的安全保护措施。它的架构哲学是宁可同时保留所有微服务（健康的微服务和不健康的微服务都会保留）也不盲目注销任何健康的微服务。使用自我保护模式，可以让 Eureka 集群更加的健壮、稳定。

禁止自我保护:（如果想）

> 在 Eureka Server 的模块中的 yml 文件进行配置：
> 
> ```
> server:
> port: 7001
> 
> eureka:
> instance:
>  hostname: eureka7001.com
> 
> client:
>  register-with-eureka: false
>  fetch-registry: false
>  service-url:
>    defaultZone: http://eureka7002.com:7002/eureka/
> server: # 与client平行
> 	# 关闭自我保护机制，保证不可用该服务被及时剔除
> 	enable-self-preservation: false
> 	eviction-interval-timer-in-ms: 2000
> 
> ```

修改 Eureka Client 模块的 心跳间隔时间：

```
# 提供者
server:
  port: 8001  # 端口号不一样

eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url: # 集群
      defaultZone: http://eureka7001.com:7001/eureka/,http://eureka7002.com:7002/eureka/
  instance: #重点，和client平行
    instance-id: payment8001 # 每个提供者的id不同，显示的不再是默认的项目名
    prefer-ip-address: true # 可以显示ip地址
    # Eureka客户端像服务端发送心跳的时间间隔，单位s，默认30s
    least-renewal-interval-in-seconds: 1
    # Rureka服务端在收到最后一次心跳后等待时间上线，单位为s，默认90s，超时将剔除服务
    least-expiration-duration-in-seconds: 2

```

##### eureka 配置项解读：

在注册服务之后，服务提供者会维护一个心跳用来持续高速 Eureka Server，“我还在持续提供服务”，否则 Eureka Server 的剔除任务会将该服务实例从服务列表中排除出去。我们称之为服务续约。  
面是服务续约的两个重要属性：

（1）eureka.instance.lease-expiration-duration-in-seconds  
leaseExpirationDurationInSeconds，表示 eureka server 至上一次收到 client 的心跳之后，等待下一次心跳的超时时间，在这个时间内若没收到下一次心跳，则将移除该 instance。  
默认为 90 秒  
如果该值太大，则很可能将流量转发过去的时候，该 instance 已经不存活了。  
如果该值设置太小了，则 instance 则很可能因为临时的网络抖动而被摘除掉。  
该值至少应该大于 leaseRenewalIntervalInSeconds

（2）eureka.instance.lease-renewal-interval-in-seconds  
leaseRenewalIntervalInSeconds，表示 eureka client 发送心跳给 server 端的频率。如果在 leaseExpirationDurationInSeconds 后，server 端没有收到 client 的心跳，则将摘除该 instance。除此之外，如果该 instance 实现了 HealthCheckCallback，并决定让自己 unavailable 的话，则该 instance 也不会接收到流量。  
默认 30 秒

> ***eureka.client.registry-fetch-interval-seconds*** : 表示 eureka client 间隔多久去拉取服务注册信息，默认为 30 秒，对于 api-gateway，如果要迅速获取服务注册状态，可以缩小该值，比如 5 秒  
> ***eureka.server.enable-self-preservation***  
> 是否开启自我保护模式，默认为 true。  
> 默认情况下，如果 Eureka Server 在一定时间内没有接收到某个微服务实例的心跳，Eureka Server 将会注销该实例（默认 90 秒）。但是当网络分区故障发生时，微服务与 Eureka Server 之间无法正常通信，以上行为可能变得非常危险了——因为微服务本身其实是健康的，此时本不应该注销这个微服务。  
> Eureka 通过 “自我保护模式” 来解决这个问题——当 Eureka Server 节点在短时间内丢失过多客户端时（可能发生了网络分区故障），那么这个节点就会进入自我保护模式。一旦进入该模式，Eureka Server 就会保护服务注册表中的信息，不再删除服务注册表中的数据（也就是不会注销任何微服务）。当网络故障恢复后，该 Eureka Server 节点会自动退出自我保护模式。  
> 综上，自我保护模式是一种应对网络异常的安全保护措施。它的架构哲学是宁可同时保留所有微服务（健康的微服务和不健康的微服务都会保留），也不盲目注销任何健康的微服务。使用自我保护模式，可以让 Eureka 集群更加的健壮、稳定。  
> ***eureka.server.eviction-interval-timer-in-ms***  
> eureka server 清理无效节点的时间间隔，默认 60000 毫秒，即 60 秒

Eureka 停更说明：

2.0 后停更了。

Zookeeper
---------

springCloud 整合 zookeeper

*   zookeeper 是一个分布式协调工具，可以实现注册中心功能
*   关闭 Linux 服务器防火墙后动 zookeeper 服务器
*   zookeeper 服务器取代 Eureka 服务器，zk 作为服务注册中心

##### 提供者

新建模块 cloud-provider-payment8004

pom 文件如下：

```
<artifactId>cloud-provider-payment8004</artifactId>

<dependencies>
    <!--springcloud 整合 zookeeper 组件-->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <!--zk发现-->
        <artifactId>spring-cloud-starter-zookeeper-discovery</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.apache.zookeeper</groupId>
                <artifactId>zookeeper</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.apache.zookeeper</groupId>
        <artifactId>zookeeper</artifactId>
        <version>3.4.9</version>
        <exclusions>
            <exclusion>
                <groupId>org.slf4j</groupId>
                <artifactId>slf4j-log4j12</artifactId>
            </exclusion>
        </exclusions>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter</artifactId>
    </dependency>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid-spring-boot-starter</artifactId>
        <version>1.1.10</version>
    </dependency>
    <!--mysql-connector-java-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
    </dependency>
    <!--jdbc-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-jdbc</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
    <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <groupId>com.dkf.cloud</groupId>
        <artifactId>cloud-api-commons</artifactId>
        <version>${project.version}</version>
    </dependency>
</dependencies>

```

yaml

```
server:
  port: 8004

spring:
  application:
    name: cloud-provider-service
  cloud:
    zookeeper:
      connect-string: 192.168.40.100:2181 # zk地址

```

主启动类：

```
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;

@SpringBootApplication
@EnableDiscoveryClient	 // 以后用这个就可以了，不用eureka了
public class PaymentMain8004 {
    public static void main(String[] args){
        SpringApplication.run(PaymentMain8004.class, args);
    }
}

```

Controller 打印信息：

```
@RestController
@Slf4j
public class PaymentController {

    @Resource
    private PaymentService paymentService;

    @Value("${server.port}")
    private String serverPort;

    @RequestMapping("/payment/zk")
    public String paymentzk(){
        return "springcloud with zookeeper :" + serverPort + "\t" + UUID.randomUUID().toString();
    }
}

```

如果 zookeeper 的版本和导入的 jar 包版本不一致，启动就会报错，由 zk-discovery 和 zk 之间的 jar 包冲突的问题。

解决这种冲突，需要在 pom 文件中，排除掉引起冲突的 jar 包，添加和服务器 zookeeper 版本一致的 jar 包，

但是新导入的 zookeeper jar 包 又有 slf4j 冲突问题，于是再次排除引起冲突的 jar 包

```
<!--springcloud 整合 zookeeper 组件-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-zookeeper-discovery</artifactId>
    <!-- 排除与zookeeper版本不一致到导致 冲突的 jar包 -->
    <exclusions>
        <exclusion>
            <groupId>org.apache.zookeeper</groupId>
            <artifactId>zookeeper</artifactId>
        </exclusion>
    </exclusions>
</dependency>
<!-- 添加对应版本的jar包 -->
<dependency>
    <groupId>org.apache.zookeeper</groupId>
    <artifactId>zookeeper</artifactId>
    <version>3.4.9</version>
    <!-- 排除和 slf4j 冲突的 jar包 -->
    <exclusions>
        <exclusion>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
        </exclusion>
    </exclusions>
</dependency>

```

启动测试：

```
# 在zk客户端
ls /services # 输入
[cloud-provider-service] #输出
# 继续向下查看
ls /services/cloud-provider-service
# 继续向下，然后get，返回了个json

```

我们在 zk 上注册的 node 是临时节点, 当我们的服务一定时间内没有发送心跳，那么 zk 就会将这个服务的 znode 删除了。没有自我保护机制。重新建立连接后 znode-id 号也会变

##### 消费者

> 创建测试 zookeeper 作为服务注册中心的 消费者 模块 cloud-customerzk-order80
> 
> 主启动类、pom 文件、yml 文件和提供者的类似

config 类，注入 RestTemplate

```
@SpringBootConfiguration
public class ApplicationContextConfig {
    @Bean
    @LoadBalanced // 继续加上这个
    public RestTemplate getTemplate(){
        return new RestTemplate();
    }
}

@SpringBootApplication
@EnableDiscoveryClient
public class OrderZKMain80{
    public static void main(String[] args) {
        SpringApplication.run(OrderZKMain80.class, args);
    }
}


```

controller 层也是和之前类似：

```
@RestController
@Slf4j
public class CustomerZkController {

    public static final String INVOKE_URL="http://cloud-provider-service"; //和原来一样

    @Resource
    private RestTemplate restTemplate;

    @RequestMapping("/customer/payment/zk")
    public String paymentInfo(){
        String result = restTemplate.getForObject(INVOKE_URL + "/payment/zk",String.class);
        return result;
    }
}

```

然后就在 zk 里查到 consumer 信息了。

关于 zookeeper 的集群搭建，目前使用较少，而且在 yml 文件中的配置也是类似，以列表形式写入 zookeeper 的多个地址即可，而且 zookeeper 集群，在 hadoop 的笔记中也有记录。总而言之，只要配合 zookeeper 集群，以及 yml 文件的配置就能完成集群搭建

后面会用 ribbon 代替 RestTemplate

Consul
------

> consul 也是服务注册中心的一个实现，是由 go 语言写的。官网地址： https://www.consul.io/intro 中文地址： https://www.springcloud.cc/spring-cloud-consul.html  
> Consul 是一套开源的分布式服务发现和配置管理系统。  
> 提供了微服务系统中的服务治理，配置中心，控制总线等功能。这些功能中的每一个都可以根据需要单独使用，也可以一起使用以构建全方位的服务网络。

*   服务发现：提供 HTTP 和 DNS 两种发现方式
*   健康监测：支持多种方式，HTTP、TCP、Docker、Shell 脚本定制化
*   KV 存储：Key、Value 的存储方式
*   多数据中心：Consul 支持多数据中心
*   可视化 Web 界面

### 安装并运行

> 下载地址：https://www.consul.io/downloads.html
> 
> 打开下载的压缩包，只有一个 exe 文件，实际上是不用安装的，在 exe 文件所在目录打开 dos 窗口使用即可。
> 
> 使用开发模式启动：consul agent -dev
> 
> 访问 8500 端口，即可访问首页

### 提供者

> 新建提供者模块：cloud-providerconsul-service8006

pom 文件：

```
	<artifactId>cloud-providerconsul-service8006</artifactId>
    <dependencies>
        <!--springcloud consul server-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-consul-discovery</artifactId>
        </dependency>

        <!-- springboot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <!-- 日常通用jar包 -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```

yml 文件：

```
server:
  port: 8006
spring:
  application:
    name: consul-provider-service
  cloud:
    consul:
      host: localhost
      port: 8500
      discovery:    # 指定注册对外暴露的服务名称
        service-name: ${spring.application.name}

```

主启动类：

```
@SpringBootApplication
@EnableDiscoveryClient // 提供者
public class ConsulProviderMain8006 {
    public static void main(String[] args) {
        SpringApplication.run(ConsulProviderMain8006.class,args);
    }
}

```

controller 也是简单的写一下就行。

### 消费者

> 新建 一个 在 82 端口的 消费者模块。pom 和 yml 和提供者的类似，主启动类不用说，记得注入 RestTemplate

```
@SpringBootApplication
@EnableDiscoveryClient //该注解用于向使用consul或者zookeeper作为注册中心时注册服务
public class OrderConsulMain80{
    public static void main(String[] args) {
            SpringApplication.run(OrderConsulMain80.class, args);
    }
}


@Configuration
public class ApplicationContextConfig{
    @Bean
    @LoadBalanced
    public RestTemplate getRestTemplate()
    {
        return new RestTemplate();
    }
}

```

controller 层：

```
@RestController
public class CustomerConsulController {

    public static final String INVOKE_URL="http://consul-provider-service";

    @Resource
    private RestTemplate restTemplate;

    @RequestMapping("/customer/payment/consul")
    public String paymentInfo(){
        String result = restTemplate.getForObject(INVOKE_URL + "/payment/consul",String.class);
        return result;
    }
}

```

总结
--

<table><thead><tr><th>组件名</th><th>语言</th><th>CAP</th><th>服务健康检查</th><th>对外暴露接口</th><th>SpringCloud 集合</th></tr></thead><tbody><tr><td>Eureka</td><td>java</td><td>AP</td><td>可配支持</td><td>HTTP</td><td>已集成</td></tr><tr><td>Consul</td><td>Go</td><td>CP</td><td>支持</td><td>HTTP/DNS</td><td>已集成</td></tr><tr><td>Zookeeper</td><td>java</td><td>CP</td><td>支持</td><td>客户端</td><td>已集成</td></tr></tbody></table>

CAP：

*   C：Consitency 强一致性
*   A：Available 可用性
*   P：Partition tolerance 分区容错性

CAP 理论关注粒度是数据，而不是整体系统设计的

![](https://img-blog.csdnimg.cn/img_convert/6151d7b348a7cf02a5107bc2821667a6.png)

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

上面讲了服务注册中心，下面讲服务调用

服务调用
====

RestTemplate 不是给我们提供远程调用了吗，那还要学其他的做什么。答案是负载均衡，在发送请求时通过负载均衡算法从提供者列表中选择一个。

> 都是使用在 client 端，即有 ” 消费者 “ 需求的模块中。  
> ![](https://img-blog.csdnimg.cn/img_convert/0665bd7da429fdb4c32683d44175999e.png)

Ribbon
------

我们这里提前启动好之前在搭建的 eureka Server 集群（5 个模块）

### 简介

SpringCloud Ribbon 是基于 NetfIixRibbon 实现的一套**客户端**负载均衡的工具。

简单的说，Ribbon 是 Neix 发布的开源项目，主要功能是提供**客户端的软件负载均衡算法和服务调用**。Ribbon 客户端组件提供一系列完善的配置项如**连接超时，重试**等。简单的说，就是在配置文件中列出 LoadBalancer（简称 LB) 后面所有的机器，Ribbon 会自动的帮助你基于某种规则（如简单轮询，随机连接等）去连接这些机器。我们很容易使用 Ribbon 实现自定义的负载均衡算法。

LB 负载均衡 (LoadBalance) 是什么？

简单的说就是将用户的请求平摊的分配到多个服务上，从而达到系统的 HA（高可用）。

常见的负载均衡有软件 Nginx，LVS，硬件 F5 等。

Ribbon 本地负载均衡客户端 VS Nginx 服务端负载均衡区别：

*   Nginx 是**服务器负载均衡**（集中式 LB），客户端所有请求都会交给 nginx，然后由 nginx 实现转发请求。即负载均衡是由服务端实现的。
    
*   Ribbon 是**本地负载均衡**（进程内 LB），在调用微服务接口时候，会**在注册中心上获取注册信息服务列表之后缓存到 JVM 本地**，从而在本地实现 RPC 远程服务调用技术。
    
*   集中式 LB：即在服务的消费方和提供方之间使用独立的 LB 设施（可以是硬件，如 F5，也可以是软件，如 nginx), 由该设施负责把访问请求通过某种策略转发至服务的提供方；
    
*   进程内 LB：将 LB 逻辑集成到消费方，消费方从服务注册中心获知有哪些地址可用，然后自己再从这些地址中选择出一个合适的服务器！Ribbon 就属于进程内 LB, 它只是一个类库，集成于消费方进程，消费方通过它来获取到服务提供方的地址。
    

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

Ribbon 在工作时分成两步：

*   第一步先选择 Eureka Server，它优先选择在同一个区域内负载较少的 server
*   第二步再根据用户指定的策略，在从 server 取到的服务注册列表中选择一个地址。
    *   其中 Ribbon 提供了多种策略：比如轮询、随相和根据响应时间加权。

上面在 eureka 时，确实实现了负载均衡机制，那是因为 **eureka-client 包里面自带着 ribbon**：

> 一句话，**Ribbon 就是 负载均衡 + RestTemplate 调用**。实际上不止 eureka 的 jar 包有，zookeeper 的 jar 包，还有 consul 的 jar 包都包含了他，就是上面使用的服务调用。

![](https://img-blog.csdnimg.cn/img_convert/20b76c287a08e1e165691a87a9db1984.png)

如果自己添加，在 模块的 pom 文件中引入：

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-ribbon</artifactId>
</dependency>

```

##### RestTemplate

对于 RestTemplate 的一些说明：

> 有两种请求方式：post 和 get , 还有两种返回类型：object 和 Entity

*   getForObject()/getForEntity()
    *   Object：返回对象响应体中数据转化成的对象，基本上可以理解成 json
    *   Entity：返回对象是 ResponseEntity 对象，包含了响应中的一些重要信息，比如响应头、响应状态码、响应体等
    *   返回的`entity.getBody()`即得到了 Object
*   postForObject()/postForEntity()

```
package com.atguigu.springcloud.controller;

@RestController
@Slf4j
public class OrderController{
    //public static final String PAYMENT_URL = "http://localhost:8001";

    public static final String PAYMENT_URL = "http://CLOUD-PAYMENT-SERVICE";

    @Resource
    private RestTemplate restTemplate;

    @Resource
    private LoadBalancer loadBalancer;
    @Resource
    private DiscoveryClient discoveryClient;

    @GetMapping("/consumer/payment/create")
    public CommonResult<Payment> create(Payment payment){
        return restTemplate.postForObject(PAYMENT_URL +"/payment/create",payment,CommonResult.class);
    }

    @GetMapping("/consumer/payment/get/{id}")
    public CommonResult<Payment> getPayment(@PathVariable("id") Long id){
        return restTemplate.getForObject(PAYMENT_URL+"/payment/get/"+id,CommonResult.class);
    }

    @GetMapping("/consumer/payment/getForEntity/{id}")
    public CommonResult<Payment> getPayment2(@PathVariable("id") Long id){
       //   ResponseEntity是spring中的类
        ResponseEntity<CommonResult> entity = restTemplate.getForEntity(PAYMENT_URL+"/payment/get/"+id,CommonResult.class);

        if(entity.getStatusCode().is2xxSuccessful()){
            return entity.getBody();//获取json
        }else{
            return new CommonResult<>(444,"操作失败");
        }
    }

    @GetMapping(value = "/consumer/payment/lb")
    public String getPaymentLB(){
        // 找到服务列表
        List<ServiceInstance> instances = discoveryClient.getInstances("CLOUD-PAYMENT-SERVICE");

        if(instances == null || instances.size() <= 0){
            return null;
        }
        // 负载均衡中选择一个服务
        ServiceInstance serviceInstance = loadBalancer.instances(instances);
        URI uri = serviceInstance.getUri();

        return restTemplate.getForObject(uri+"/payment/lb",String.class);
    }

    // ====================> zipkin+sleuth
    @GetMapping("/consumer/payment/zipkin")
    public String paymentZipkin(){
        String result = restTemplate.getForObject("http://localhost:8001"+"/payment/zipkin/", String.class);
        return result;
    }
}

```

### 负载均衡

IRule：根据特定算法从服务列表中选择一个要访问的服务

Ribbon 负载均衡规则类型：

*   com.netflix.loadbalancer.RoundRobinRule：轮询
*   com.netflix.loadbalancer.RandomRule：随机
*   com.netfIix.IoadbaIancer.RetryRuIe：先按照 RoundRobinRule 的策略获取服务，如果获取服务失败则在指定时间内会进行重试，获取可用的服务
*   WeightedResponseTimeRule：对 RoundRobinRule 的扩展，响应速度越快的实例选择权重越大，越容易被选择
*   BestAvailableRule：会先过滤掉由于多次访问故障而处于断路器跳闸状态的服务，然后选择一个并发量最小的服务
*   AvailabilityFilteringRule：先过滤掉故障实例，再选择并发较小的实例
*   ZoneAvoidanceRule：默认规则，复合判断 server 所在区域的性能和 server 的可用性选择服务器

![](https://img-blog.csdnimg.cn/img_convert/3fab156f64a839166f24865f6a425390.png)

配置负载均衡规则：

官方文档明确给出了警告：

> 这个自定义配置类不能放在 @ComponentScan 所扫描的当前包下以及子包下，否则我们自定义的这个配置类就会被所有的 Ribbon 客户端所共享，达不到特殊化定制的目的了。

注意上面说的，而 Springboot 主启动类上的 @SpringBootApplication 注解，相当于加了 @ComponentScan 注解，会自动扫描当前包及子包，所以注意不要放在 SpringBoot 主启动类的包内。

创建包：

*   java
    *   com.hh
        *   myrule
            *   MySelfRule.java
        *   springcloud
            *   主启动类

在这个包下新建 MySelfRule 类：

```
package com.dkf.myrule;

import com.netflix.loadbalancer.IRule;
import com.netflix.loadbalancer.RandomRule;

@Configuration
public class MySelfRule {
    @Bean
    public IRule myrule(){
        return new RandomRule(); //负载均衡规则定义为随机
    }
}

```

然后在主启动类上添加如下注解 @RibbonClient：

```
package com.dkf.springcloud;

import com.dkf.myrule.MySelfRule;

@SpringBootApplication
@EnableEurekaClient
@EnableDiscoveryClient
@RibbonClient(, configuration = MySelfRule.class)//指定该负载均衡规则对哪个提供者服务使用 ， 加载自定义规则的配置类
public class OrderMain80 {

    public static void main(String[] args){
        SpringApplication.run(OrderMain80.class, args);
    }
}

```

### 轮询算法原理

**负载均衡轮询算法** ：

rest 接口第几次请求次数 % 服务器集群总数量 = 实际调用服务器位置下标

每次服务器重启后，rest 接口计数从 1 开始。

![](https://img-blog.csdnimg.cn/img_convert/bbbad3b38503c1d502c364aa8849c715.png)

ribbon 源码：

```
private AtomicInteger nextServerCyclicCounter;

public Server choose(ILoadBalancer lb, Object key) {

    Server server = null;
    int count = 0;
    while (server == null && count++ < 10) {
        List<Server> reachableServers = lb.getReachableServers();
        List<Server> allServers = lb.getAllServers();
        int upCount = reachableServers.size();
        int serverCount = allServers.size();

        int nextServerIndex = incrementAndGetModulo(serverCount);
        server = allServers.get(nextServerIndex);

        if (server == null) {
            /* Transient. */
            Thread.yield();
            continue;
        }

        if (server.isAlive() && (server.isReadyToServe())) {
            return (server);
        }

        // Next.
        server = null;
    }

    if (count >= 10) {
        log.warn("No available alive servers after 10 tries from load balancer: "  + lb);
    }
    return server;
}
private int incrementAndGetModulo(int modulo) {
    for (;;) {
        int current = nextServerCyclicCounter.get();//获取原子的值
        int next = (current + 1) % modulo;
        if (nextServerCyclicCounter.compareAndSet(current, next)) //CAS
            return next;
    }
}

```

手写负载算法：cas + 自旋

首先 8001、8002 服务 controller 层加上

```
@GetMapping("/payment/lb")
public String getPaymentLB() {
    return SERVER_PORT;
}

```

LoadBalancer 接口：

```
import org.springframework.cloud.client.ServiceInstance;
import java.util.List;

public interface LoadBalancer {
    ServiceInstance instances(List<ServiceInstance> serviceInstances);
}

```

实现

```
import org.springframework.cloud.client.ServiceInstance;
import java.sql.SQLOutput;

@Component
public class MyLB implements LoadBalancer {

    private AtomicInteger atomicInteger = new AtomicInteger(0);

    private final int getAndIncrement() {
        int current;
        int next;

        do {
            current = this.atomicInteger.get();
            next = current >= Integer.MAX_VALUE ? 0 : current + 1;
        } while (!atomicInteger.compareAndSet(current, next));
        System.out.println("第几次访问,次数next:" + next);
        return next;
    }

    @Override
    public ServiceInstance instances(List<ServiceInstance> serviceInstances) {
        int index = getAndIncrement() % serviceInstances.size();
        return serviceInstances.get(index);
    }
}

```

controller 类中添加：

```
@GetMapping("/consumer/payment/lb")
public String getPaymentLB() {
    List<ServiceInstance> instances = discoveryClient.getInstances("CLOUD-PAYMENT-SERVICE");//获得总的提供者数
    if (instances == null || instances.size() <= 0) {
        return null;
    }

    ServiceInstance serviceInstance = loadBalancer.instances(instances);//传入总的实例数
    URI uri = serviceInstance.getUri();

    return restTemplate.getForObject(uri + "/payment/lb", String.class);
}

```

OpenFeign
---------

### 概述

> 这里和之前学的 dubbo 很像，例如消费者的 controller 可以调用提供者的 service 层方法，但是不一样，它貌似只能调用提供者的 controller，即写一个提供者项目的 controller 的接口，消费者来调用这个接口方法，就还是相当于是调用提供者的 controller ，和 RestTemplate 没有本质区别

Feign 能干什么：

Feign 旨在使编写 JavaHttp 客户端变得更容易。

前面在使用 Ribbon+RestTemplate 时，利用 RestTemplate 对 http 请求的封装处理，形成了一套模版化的调用方法。但是在实际开发中，由于对服务依赖的调用可能不止一处，往往一个接囗会被多处调用，所以通常都会针对每个微服务自行封装些客户端类来包装这些依赖服务的调用。所以，Feign 在此基础上做了进一步封装，由他来帮助我们定义和实现依赖服务接口的定义。在 Feign 的实现下，我们**只需创建一个接口并使用注解的方式来配置它**（以前是 Dao 接口上面标注 Mapper 注解，现在是一个微服务接口上面标注一个 Feign 注解即可，即可完成对服务提供方的接口绑定，简化了使用 Springcloud Ribbon 时，自动封装服务调用客户端的开发量。

Feign 集成了 Ribbon

利用 Ribbon 维护了 Payment 的服务列表信息，并目通过轮询实现了客户端的负载均衡。而与 Ribbon 不同的是，通过 feign 只需要定义服务绑定接口目以声明式的方法，优雅而简单的实现了服务调用

<table><thead><tr><th>Feign</th><th>OpenFeign</th></tr></thead><tbody><tr><td>Feign 是 SpringCloud 组件中的一个轻量级 RESTful 的 HTTP 服务客户端。Feign 内置了 Ribbon，用来做客户端负载均衡，去调用服务注册中心的服务。Feign 的使用方式是：使用 Feign 的注解定义接口，调用这个接口，就可以调用服务注册中心的服务</td><td>OpenFeign 是 SpringCloud 在 Feign 的基础上支持了 SpringMVC 的注解，如 @RequestMapping 等等。OpenFeign 的<code>@FeignClient</code>可以解析 SpringMVC 的下的接囗，并通过动态代理的方式产生实现类，实现类中做负载均衡并调用其他服务。</td></tr><tr><td>org.springframework.cloud spring-cloud-starter-feign</td><td>org.springframework.cloud spring-cloud-starter-openfeign</td></tr></tbody></table>

### 消费端

新建 cloud-consumer-feign-order80 模块

feign 用在消费端，feign 自带负载均衡配置，所以不用手动配置

pom ：

```
	<dependencies>
        <!-- Open Feign，他里面也有ribbon，所以有负载均衡 -->
         <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
        <!-- eureka Client -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

```

yaml

```
server:
  port: 80

eureka:
  client:
    register-with-eureka: false
    service-url: # 配置服务中心，openFeign去里面找服务
      defaultZone: http://eureka7001.com:7001/eureka/,http://eureka7002.com:7002/eureka/

```

###### `@EnableFeignClients`

主启动类：

```
@SpringBootApplication
@EnableFeignClients   //关键注解
public class CustomerFeignMain80 {
    public static void main(String[] args) {
        SpringApplication.run(CustomerFeignMain80.class, args);
    }
}

```

###### `@FeignClient`

新建一个 service

> 这个 service 还是 customer 模块的接口，和提供者没有任何关系，不需要包类名一致。它使用起来就相当于是普通的 service。
> 
> 推测大致原理，对于这个 service 接口，读取它某个方法的注解（GET 或者 POST 注解不写报错），知道了请求方式和请求地址，而抽象方法，只是对于我们来讲，调用该方法时，可以进行传参等。

```
@Component //别忘了添加这个
@FeignClient(value = "CLOUD-PROVIDER-SERVICE")  //服务名称，要和eureka上面的一致才行
public interface PaymentFeignService
{
    //这个就是provider 的controller层的方法定义。
    @GetMapping(value = "/payment/get/{id}")
    public CommonResult<Payment> getPaymentById(@PathVariable("id") Long id);

    @GetMapping(value = "/payment/feign/timeout")
    public String paymentFeignTimeout();
}
/*
在提供端有：
	@GetMapping(value = "/payment/get/{id}")
    public CommonResult<Payment> getPaymentById(@PathVariable("id") Long id)
    {
        Payment payment = paymentService.getPaymentById(id);

        if(payment != null)
        {
            return new CommonResult(200,"查询成功,serverPort:  "+serverPort,payment);
        }else{
            return new CommonResult(444,"没有对应记录,查询ID: "+id,null);
        }
    }
*/

```

Controller 层：

```
//使用起来就相当于是普通的service。
@RestController
public class CustomerFeignController {

    @Resource
    private PaymentFeignService paymentFeignService;//动态代理

    @GetMapping("/customer/feign/payment/{id}")
    public CommonResult<Payment> getPaymentById(@PathVariable("id") Long id){
        return paymentFeignService.getPaymentById(id);
    }
}

```

### 超时控制

超时设置，故意设置超时演示出错情况：

*   服务提供方 8001 故意写暂停程序
*   服务消费方 80 添加超时方法 PaymentFeignService
*   服务消费方 80 添加超时方法 OrderFeignControIIer
*   测试：http://localhost/consumer/payment/feign/timeout  
    错误页面

> Openfeign 默认超时等待为一秒，在消费者里面配置超时时间

```
//8001服务提供方 
@GetMapping(value = "/payment/feign/timeout")
public String paymentFeignTimeout(){
    // 业务逻辑处理正确，但是需要耗费3秒钟
    try { TimeUnit.SECONDS.sleep(3); } catch (InterruptedException e) { e.printStackTrace(); }
    return serverPort;
}

```

```
//消费方80 
@GetMapping(value = "/consumer/payment/feign/timeout")
public String paymentFeignTimeout(){
    // OpenFeign客户端一般默认等待1秒钟
    return paymentFeignService.paymentFeignTimeout();
}

```

```
eureka:
  client:
    register-with-eureka: false
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/,http://eureka7002.com:7002/eureka/
#设置feign客户端超时时间(OpenFeign默认支持ribbon)
ribbon:
  #指的是建立连接所用的时间，适用于网络状况正常的情况下,两端连接所用的时间
  ReadTimeout: 5000
  #指的是建立连接后从服务器读取到可用资源所用的时间
  ConnectTimeout: 5000

```

### 开启日志打印

Feign 共了日志打印功能，我们可以诵过配置来调整日志级别，从而了解 Feign 中 Tttp 请求的细节。

说白了就是对 Feign 接口的调用情况进行监控和输出。

日志级别：

*   NONE. 默认的，不显示任何日志；
*   BASIC，仅记录请求方法、URL、响应状态码及执行时间；
*   HEADERS：除了 BASIC 中定义的信息之外，还有请求和响应的头信息
*   FULL: 除了 HEADERS 中定义的信息之外，还有请求和响应的正文及元数据。

首先写一个 config 配置类：

```
package com.atguigu.springcloud.config;

import feign.Logger;

@Configuration
public class FeignConfig{
    @Bean
    Logger.Level feignLoggerLevel(){
        return Logger.Level.FULL;
    }
}

```

然后在 yml 文件中开启日志打印配置：

```
server:
  port: 80

eureka:
  client:
    register-with-eureka: false
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/,http://eureka7002.com:7002/eureka/
  #设置feign客户端超时时间(OpenFeign默认支持ribbon)
ribbon:
  #指的是建立连接所用的时间，适用于网络状况正常的情况下,两端连接所用的时间
  ReadTimeout: 5000
  #指的是建立连接后从服务器读取到可用资源所用的时间
  ConnectTimeout: 5000

logging:
  level:
    # feign日志以什么级别监控哪个接口
    com.atguigu.springcloud.service.PaymentFeignService: debug

```

中级部分
====

> 主要是服务降级、服务熔断、服务限流的开发思想和框架实现

![](https://img-blog.csdnimg.cn/img_convert/0665bd7da429fdb4c32683d44175999e.png)

Hystrix 断路器
===========

> 官方地址：https://github.com/Netflix/Hystrix/wiki/How-To-Use
> 
> " 断路器 “本身是一种开关装置，当某个服务单元发生故障之后，涌过断路器的故障监控（类似熔断保险丝），向调用方返回一个符合预期的、可处理的备选响应 (FallBack)，而不是长时间的等待或者抛出调用方无法处理的异常，这样就保证了服务调用方的线程不会被长时间、不必要地占用，从而避免了故障在分布式系统中的蔓延，乃至雪崩。

概述
--

##### 服务雪崩：

多个微服务之间调用的时候，假设微服务 A 调用微服务 B 和微服务 C，微服务 B 和微服务 C 又调用其它的微服务，这就是所谓的 “**扇出** "

```
A-->B,C
BC-->D

```

如果扇出的链路上某个微服务的调用响应时间过长或者不可用，对微服务 A 的调用就会占用越来越多的系统资源，进而引起系统崩溃，即所谓的 “`雪崩效应`”。

对于高流量的应用来说，单一的后端依赖可能会导致所有服务器上的所有资源都在几秒钟内饱和。比失败更糟糕的是，这些应用程序还可能导致服务之间的延迟增加，备份队列，线程和其他系统资源紧张，导致整个系统发生更多的级联故障。这些都表示需要对故障和延迟进行隔离和管理，以便单个依赖关系的失败，不能取消整个应用程序或系统。

Hystrix 是一个用于处理分布式系统的延迟和容错的开源库，在分布式系统里，许多依赖不可避免的会调用失败，比如超时、异常等，Hystrix 能够保证在一个依赖出问题的情况下，不会导致整体服务失败，避免级联故障，以提高分布式系统的弹性。

> Hystrix 停止更新，进入维护阶段：https://github.com/Netflix/Hystrix
> 
> https://github.com/Netflix/Hystrix/wiki/How-To-Use

##### 服务降级：

fallback

> 服务器忙碌或者网络拥堵时，不让客户端等待并立刻返回一个友好提示，fallback。
> 
> *   对方系统不可用了，你需要给我一个**兜底的方法**，不要耗死。
> *   向调用方返回一个符合预期的、可处理的**备选响应** (FallBack)，而不是长时间的等待或者抛出调用方无法处理的异常，这样就保证了服务调用方的线程不会被长时间、不必要地占用，从而避免了故障在分布式系统中的蔓延，乃至雪崩。

降低发生的情况：

*   程序运行异常
*   超时
*   服务熔断触发服务降级
*   线程池 / 信号量打满也会导致服务降级

##### 服务熔断：

break

*   类比保险丝达到最大服务访问后，**直接拒绝访问**，拉闸限电，然后调用服务降级的方法并返回友好提示
*   就是保险丝：服务的降级 -> 进熔断 -> 恢复调用链路

##### 服务限流：

flowlimit

秒杀高并发等操作，严禁一窝蜂的过来拥挤，大家排队，一秒钟几个，有序进行

> 可见，上面的技术不论是消费者还是提供者，根据真实环境都是可以加入配置的。

断路案例
----

> 首先构建一个 eureka 作为服务中心的单机版微服务架构 ，这里使用之前 eureka Server 7001 模块，作为服务中心

新建 提供者 `cloud-provider-hystrix-payment8001` 模块：

pom 文件：

```
	<dependencies>
        <!-- hystrix -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
        </dependency>
        
        <!--eureka-client-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```

下面主启动类、service、和 controller 代码都很简单普通。

主启动类：

```
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)
@EnableEurekaClient
public class PaymentMain8001 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain8001.class,args);
    }
}

```

service 层：

```
@Service
public class PaymentService {

    /* 可以正常访问的方法*/
    public String paymentinfo_Ok(Integer id){
        return "线程池：" + Thread.currentThread().getName() + "--paymentInfo_OK，id:" + id;
    }

    /* 超时访问的方法 */
    public String paymentinfo_Timeout(Integer id){
        int interTime = 3;
        try{
            TimeUnit.SECONDS.sleep(interTime);//模拟超时
        }catch (Exception e){
            e.printStackTrace();
        }
        return "线程池：" + Thread.currentThread().getName() + "--paymentInfo_Timeout，id:" + id + 
            "耗时" + interTime + "秒钟--";
    }
}

```

controller 层：

```
@RestController
@Slf4j
public class PaymentController {

    @Resource
    private PaymentService paymentService;

    @Value("${server.port}")
    private String serverPort;

    @GetMapping("/payment/hystrix/{id}")
    public String paymentInfo_OK(@PathVariable("id")Integer id){
        log.info("paymentInfo_OKKKKOKKK");
        return paymentService.paymentinfo_Ok(id);
    }

    @GetMapping("/payment/hystrix/timeout/{id}")
    public String paymentInfo_Timeout(@PathVariable("id")Integer id){
        log.info("paymentInfo_timeout");
        return paymentService.paymentinfo_Timeout(id);
    }
}

```

### 模拟高并发

##### `JMeter`

这里使用一个新东西 JMeter 压力测试器，模拟多个请求

下载压缩包，解压，双击 /bin/ 下的 jmeter.bat 即可启动

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

ctrl + S 保存后，输入请求地址开始压测。

![](https://img-blog.csdnimg.cn/img_convert/4393d2e2bd953e109c050dd459a29647.png)

**从测试可以看出，当模拟的超长请求被高并发以后，访问普通的小请求速率也会被拉低。**

tomcat 的默认工作线程数被打满了，没有多余的线程来分解压力和处理。

上面还是服务 8001 自己测试，加入此时外部的消费者 80 页来访问，那消费者只能干等，最终导致消费端 80 不满意，服务端 8001 直接被拖死。

测试可见，当启动高并发测试时，消费者访问也会变得很慢，甚至出现超时报错。

演示问题：8001 端口自身已经被打满了，80 还要访问 8001，80 也响应慢了。

*   超时导致服务器变慢（转圈）：超时不再等待
*   出错（宕机或程序运行出错）：出错要有兜底

解决思路：

*   对方服务（8001）`超时`了，调用者（80）不能一直卡死等待，必须有服务降级
*   对方服务（8001) `down机`了，调用者（80）不能一直卡死等待，必须有服务降级
*   对方服务（8001) OK，调用者（80）自己出故障或有自我要求（自己的等待时间小于服务提供者），自己处理降级

### 服务降级案例

新建消费者 `cloud-customer-feign-hystrix-order80` 模块：以 feign 为服务调用，eureka 为服务中心的模块，

```
<dependencies>
    <!--openfeign-->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-openfeign</artifactId>
    </dependency>
    <!--hystrix-->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
    </dependency>
    <!--eureka client-->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>

```

```
server:
  port: 80

eureka:
  client:
    register-with-eureka: false
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/

feign:
  hystrix:
    enabled: true

```

主启动类

```
@SpringBootApplication
@EnableFeignClients
@EnableHystrix
public class OrderHystrixMain80{//消费端
    public static void main(String[] args) {
        SpringApplication.run(OrderHystrixMain80.class,args);
    }
}

```

> 一般服务降级放在客户端，即 消费者端 ，但是提供者端一样能使用。
> 
> 首先提供者，即 8001 先从自身找问题，设置自身调用超时的峰值，峰值内正常运行，超出峰值需要有兜底的方法处理，作服务降级 fallback

#### 服务端降级`@HystrixCommand`

首先 对 `8001`的 service 进行配置（对容易超时的方法进行配置) :

降级配置：`@HystrixCommand`，可以在里面指定超时 / 出错的回调方法，作为兜底方法

提供方 service 方法：演示超时

```
// 服务端service
@HystrixCommand(fallbackMethod = "paymentInfo_TimeOutHandler",//超时后回调方法
                commandProperties = {
                    @HystrixProperty(,//时间单位
                                     value="3000")})//超时时间
public String paymentInfo_TimeOut(Integer id){
    try { TimeUnit.MILLISECONDS.sleep(5000); } catch (InterruptedException e) { e.printStackTrace(); }
    return "线程池:  "+Thread.currentThread().getName()+" id:  "+id+"\t"+"O(∩_∩)O哈哈~"+"  耗时(秒): ";
}

// 兜底方法
public String paymentInfo_TimeOutHandler(Integer id){ // 回调函数向调用方返回一个符合预期的、可处理的备选响应
    return "线程池:  "+Thread.currentThread().getName()+"  8001系统繁忙或者运行报错，请稍后再试,id:  "+id+"\t"+"o(╥﹏╥)o";
}

```

提供方 主启动类：

```
@SpringBootApplication
@EnableEurekaClient
@EnableCircuitBreaker//加上这个
public class PaymentHystrixMain8001{//提供者
    public static void main(String[] args) {
            SpringApplication.run(PaymentHystrixMain8001.class, args);
    }

```

上面演示的是超时，下面演示上面 service 出错：同样走一样的回调方法

```
// 服务端service
@HystrixCommand(fallbackMethod = "paymentInfo_TimeOutHandler",//超时后回调方法，出错后也走
                commandProperties = {
                    @HystrixProperty(,//时间单位
                                     value="3000")})//超时时间
public String paymentInfo_TimeOut(Integer id){
    int age = 10/0;
    return "线程池:  "+Thread.currentThread().getName()+" id:  "+id+"\t"+"O(∩_∩)O哈哈~"+"  耗时(秒): ";
}

// 兜底方法
public String paymentInfo_TimeOutHandler(Integer id){ // 回调函数向调用方返回一个符合预期的、可处理的备选响应
    return "线程池:  "+Thread.currentThread().getName()+"  8001系统繁忙或者运行报错，请稍后再试,id:  "+id+"\t"+"o(╥﹏╥)o";
}

```

#### 消费端降级

上面的案例是服务端降级，现在我们服务端处理 3s，然后返回。但是消费端等 1s 就等不住了，这时候就需要消费端也有降级方法

`80`的降级。原理是一样的，上面的 @HystrixCommand 降级可以放在服务端，也可以放在消费端。但一般放在客户端。

> 注意：我们自己配置过的热部署方式对 java 代码的改动明显，但对 @HystrixCommand 内属性的修改建议重启微服务。

```
server:
  port: 80

eureka:
  client:
    register-with-eureka: false
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/

feign:
  hystrix:
    enabled: true

```

```
@SpringBootApplication
@EnableFeignClients
@EnableHystrix // 加上这个  //注意区别我们在提供端添加的注解是@EnableCircuitBreaker
public class OrderHystrixMain80{
    public static void main(String[] args){
        SpringApplication.run(OrderHystrixMain80.class,args);
    }
}

```

然后对 80 进行服务降级：很明显 service 层是接口，所以我们对消费者，在它的 controller 层进行降级。继续使用`@HystrixCommand`注解指定方法超时后的回调方法

controller

```
@RestController
@Slf4j
public class OrderHystirxController{
    @Resource
    private PaymentHystrixService paymentHystrixService;


    @GetMapping("/consumer/payment/hystrix/timeout/{id}")
    @HystrixCommand(fallbackMethod = "paymentTimeOutFallbackMethod",
                    commandProperties = {
            @HystrixProperty(,
                             value="1500") })//只等1.5s
    //@HystrixCommand
    public String paymentInfo_TimeOut(@PathVariable("id") Integer id) {
        // int age = 10/0;
        String result = paymentHystrixService.paymentInfo_TimeOut(id);
        return result;
    }
    public String paymentTimeOutFallbackMethod(@PathVariable("id") Integer id) {
        return "我是消费者80,对方支付系统繁忙请10秒钟后再试 或者 自己运行出错请检查自己,o(╥﹏╥)o";
    }
}
//然后我们把上面的 int age=10/0;打开，出错后也会调用它的兜底方法

```

service

```
@Component
@FeignClient(value = "CLOUD-PROVIDER-HYSTRIX-PAYMENT" ,fallback = PaymentFallbackService.class)
public interface PaymentHystrixService{
    @GetMapping("/payment/hystrix/ok/{id}")
    public String paymentInfo_OK(@PathVariable("id") Integer id);

    @GetMapping("/payment/hystrix/timeout/{id}")
    public String paymentInfo_TimeOut(@PathVariable("id") Integer id);
}

```

目前问题：

*   每个业务方法对应一个兜底的方法，代码膨胀
*   同样和自定义分开

我们定义一个全局的兜底方法，这样就不用每个方法都得写兜底方法了。

##### 全局兜底`@DefaultProperties`

```
@RestController
@Slf4j
@DefaultProperties(defaultFallback = "payment_Global_FallbackMethod") //添加了这个
public class OrderHystirxController{
    @Resource
    private PaymentHystrixService paymentHystrixService;

    @GetMapping("/consumer/payment/hystrix/timeout/{id}")
    @HystrixCommand(fallbackMethod = "paymentTimeOutFallbackMethod",
                    commandProperties = {
            @HystrixProperty(,
                             value="1500") })//只等1.5s
    public String paymentInfo_TimeOut(@PathVariable("id") Integer id) {
        // int age = 10/0;
        String result = paymentHystrixService.paymentInfo_TimeOut(id);
        return result;
    }
    public String paymentTimeOutFallbackMethod(@PathVariable("id") Integer id) {
        return "我是消费者80,对方支付系统繁忙请10秒钟后再试 或者 自己运行出错请检查自己,o(╥﹏╥)o";
    }

    // 下面是全局fallback方法
    public String payment_Global_FallbackMethod(){
        return "Global异常处理信息，请稍后再试，/(ㄒoㄒ)/~~";
    }
}
// 自己指定了兜底方法的话就走自己的兜底方法，否则走全局的兜底方法

```

##### service 降级`@FeignClient`

下面解决业务逻辑混在一起的问题（解耦）：我们改在 service 层进行服务降级

> 服务降级，客户端去调用服务端，碰上服务端宕机或关闭。
> 
> 本次案例降级处理是在客户端 80 实现完成的，与服务端 8001 没有关系。只需要为 Feign 客户端定义的接口添加一个服务降级处理的实现类即可实现解耦。

在这种方式一般是在客户端，即消费者端，首先上面再 controller 中添加的 @HystrixCommand 和 @DefaultProperties 两个注解去掉。就是保持原来的 controller

```
@Component 	// service
@FeignClient(value = "CLOUD-PROVIDER-HYSTRIX-PAYMENT" ,
             fallback = PaymentFallbackService.class)//指定的是回调的class类
public interface PaymentHystrixService{
    @GetMapping("/payment/hystrix/ok/{id}")
    public String paymentInfo_OK(@PathVariable("id") Integer id);

    @GetMapping("/payment/hystrix/timeout/{id}")
    public String paymentInfo_TimeOut(@PathVariable("id") Integer id);
}

```

service 回调方法：是 service 接口的实现类。此时就不需要在 controller 上写 fallback 方法了

```
@Component
public class PaymentFallbackService implements PaymentHystrixService{ // 统一为该接口异常处理
    @Override
    public String paymentInfo_OK(Integer id){
        return "-----PaymentFallbackService fall back-paymentInfo_OK ,o(╥﹏╥)o";
    }

    @Override //兜底方法，根据上述配置，程序内发生异常、或者运行超时，都会执行该兜底方法
    public String paymentInfo_TimeOut(Integer id){
        return "-----PaymentFallbackService fall back-paymentInfo_TimeOut ,o(╥﹏╥)o";
    }
}

```

此时的 yml 文件配置

```
server:
  port: 80
spring:
  application:
    name: cloud-customer-feign-hystrix-service
eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/

# 用于服务降级 在注解@FeignClient 中添加 fallback 属性值
feign:
  hystrix:
    enabled: true  # 在feign中开启 hystrix

```

2.  修改 service 接口：

```
@Component											// 这里是重点
@FeignClient(value = "CLOUD-PROVIDER-HYSTRIX-PAYMENT", fallback = OrderFallbackService.class)
public interface OrderService {

    @GetMapping("/payment/hystrix/{id}")
    public String paymentInfo_OK(@PathVariable("id")Integer id);

    @GetMapping("/payment/hystrix/timeout/{id}")
    public String paymentInfo_Timeout(@PathVariable("id")Integer id);

}

```

3.  fallback 指向的类：

```
package com.dkf.springcloud.service;

@Component		//注意这里，它实现了service接口
public class OrderFallbackService implements  OrderService{


    @Override
    public String paymentInfo_OK(Integer id) {
        return "OrderFallbackService --发生异常";
    }

    @Override
    public String paymentInfo_Timeout(Integer id) {
        return "OrderFallbackService --发生异常--paymentInfo_Timeout";
    }
}

```

新问题，这样配置如何设置超时时间？

> 首先要知道 下面两个 yml 配置项：
> 
> ```
> hystrix.command.default.execution.timeout.enable=true    ## 默认值
> 
> ## 为false则超时控制有ribbon控制，为true则hystrix超时和ribbon超时都是用，但是谁小谁生效，默认为true
> 
> hystrix.command.default.execution.isolation.thread.timeoutInMilliseconds=1000  ## 默认值
> 
> ## 熔断器的超时时长默认1秒，最常修改的参数
> 
> ```
> 
> 看懂以后，所以：
> 
> 只需要在 yml 配置里面配置 Ribbon 的 超时时长即可。注意：hystrix 默认自带 ribbon 包。
> 
> ```
> ribbon:
> 	ReadTimeout: xxxx
> 	ConnectTimeout: xxx
> 
> ```

### 服务熔断案例

> 实际上服务熔断 和 服务降级 没有任何关系，就像 java 和 javaScript
> 
> 服务熔断，有点自我恢复的味道
> 
> 参考：https://blog.csdn.net/www1056481167/article/details/81157171

> **服务雪崩**
> 
> 多个微服务之间调用的时候，假设微服务 A 调用微服务 B 和微服务 C，微服务 B 和微服务 C 有调用其他的微服务，这就是所谓的” 扇出”，如扇出的链路上某个微服务的调用响应式过长或者不可用，对微服务 A 的调用就会占用越来越多的系统资源，进而引起系统雪崩，所谓的” 雪崩效应”
> 
> **Hystrix**：
> 
> Hystrix 是一个用于分布式系统的延迟和容错的开源库。在分布式系统里，许多依赖不可避免的调用失败，比如超时、异常等，Hystrix 能够保证在一个依赖出问题的情况下，不会导致整个服务失败，避免级联故障，以提高分布式系统的弹性。
> 
> **断路器**：
> 
> “断路器” 本身是一种开关装置，当某个服务单元发生故障监控 (类似熔断保险丝)，向调用方法返回一个符合预期的、可处理的备选响应 (FallBack)，而不是长时间的等待或者抛出调用方法无法处理的异常，这样就保证了服务调用方的线程不会被长时间、不必要地占用，从而避免了故障在分布式系统中的蔓延。乃至雪崩。
> 
> **服务熔断**：
> 
> 熔断机制是应对雪崩效应的一种微服务链路保护机制，当扇出链路的某个微服务不可用或者响应时间太长时，会进行服务的降级，进而熔断该节点微服务的调用，快速返回” 错误” 的响应信息。
> 
> 当检测到该节点微服务响应正常后恢复调用链路，在 SpringCloud 框架机制通过 Hystrix 实现，Hystrix 会监控微服务见调用的状况，当失败的调用到一个阈值，默认是 5 秒内 20 次调用失败就会启动熔断机制，熔断机制的注解是`@HystrixCommand`

熔断的状态：

*   熔断打开：请求不再进行调用当前服务，内部设置时钟一般为 MTTR（平均故障处理时间），当打开时长达到所设时钟则进入半熔断状态
*   熔断关闭：熔断关闭不会对服务进行熔断
*   熔断半开：**部分请求**根据规则调用当前服务，如果请求成功目符合规则，则认为当前服务恢复正常，关闭熔断。

修改 cloud-provider-hystrix-payment8001 模块

```
package com.atguigu.springcloud.service;

import cn.hutool.core.util.IdUtil;
import com.netflix.hystrix.contrib.javanica.annotation.HystrixCommand;
import com.netflix.hystrix.contrib.javanica.annotation.HystrixProperty;

@Service
public class PaymentService{

    //=====服务熔断
    @HystrixCommand(fallbackMethod = "paymentCircuitBreaker_fallback",
                    commandProperties = {
            @HystrixProperty(name = "circuitBreaker.enabled",value = "true"),// 是否开启断路器
            @HystrixProperty(name = "circuitBreaker.requestVolumeThreshold",value = "10"),// 请求次数
            @HystrixProperty(name = "circuitBreaker.sleepWindowInMilliseconds",value = "10000"), // 时间窗口期
            @HystrixProperty(name = "circuitBreaker.errorThresholdPercentage",value = "60"),// 失败率达到多少后跳闸
    }) // 在10s内10次请求有60%失败 // 先看次数，再看百分比
    public String paymentCircuitBreaker(@PathVariable("id") Integer id){
        if(id < 0) {
            throw new RuntimeException("******id 不能负数");
        }
        String serialNumber = IdUtil.simpleUUID();// 等价于UUID.randomUUID().toString(); //pom中有hutool-all

        return Thread.currentThread().getName()+"\t"+"调用成功，流水号: " + serialNumber;
    }
    
    public String paymentCircuitBreaker_fallback(@PathVariable("id") Integer id){//服务降级
        return "id 不能负数，请稍后再试，/(ㄒoㄒ)/~~   id: " +id;
    }

}

```

涉及到断路器的三个重要参数快照时间窗、请求总数阀值、错误百分比阀值

*   1：快照时间窗：断路器确定是否打开需要统计一些请求和错误数据而统计的时间范围就是快照时间窗，默认为最近的 10 秒。
*   2：请求总数阀值：在快照时间窗内，必须满足请求总数阀值才有资格熔断。默认为 20，意味着在 10 秒内，如果该 hystrix 命令的调用次数不足 20 次，即使所有的请求都超时或具他原因失败，断路器都不会打开。
*   3：错误百分比阀值：当请求总数在快照时间窗内超过了阀值，上日发生了 30 次调用，如果在这 30 次调用中，有 15 次发生了超时异常，也就是超过 50％的错误百分比，在默认设定 50％阀值情况，这时候就会将断路器打开。

> The precise way that the circuit opening and closing occurs is as follows:
> 
> 1.  Assuming the volume across a circuit meets a certain threshold (`HystrixCommandProperties.circuitBreakerRequestVolumeThreshold()`)…
> 2.  And assuming that the error percentage exceeds the threshold error percentage (`HystrixCommandProperties.circuitBreakerErrorThresholdPercentage()`)…
> 3.  Then the circuit-breaker transitions from `CLOSED` to `OPEN`.
> 4.  While it is open, it short-circuits all requests made against that circuit-breaker.
> 5.  After some amount of time (`HystrixCommandProperties.circuitBreakerSleepWindowInMilliseconds()`), the next single request is let through (this is the `HALF-OPEN` state). If the request fails, the circuit-breaker returns to the `OPEN` state for the duration of the sleep window. If the request succeeds, the circuit-breaker transitions to `CLOSED` and the logic in **1.** takes over again. 经过一段时间后，如果有 1 个尝试成功了，就慢慢尝试恢复
> 
> 参考：https://github.com/Netflix/Hystrix/wiki/How-it-Works#CircuitBreaker

controller:

```
	//====服务熔断
    @GetMapping("/payment/circuit/{id}")
    public String paymentCircuitBreaker(@PathVariable("id")Integer id){
        return paymentService.paymentCircuitBreaker(id);
    }

```

实验效果为，多次出错调用 fallback 后，调用正常的也出错调用 fallback。过了一会又自己恢复了。  
展望：以后用的是 Sentinel 代替。

关于解耦以后的全局配置说明：

例如上面提到的全局服务降级，并且是 feign+hystrix 整合，即 service 实现类的方式，如何做全局配置？

> 上面有 做全局配置时，设置超时时间的方式，我们可以从中获得灵感，即在 yml 文件中 进行熔断配置：
> 
> ```
> hystrix:
> command:
> default:
> circuitBreaker:
>   enabled: true
>   requestVolumeThreshold: 10
>   sleepWindowInMilliseconds: 10000
>   errorThresholdPercentage: 60
> 
> ```

Hystrix DashBoard
-----------------

除了隔离依赖服务的调用以外，Hystrix 还提供了准实时的调用监控 (HystrixDashboard)，Hystrix 会持续地记录所有通过 Hystrix 发起的请求的执行信息，并以统计报表和图形的形式展示给用户，包括每秒执行多少请求多少成功，多少失败等。Netflix 通过 hystrix-metrics-event-stream 实现了对以上指标的监控。SpringCloud 也提供了 HystrixDashboard 的整合，对监控内容转化成可视化界面。

新建模块 cloud-hystrix-dashboard9001 ：

pom 文件：

```
	<dependencies>
        <!-- hystrix Dashboard-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-hystrix-dashboard</artifactId>
        </dependency>
        
        <!-- 常规 jar 包 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <dependency>
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```

yml 文件只需要配置端口号，主启动类加上这样注解：@EnableHystrixDashboard

启动测试：访问 http://ocalhost:9001/hystrix

### 监控实战

> 下面使用上面 9001 Hystrix Dashboard 项目，来监控 8001 项目 Hystrix 的实时情况：

注意 8001 被监控的时候 pom 里要 actuator 依赖，此外还要有

*   主启动类上加`@EnableCircuitBreaker`，用于对豪猪熔断机制的支持

```
@Bean // 注入豪猪的servlet // 该servlet与服务容错本身无关 // springboot默认路径不是/hustrix.stream，只要在自己的项目里自己配置servlet
public ServletRegistrationBean getServlet(){
    HystrixMetricsStreamServlet streamServlet = new HystrixMetricsStreamServlet();
    ServletRegistrationBean servletRegistrationBean = new ServletRegistrationBean(streamServlet);
    servletRegistrationBean.setLoadOnStartup(1);
    servletRegistrationBean.addUrlMappings("/hystrix.stream");
    servletRegistrationBean.setName("HystrixMetricsStreamServlet");
    return servletRegistrationBean;
}

```

然后就可以取页面里看熔断情况了。输入 localhost:8001/hystrix.stream

![](https://img-blog.csdnimg.cn/img_convert/c25ab441fcf34f252a293d95a74871ce.png)

服务网关
====

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

Gateway
-------

> 内容过多，开发可参考 https://docs.spring.io/ 官网文档

### 简介

SpringCloud Gateway 是 SpringCloud 的一个全新项目，基于 Spring5.O+Springboot 2.0 和 ProjectReactor 等技术开发的网关，它旨在为微服务架构提供一种简单有效的统一的 API 路由管理方式。

SpringCloudGateway 作为 SpringCloud 生态系统中的网关，目标是替代 Zuul, 在 SpringCloud2.0 以上版本中，没有对新版本的 zuul2.0 以上最新高性能版本进行集成，仍然还是使用的 Zuul 1.x 非 Reactor 模式的老版本。而为了提升网关的性能，**SpringCloud Gateway 是基于 WebFlux 框架实现的，而 webFlux 框架底层则使用了高性能的 Reactor 模式通信框架 Netty**。

springCloudGateway 的目标提供统一的路由方式且基于 Filter 链的方式提供了网关基本的功能，例如：安全，监控 / 指标，和限流。

一方面因为 Zuul 1.0 已经进入了维护阶段，而且 Gateway 是 SpringCloud 团队研发的是亲儿子产品，值得信赖。而且很多功能比 zull 用起来都简单便捷。

Gateway 是基于异步非阻塞模型上进行开发的，性能方面不需要担心。虽然 Netflix 早就发布了最新的 Zuul2.x，但 Spring Cloud 貌似没有整合计划。而且 Netflix 相关组件都宣布进入维护期；不知前景如何？

多方面综合考虑 Gateway 是很理想的网关选择。

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

SpringCloudGateway 与 Zuul 的区别：

在 SpringCloudFinchley 正式版之前，SpringCloud 推荐的网关是 Netflix 提供的 Zuul：

*   1、Zuul 1.x 是一个基于`阻塞I/O`的 APIGateway  
    2、Zuul 1.x 基于 ServIet2.5 使用阻塞架构，它**不支持任何长连接**（如 WebSocket)，Zuul 的设计模式和 Nginx 较像，每次 I/O 操作都是从  
    工作线程中选择一个执行，请求线程阻塞到工作线程完成，但是差别是 Nginx 用 C++ 实现，Zuul 用 Java 实现，而 JVM 本身会有第一次加载较慢的情况，使得 Zuul 的性能相对较差。
*   3、Zuul 2.x 理念更先进想基于 Netty 非阻塞和支持长连接，但 SpringCloud 目前还没有整合。Zuul2.x 的性能较 Zuul1.x 有较大提升。在性能方面，根据官方提供的基准测试，SpringCloudGateway 的 RPS（每秒请求数）是 Zuul 的 1.6 倍。
*   4、SpringCloudGateway 建立在 SpringFramework5、ProjectReactor 和 SpringB00t2．之上，使用非阻塞 API
*   5、SpringCloudGateway 还支持 WebSocket, 并且与 Spring 紧密集成拥有更好的开发体验

Zuull.x  
springcloud 中所集成的 zuul 版本，采用的是 tomcat 容器，使用的是传统的 servlet IO 处理模型。

学过尚硅谷 web 中期课程都知道一个题目，Servlet 的生命周期，servlet 由 servlet container 进行生命周期管理

*   container 启动时构造 servlet 对象并调用 servlet init() 进行初始化，
*   container 运行时接受请求，并为每个请求分配一个线程（一般从线程池中获取空闲线程）然后调用 service()
*   container 关闭时调用 servlet destory() 销毁 servlet

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

上述模式的缺点：

servlete—个简单的网络 IO 模型，当请求进入 servlet container 时，servlet container 就会为其绑定一个线程在并发不高的场景下这种模型是适用的。但是一旦高并发（比如抽风用 jemeter 压), 线程数量就会上涨，而线程资源代价是昂贵的（上线文切换，内存消耗大）严重影响请求的处理时间。

在一些简单业务场景下，不希望为每个 request 分配一个线程，只需要 1 个或几个线程就能应对极大并发的请求，这种业务场景下 servlet 模型没有优势

所以 Zuul 1.x 是基于 servlet 之上的一个阻塞式处理模型，即 spring 实现了处理所有 request 请求的一个 servlet(DispatcherServlet) 并由该 servlet 阻塞式处理处理。所以 springcloudzuul 无法摆脱 servlet 模型的弊端。

传统的 Web 框架比如说：struts2,springmvc 等都是基于 Servlet API 与 Servlet 容器基础之上运行的。

但是，在 **Servlet3.1 之后有了异步非阻塞的支持**。而 WebFlux 是一个典型**非阻塞异步**的框架，它的核心是基于 Reactor 的相关 API 实现的。相对于传统的 web 框架来说，它可以运行在诸如 Netty，Undertow 及支持 Servlet3.1 的容器上。非阻塞式 + 函数式编程 (Spring5 必须让你使  
用 java8)

SpringWebFlux 是 Spring5.0 引入的新的响应式框架区别于 SpringMVC, 它不需要依赖 ServletAPI，它是完全异步非阻塞的，并且基于 Reactor 来实现响应式流规范。

##### Gateway 是什么

Gateway 特性：

*   基于 SpringFramework5，ProjectReactor 和 SpringBoot 2.0 进行构建；
*   动态路由：能够匹任何请求属性；
*   可以对路由指定 Predicate（断言）和 Filter（过滤器）·
*   集成 Hystrix 的断路器功能；
*   集成 SpringCloud 服务发现功能；
*   易于编写的 Predicate（断言）和 Filter（过滤器）·
*   请求限流功能；
*   支持路径重写。

GateWay 的三大核心概念：

*   Route(路由）：路由是构建网关的基本模块，它由 ID、目标 URI、一系列的断言和过滤器组成，如果断言为 true 则匹配该路由
*   Predicate(断言）：参考的是 Java8 的 java.util.function.predicate。开发人员可以匹配 HTTP 请求中的所有内容（例如请求头或请求参数），如果请求与断言相匹配则进行路由
    *   匹配条件
*   Filter(过滤）：指的是 spring 框架中 GatewayFilter 的实例，使用过滤器，可以在请求被路由前或者之后对请求进行修改。
*   例子：通过`断言`虽然进来了，但老师要罚站 10min（`过滤器`操作），然后才能正常坐下听课

web 请求，通过一些匹配条件，定位到真正的服务节点。并在这个转发过程的前后，进行一些精细化控制。  
而 filter，就可以理解为一个无所不能的拦截器。有了这两个元素，再加上目标 uri，就可以实现一个具体的路由了

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

![](https://img-blog.csdnimg.cn/img_convert/b925eec3db224cb6eee4dea48732e65d.png)

客户端向 Spring Cloud Gateway 发出请求。然后在 Gateway HandlerMapping 中找到与请求相匹配的路由，将其发送到 Gateway Web Handler

Handler 再通过指定的过滤器链来将请求发送到我们实际的服务执行业务逻辑，然后返回。

过滤器之间用虚线分开是因为过滤器可能会在发送代理请求之前（Pre）或之后（post）执行业务逻辑。

`Filter`在 pre 类型的过滤器可以做**参数校验，权限校验，流量监听，日志输出，协议转换**等，

在 post 类型的过滤器中可以做响应内容、响应头的修改，日志的输出，流量监控等有着非常重要的作用。

### 入门配置

新建模块 cloud-gateway-gateway9527

> 现在实现，通过 Gateway (网关) 来访问其它项目，这里选择之前 8001 项目，要求注册进 Eureka Server 。其它没要求。

pom 文件：

```
<dependencies>
        <!--gateway-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-gateway</artifactId>
        </dependency>
        <!--eureka-client gateWay网关作为一种微服务，也要注册进服务中心。哪个注册中心都可以，如zk-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
    <!-- gateway和spring web+actuator不能同时存在，即web相关jar包不能导入 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```

yml 文件：

```
server:
  port: 9527
spring:
  application:
    name: cloud-gateway
  ## GateWay配置
  cloud:
    gateway: 
      routes: #多个路由
        - id: payment_routh  # 路由ID ， 没有固定的规则但要求唯一，建议配合服务名
          uri: http://localhost:8001  # 匹配后提供服务的路由地址 #uri+predicates  # 要访问这个路径得先经过9527处理
          predicates:
            - Path=/payment/get/**  # 断言，路径相匹配的进行路由

        - id: payment_routh2  # 路由ID ， 没有固定的规则但要求唯一，建议配合服务名
          uri: http://localhost:8001  # 匹配后提供服务的路由地址
          predicates:
            - Path=/payment/lb/**  # 断言，路径相匹配的进行路由

# 注册进 eureka Server # 网关他本身也是一个微服务，也要注册进注册主中心
eureka:
  client:
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/
    register-with-eureka: true
    fetch-registry: true

```

> 如果 IDEA 出现了 bug，yml 配置文件没有变为小叶子，就去 structure 里设置下模块的 spring，选择该 yml

主启动类

```
@SpringBootApplication
@EnableEurekaClient
public class GatewayMain9527 {
    public static void main(String[] args) {
        SpringApplication.run(GatewayMain9527.class,args);
    }
}

```

8001 看看 controller 的访问地址，我们目前不想暴露 8001 端口，希望在 8001 外面套一层 9527。这样别人就攻击不了 8001，有网关挡着

访问测试：

*   1 启动 eureka Server，
*   2 启动 8001 项目，
*   3 启动 9527（Gateway 项目）

> 可见，当我们访问 http://localhost:9527/payment/get/1 时，即访问网关地址时，会给我们转发到 8001 项目的请求地址，以此作出响应。
> 
> 加入网关前：http://localhost:8001/payment/get/1
> 
> 加入网关后：http://localhost:9527/payment/get/1

上面是以 yml 文件配置的路由，也有使用 config 类配置的方式：

```
@Configuration
public class GateWayConfig{
    @Bean
    public RouteLocator customRouteLocator(RouteLocatorBuilder routeLocatorBuilder){
        RouteLocatorBuilder.Builder routes = routeLocatorBuilder.routes();

        // 分别是id，本地址，转发到的地址
        routes.route("path_route_atguigu",
                r -> r.path("/guonei").uri("http://news.baidu.com/guonei")
                    ).build();//JDK8新特性

        return routes.build();
    }
}

```

```
@Component
@Slf4j
public class MyLogGateWayFilter implements GlobalFilter,Ordered {

    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        log.info("***********come in MyLogGateWayFilter:  "+new Date());

        String uname = exchange.getRequest().getQueryParams().getFirst("uname");

        if(uname == null) {
            log.info("*******用户名为null，非法用户，o(╥﹏╥)o");
            exchange.getResponse().setStatusCode(HttpStatus.NOT_ACCEPTABLE);
            return exchange.getResponse().setComplete();
        }

        return chain.filter(exchange);
    }

    @Override
    public int getOrder() {
        return 0;
    }
}

```

### 动态配置

> 这里所谓的动态配置就是利用服务注册中心，来实现 负载均衡 的调用 多个微服务。
> 
> 默认情况下 gateway 会根据注册中心注册的服务列表，以注册中心上微服务名为路径创建动态路由进行转发，从而实现动态路由的功能
> 
> 注意，这是 GateWay 的负载均衡

对 yml 进行配置：让其先通过 gateway，再通过 gateway 去注册中心找提供者

```
server:
  port: 9527

spring:
  application:
    name: cloud-gateway
  cloud:
    gateway:
      discovery:
        locator:
          enabled: true # 开启从注册中心动态创建路由的功能，利用微服务名进行路由
      routes:
        - id: payment_routh  # 路由ID ， 没有固定的规则但要求唯一，建议配合服务名
         # uri: http://localhost:8001  # 匹配后提供服务的路由地址 
          uri: lb://CLOUD-PROVIDER-SERVICE # lb 属于GateWay 的关键字，代表是动态uri，即代表使用的是服务注册中心的微服务名，它默认开启使用负载均衡机制 
          predicates:
            - Path=/payment/get/**  # 断言，路径相匹配的进行路由

        - id: payment_routh2  # 路由ID ， 没有固定的规则但要求唯一，建议配合服务名
        #  uri: http://localhost:8001  # 匹配后提供服务的路由地址
          uri: lb://CLOUD-PROVIDER-SERVICE
          predicates:
            - Path=/payment/lb/**  # 断言，路径相匹配的进行路由

# uri: lb://CLOUD-PROVIDER-SERVICE  解释：lb 属于GateWay 的关键字，代表是动态uri，即代表使用的是服务注册中心的微服务名，它默认开启使用负载均衡机制 

eureka:
  instance:
    hostname: cloud-gateway-service
  client: #服务提供者provider注册进eureka服务列表内
    service-url:
      register-with-eureka: true
      fetch-registry: true
      defaultZone: http://eureka7001.com:7001/eureka

```

> 下面可以开启 8002 模块，并将它与 8001 同微服务名，注册到 Eureka Server 进行测试。

### Gateway:Predicate

> 注意到上面 yml 配置中，有个 predicates 属性值。

*   1 After Route Predicate
*   2 Before Route Predicate
*   3 Between Route Predicate
*   4 Cookie Route Predicate
*   5 Header Route Predicate
*   6 Host Route Predicate
*   7 Method Route Predicate
*   8 Path Route Predicate
*   9 Query Route Predicate

具体使用：

```
spring:
  application:
    name: cloud-gateway
  cloud:
    gateway:
      discovery:
        locator:
          enabled: true #开启从注册中心动态创建路由的功能，利用微服务名进行路由
      routes:
        - id: payment_routh #payment_route    #路由的ID，没有固定规则但要求唯一，建议配合服务名
          #uri: http://localhost:8001          #匹配后提供服务的路由地址
          uri: lb://cloud-payment-service #匹配后提供服务的路由地址
          predicates:
            - Path=/payment/get/**         # 断言，路径相匹配的进行路由

        - id: payment_routh2 #payment_route    #路由的ID，没有固定规则但要求唯一，建议配合服务名
          #uri: http://localhost:8001          #匹配后提供服务的路由地址
          uri: lb://cloud-payment-service #匹配后提供服务的路由地址
          predicates:
            - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
            #- After=2020-02-21T15:51:37.485+08:00[Asia/Shanghai]
            #- Cookie=username,zzyy
            #- Header=X-Request-Id, \d+  # 请求头要有X-Request-Id属性并且值为整数的正则表达式

```

predicates 下面可以有多个属性，表示多个属性与操作为 true 这个路由才生效

predicates 属性下的 After 属性

```
		predicates:
            - Path=/payment/lb/** 
            - After=2020-02-21T15:51:37.485+08:00[Asia/Shanghai] # 会在这个时间之后这个路由才生效

```

predicates 属性下的 Cookie 属性

```
predicates:
	- Cookie=username,zzyy,ch.p # 需要有这个Cookie值才生效  最后一个是正则表达式
	# curl 地址 --cookie "a=b"

```

predicates 属性下的 Header 属性

```
spring:
  cloud:
    gateway:
      routes:
      - id: header_route
        uri: https://example.org
        predicates:
        - Header=X-Request-Id, \d+

```

```
spring:
  cloud:
    gateway:
      routes:
      - id: host_route
        uri: https://example.org
        predicates:
        - Host=**.somehost.org,**.anotherhost.org  # Host Route Predicate Factory接收一组参数，一组匹配的域名列表，这个模板是一个ant分隔的模板，用.号作为分隔符。它通过参数中的主机地址作为匹配规则
        
        
        # 放爬虫思路，前后端分离的话，只限定前端项目主机访问，这样可以屏蔽大量爬虫。

例如我加上： - Host=localhost:**       ** 代表允许任何端口

就只能是主机来访

```

更多属性可以参考：https://docs.spring.io/spring-cloud-gateway/docs/2.2.5.RELEASE/reference/html/#configuring-route-predicate-factories-and-gateway-filter-factories

需要注意的是 value 部分写的是正则表达式

高并发工具：jmeter、postman、curl

配置错误页面:

> 注意，springboot 默认 / static/error/ 下错误代码命名的页面为错误页面，即 404.html
> 
> 而且不需要导入额外的包，Gateway 里面都有。

### Gateway:Filter

生命周期：

*   pre：
*   post：

种类：

*   GatewayFilter：https://docs.spring.io/spring-cloud-gateway/docs/2.2.5.RELEASE/reference/html/#gatewayfilter-factories
*   GlobalFilter：https://docs.spring.io/spring-cloud-gateway/docs/2.2.5.RELEASE/reference/html/#global-filters

```
spring:
  cloud:
    gateway:
      routes:
      - id: add_request_header_route
        uri: https://example.org
        filters:
        - AddRequestHeader=X-Request-red, blue # 添加了个请求头X-Request-red

```

主要是配置全局自定义过滤器，其它的小配置具体看官网吧

2 个主要接口：`implements GlobalFilter,Ordered`

场景：

*   全局日志记录
*   统一网关鉴权
*   。。。

自定义全局过滤器配置类：

```
@Component
@Slf4j
public class MyLogGateWayFilter implements GlobalFilter,Ordered {

    @Override
    public Mono<Void> filter(ServerWebExchange exchange,
        GatewayFilterChain chain) {

        log.info("********** come in MyLogGateWayFilter:  "+new Date());

        String uname = exchange.getRequest().getQueryParams().getFirst("uname");

        //合法性检验
        if(uname == null) {
            log.info("*******用户名为null，非法用户，o(╥﹏╥)o，请求不被接受");
            //设置 response 状态码   因为在请求之前过滤的，so就算是返回NOT_FOUND 也不会返回错误页面
            exchange.getResponse().setStatusCode(HttpStatus.NOT_ACCEPTABLE);
            //完成请求调用
            return exchange.getResponse().setComplete();
        }

        return chain.filter(exchange);//过滤链放行
    }

    // 返回值是加载顺序，一般全局的都是第一位加载
    @Override
    public int getOrder() {
        return 0;
    }
}

```

服务配置
====

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

Config
------

> SpringCloud Config 分布式配置中心

### 概述

微服务意味着要将单应用中的业务拆分成一个个子服务，每个服务的粒度相对较小，因此系统中会出现大量的服务。由于每个服务都需要必要的配置信息才能运行，所以一套集中式的、动态的配置管理设施是必不可少的。

springCloud 提供了 ConfigServer 来解决这个问题，我们每一个微服务自己带着一个 application.yml，上百个配置文件的管理。比如数据库的信息，我们可以写到一个统一的地方。

*   config+bus
*   alibaba nacos
*   携程 阿波罗

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

SpringCloud Config 是什么：Spring Cloud Config 为微服务架构中的微服务提供集中化的外部配置支持，配置服务器为各个不同微服务应用的所有环境提供了一个**中心化的外部配置**。

怎么玩：  
SpringCloud Config 分为服务端和客户端两部分。

*   服务端也称为分布式配置中心，它是一个独立的微服务应用，用来连接配置服务器并为客户端提供获取配置信息，加密 / 解密信息等访问接口
*   客户端则是通过指定的配置中心来管理应用资源，以及与业务相关的配置内容，并在启动的时候从配置中心取和加载配置信息配置服务器默认采用 git 来存储配置信息，这样就有助于对环境配置进行版本管理，并且可以通过 git 客户端工具来方便的管理和访问配置内容

能干嘛：

*   集中管理配置文件
*   不同环境不同配置，**动态化的配置更新**，分环境部署比如 dev/test/prod/beta/release
*   运行期间动态调整配置，不再需要在每个服务部署的机器上编写配置文件，服务会向配置中心统一拉取配置自己的信息
*   当配置发生变动时，服务不需要重启即可感知到配置的变化并应用新的配置
*   将配置信息以 REST 接囗的形式暴露

### config 服务端配置

这个服务端指的是消费端与 github 之间的桥接

> 首先在 github 上新建一个仓库 springcloud-config
> 
> git@github.com: 名字 / 项目. git
> 
> 然后使用 git 命令克隆到本地，命令：git clone https://github.com/LZXYF/springcloud-config
> 
> 注意上面的操作不是必须的，只要 github 上有就可以，克隆到本地只是修改文件。
> 
> 常用命令：
> 
> *   git add
> *   git commit -m “标记”
> *   git push origin master

在 git 根目录下创建

*   开发环境：config-dev.yml
*   生产环境：config-pro.yml
*   测试环境：config-test.tml

注意格式

新建 `cloud-config-center3344` 模块：

pom 文件：

```
	<dependencies>
        <!-- config Server -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-config-server</artifactId>
        </dependency>

        <!--eureka-client config Server也要注册进服务中心-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```

yml 配置：

```
server:
  port: 3344

spring:
  application:
    name:  cloud-config-center #注册进Eureka服务器的微服务名
  cloud:
    config:
      server:
        git: # 此处使用的是老师是配置中心
          uri: git@github.com:zzyybs/springcloud-config.git #GitHub上面的git仓库名字
          ####搜索目录
          search-paths:
            - springcloud-config
      ####读取分支
      label: master
      
#服务注册到eureka地址
eureka:
  client:
    service-url:
      defaultZone: http://localhost:7001/eureka

```

主启动类：

```
@SpringBootApplication
@EnableConfigServer   //关键注解
public class ConfigCenterMain3344 { // 注意先去把Eureka启动起来
    public static void main(String[] args) {
        SpringApplication.run(ConfigCenterMain3344.class,args);
    }
}

```

添加模拟映射：【C:\Windows\System32\drivers\etc\hosts】文件中添加： `127.0.0.1 config-3344.com`

启动微服务 3344，访问 http://config-3344.com:3344/master/config-dev.yml 文件（注意，要提前在 git 上弄一个这文件）

老师的配置中心地址：https://github.com/zzyybs/springcloud-config

文件命名和访问的规则：

![](https://img-blog.csdnimg.cn/img_convert/df118f6e915a845d5c71400938260c1b.png)

不加分支名默认是 master:

![](https://img-blog.csdnimg.cn/img_convert/329f61d194f7839a55f37b5a65b70667.png)

最后一个出的是 json 串

*   label：分支 branch
*   name：服务名
*   profiles：环境 dev/test/prod

### config 客户端配置

> 这里的客户端指的是，使用 Config Server 统一配置文件的项目。既有之前说的消费者，又有提供者

新建 `cloud-config-client-3355` 模块：

pom 文件：

```
	<dependencies>
        <!-- config Client 和 服务端的依赖不一样 -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
        </dependency>

        <!--eureka-client config Server也要注册进服务中心-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```

要将 Client 模块下的 application.yml 文件改为 bootstrap.yml，删掉 application.yml 这是很关键的

因为 bootstrap.yml 是比 application.yml 先加载的。bootstrap.yml 优先级高于 application.yml

appllication.yml 是用户级的资源配置项

bootstrap.ym1 是系统级的，优先级更加高

SpringCloud 会创建一个 "Bootstrap Context" 作为 Spring 应用的 ApplicationContext 的`父上下文`。初始化的时候，Bootstrap Context 负责从外部源加载配置属性并解析配置。这两个上下文共享一个从外部获取的 Environment

Bootstrap 属性有高优先级，默认情况下，它们不会被本地配置覆盖。BootstrapContext 和 ApplicationContext、有着不同的约定，所以新增了一个 bootstrap.yml 文件，保证 BootstrapContext 和 ApplicationContext 配置的分离。

bootstrap.yml 文件：

```
server:
  port: 3355

spring:
  application:
    name: config-client
  cloud:
    #Config客户端配置
    config:
      label: master #分支名称
      name: config #配置文件名称，文件也可以是client-config-dev.yml这种格式的，这里就写 client-config 
      profile: dev #读取后缀名称   上述3个综合：master分支上config-dev.yml的配置文件被读取http://config-3344.com:3344/master/config-dev.yml
      uri: http://localhost:3344 #配置中心地址
      # 综合上面四个 即读取配置文件地址为： http://config-3344.com:3344/master/config-dev.yml

#服务注册到eureka地址
eureka:
  client:
    service-url:
      defaultZone: http://localhost:7001/eureka

```

主启动类，极其普通：

```
@SpringBootApplication
@EnableEurekaClient
public class ConfigClientMain3355 
    public static void main(String[] args) {
        SpringApplication.run(ConfigClientMain3355.class, args);
    }
}

```

controller 层，测试读取配置信息

```
package com.dkf.springcloud.controller;

@RestController
public class ConfigClientController {

    @Value("${config.info}") // 消费 //相当于配置了config后，就把config服务端里的变量引入进来了
    private String configInfo;

    @GetMapping("/configInfo")
    public String getConfigInfo(){
        return configInfo;
    }
}

```

启动测试完成！如果报错，注意 github 上的 yml 格式有没有写错！

启动 Config 配置中心 3344 微服务并自测，启动 3355 作为 client 访问 localhost:3355/configInfo

修改 config-dev.yml 配置文件并提交到 github 中，比如加个变量 age 或者版本号 version。更改消费者端的配置看看其他环境能不能用

### 动态刷新

问题：

*   Linux 运维修改 GitHub 上的配置文件内容做调整：比如修改 config-dev.yml 提交
*   刷新 3344，发现 ConfigServer 服务端配置中心立刻响应，得到最新值了
*   刷新 3355，发现 ConfigClient 客户端没有任何响应，拿到的还是旧值
*   客户端 3355 没有变化除非自己重启或者重新加载，才能拿到最新值
*   难到每次运维修改配置文件，**客户端**都需要重启？？噩梦

> 就是 github 上面配置更新了，config Server 项目上是动态更新的，但是，client 端的项目中的配置，目前还是之前的，它不能动态更新，必须重启才行。

动态刷新问题解决：

1.  client 端一定要有 actuator 依赖：
    
    ```
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    
    ```
    
2.  client 端增加 yml 配置如下，即在 bootstrap.yml 文件中：
    

```
server:
  port: 3355

spring:
  application:
    name: config-client
  cloud:
    #Config客户端配置
    config:
      label: master #分支名称
      name: config #配置文件名称
      profile: dev #读取后缀名称   上述3个综合：master分支上config-dev.yml的配置文件被读取http://config-3344.com:3344/master/config-dev.yml
      uri: http://localhost:3344 #配置中心地址k

#服务注册到eureka地址
eureka:
  client:
    service-url:
      defaultZone: http://localhost:7001/eureka

# 暴露监控端点
management:
  endpoints:
    web:
      exposure:
        include: "*"

```

3.  在 controller 上添加注解`@RefreshScope`：
    
    ```
    @RestController
    @RefreshScope //这个注解
    public class ConfigClientController {
        @Value("${config.info}")
        private String configInfo;
    
        @GetMapping("/configInfo")
        public String getConfigInfo() {
            return configInfo;
        }
    }
    
    ```
    

> 到此为止，配置已经完成，但是测试客户端 localhost:3355/configInfo 仍然不能动态刷新，还是旧值（也就是说环境变量里的还是旧值），需要下一步。

4.  向 client 端发送一个 POST 请求

> 如 curl -X POST “http://localhost:3355/actuator/refresh”
> 
> 两个必须：1. 必须是 POST 请求，2. 请求地址：http://localhost:3355/actuator/refresh

成功获得到最新值

但是又有一个问题，就是要向每个微服务客户端发送一次 POST 请求，当微服务数量庞大，又是一个新的问题。

能否广播，一次通知，处处生效？（还要求不要全广播，差异化管理，定点清除，20 台只有 18 台更新）

就有下面的消息总线！

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

消息总线
====

消息总线的由来看上面一小节

Bus
---

spring cloud Bus 配置 spring cloud Config 使用可以实现配置的动态刷新

spring cloud bus 是用来将分布式系统的节点与轻量级消息系统链接起来的框架，它整合了 java 的事件处理机制和消息中间件的功能。

spring cloud bus 目前支持 RabbitMQ 和 Kafka（因为是主题订阅）

什么是总线

在微服务架构的系统中，通常会使用轻量级的消息代理来构建一个共用的消息主题，并让系统中所有微服务实例都连接上来。由于该主题中产生的消息会被所有实例**监听和消费**，所以称它为消息总线。在总线上的各个实例，都可以方便地广播一些需要让貝他连接在该主题上的实例都知道的消息。

基本原理：

`ConfigClient`实例都监听 MQ 中同一个 topic 主题 (默认是`springCloud Bus`)。当一个服务刷新数据的时候，它会把这个信息放入到 Topic 中，这样其它监听同一 topic 的服务就能得到通知，然后去更新自身的配置

下图原盈利是就是给其中一台发送我们的刷新 POST，他刷新完后给 Bus 发消息，然后 Bus 通过消息中间件发送给 BC 进行更新

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

Bus 能管理和传输分布式系统间的消息，就像一个分布式执行器，可用于广播状态更改、事件推送等，也可以当做微服务间的通信通道

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

### RabbitMQ

> 在 windows 上安装 RabbitMQ

1.  安装 RabbitMQ 的依赖环境 Erlang 下载地址： http://erlang.org/download/otp_win64_21.3.exe
2.  安装 RabbitMQ 下载地址： http://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.14/rabbitmq-server-3.7.14.exe
3.  进入 rabbitMQ 安装目录的 sbin 目录下，打开 cmd 窗口，执行 【`rabbitmq-plugins enable rabbitmq_management`】
4.  访问【http://localhost:15672/】，输入密码和账号：默认为 guest

### 广播式刷新配置

*   必须先具有良好的 RabbitMQ 环境
*   演示广播效果，增加复杂度，再以 3355 为模板再制作一个 3366
*   设计思想
    *   1）利用消息总线触发一个客户端 / bus/refresh，而刷新所有客户端的配置
    *   2）利用消息总线触发一个服务端 ConfigServer 的 / bus/refres 端点，从而刷新所有客户端的配置
    *   ![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)
    *   图二的架构显然更加适合，图一不适合的原因如下
        *   打破了微服务的职责单一性，因为微服务本身是业务模块，它本不应该承担配置刷新的职责
        *   破坏了微服务各节点的对等性。
        *   有一定的局限性 “例如，微服务在迁移时，它的网络地址常常会发生变化，此时如果想要做到自动刷新，那就会增加更多的
*   给 cloud-config-center-3344 配置中心服务端添加消息总线支持
*   给 cloud-config-client-3355 客户端添加消息总线支持
*   给 cloud-config-client-3366 客户端添加消息总线支持（以 3355 为模板）
*   测试
*   一次修改，广播通知，出处生效
*   但还是得发一个 POST 请求，只不过只给 config 发而已

首先给 config Server 和 config client 都添加如下依赖：

```
<!-- 添加rabbitMQ的消息总线支持包 -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bus-amqp</artifactId>
</dependency>

```

config Server 的 yml 文件增加如下 rabbitmq 配置：

```
# rabbitMq的相关配置
rabbitmq:
  host: localhost
  port: 5672  # 这里没错，虽然rabbitMQ网页是 15672
  username: guest
  password: guest
# rabbitmq 的相关配置2 暴露bus刷新配置的端点
management:
  endpoints:
    web:
      exposure:
        include: 'bus-refresh'

```

config Client 的 yml 文件修改成如下配置：（注意对齐方式，和 config Server 不一样）

```
spring:
  cloud:
    # config 客户端配置
    config:
      label: master         # 分支名称
      name: client-config       # 配置文件名称
      profile: test      # 使用配置环境
      uri: http://config-3344.com:3344  # config Server 地址

```

3355 客户端的 bootstrap.yml

```
server:
  port: 3355 # client

spring:
  application:
    name: config-client
  cloud:
    #Config客户端配置
    config:
      label: master #分支名称
      name: config #配置文件名称
      profile: dev #读取后缀名称   上述3个综合：master分支上config-dev.yml的配置文件被读取http://config-3344.com:3344/master/config-dev.yml
      uri: http://localhost:3344 #配置中心地址k

#rabbitmq相关配置 15672是Web管理界面的端口；5672是MQ访问的端口
  rabbitmq:
    host: localhost
    port: 5672
    username: guest
    password: guest

#服务注册到eureka地址
eureka:
  client:
    service-url:
      defaultZone: http://localhost:7001/eureka

# 暴露监控端点
management:
  endpoints:
    web:
      exposure:
        include: "*"

```

3344 注册中心的 application.yml

```
server:
  port: 3344

spring:
  application:
    name:  cloud-config-center #注册进Eureka服务器的微服务名
  cloud:
    config:
      server:
        git:
          uri: git@github.com:zzyybs/springcloud-config.git #GitHub上面的git仓库名字
        ####搜索目录
          search-paths:
            - springcloud-config
      ####读取分支
      label: master
#rabbitmq相关配置
rabbitmq:
    host: localhost
    port: 5672
    username: guest
    password: guest

#服务注册到eureka地址
eureka:
  client:
    service-url:
      defaultZone: http://localhost:7001/eureka

##rabbitmq相关配置,暴露bus刷新配置的端点
management:
  endpoints: #暴露bus刷新配置的端点
    web:
      exposure:
        include: 'bus-refresh'

```

可在 github 上修改 yml 文件进行测试，修改完文件，向 config server 发送 请求：

给 3344 发就能全局同步了【curl -X POST “http://localhost:3344/actuator/bus-refresh”】

> 注意，之前是向 config client 一个个发送请求，但是这次是向 config Server 发送请求，而所有的 config client 的配置也都全部更新。

### 定点通知

新的需求：指定具体某一个实例（的参数）生效而不是全部，一些是最新值，一些是旧值

*   公式：`http://localhost:配置中心的端口号/actuator/bus-refresh/{destination}`
    
*   例子：curl -X POST "http//localhost:3344/actuator/bus-refresh/config-client:3355
    
*   即微服务名称 + 端囗号
    
*   /bus/refresh 请求不再发送到具体的服务实例上，而是发给 configserver 并通过 destination 参数类指定需要更新配置的服务或实例
    
*   我们这里以刷新运行在 3355 端口上的 config-client 为例
    
    *   只通知 3355
    *   不通知 3366

消息驱动
====

Stream
------

需求：消息中间件很多，希望向上抽象一个接口，我们不关心底层用的是什么消息中间件

屏蔽底层消息中间件的差异，降低切换成本，统一消息的编程模型

就像 JDBC 形成一种规范，统一不同数据库的接口

![](https://img-blog.csdnimg.cn/img_convert/d1710ba414fcbc3720ffea05aee186b5.png)

什么是 SpringCloud Stream

官方定义 SpringCloud Stream 是一个构建消息驱动微服务的框架。https://spring.io/projects/spring-cloud-stream#overview

应用程序通过 inputs 或者 outputs 来与 SpringCloud Stream 中 binder 对象（绑定器）交互

涌过我们配置来 binding（绑定）而 SpringCloud Stream 的 binder 对象负责与消息中间件交互。

所以，我们只需要搞清楚如何与 springCloudstrearn 交互就可以方便使用消息驱动的方式。

通过使用 Spring Integration 来连接消息代理中间件以实现消息事件驱动。

SpringCloud Stream 为一些供应商的消息中间件产品提供了个性化的自动化配置实现，引用了发布 - 订阅、消费组、分区的三个核心概念

目前仅支持 RabbitMQ、Kafka。

> 流程：
> 
> pub 生产者发送消息，BROKER 接收消息放到队列中，订阅者接收到消息
> 
> 选修必须走特定的通道：下嘻嘻通道 MessageChannel
> 
> 消息通道里的消息如何消费呢？谁负责收发处理：消息通道 MessageChannel 的子接口 SubscribableChannel，由 MessageHandler 消息处理器所订阅
> 
> 比如 java 里用的是 RabbitMQ，大数据里用的是 kafka，来回切换麻烦，链各个消息中间件的架构上不同
> 
> 像 RabbitMQ 有 exchange，kafka 有 Topic 和 Partitions 分区
> 
> 这些中间件的差异导致我们实际项目开发给我们造成了一定的困难，我们如果用了两个消息队列的其中一种，后面的业务需求，我们想往另外一种消息队列进行迁移，这时候无疑就是一个灾难性的，一大堆东西都要重新推倒重新做，因为它跟我们的系统耦合了，这时候 SpringCloud Stream 给我们提供了一种解耦合的方式。

Stream 的消息通信方式遵循了**发布 - 订阅模式**

通过定义绑定器 Binder 作为中间层，实现了应用程序与消息中间件细节之间的隔离。INPUT 对应于生产者，OUTPUT 对应于消费者

![](https://img-blog.csdnimg.cn/img_convert/65fa5f0d45eba8e13f3c3d5614eae009.png)

Stream 标准流程套路：

*   binder：很方便的连接中间件，屏蔽差异
*   Channel：通道，是队列 Queue 的一种抽象，在消息通讯系统中就是实现存储和转发的媒介，通过 channel 对队列进行配置
*   Source（生产）和 sink（消费）：简单地可理解为参照对象是 spring cloud stream 自身，从 stream 发布消息就是输出，接收消息就是输入

![](https://img-blog.csdnimg.cn/img_convert/074eeb14cc99b7067376138d25cc750b.png)

常用注解：

<table><thead><tr><th>组成</th><th>说明</th></tr></thead><tbody><tr><td>Middleware</td><td>中间件，目前只支 FRabbitMQ 和 Kafka</td></tr><tr><td>Binder</td><td>Binder 是应用与消息中间件之间的封装，目前实行了 KafKa 和 RabbitMQ 的 Binder, 通过<br>Binder 可以很方便的连接中间件，可以动态的改变消息类型（对应 kafka 的 topic，<br>RabbitMQ 的 exchange)，这些都可以通过配置文件来实现</td></tr><tr><td>@Input</td><td>注解标识输入通道，通过该输入通接收到的消息息进入应用程序</td></tr><tr><td>@Output</td><td>注解标识输出通道，发布的消息将通过该通道离开应用程序</td></tr><tr><td>@StreamListener</td><td>监听队列，用于消费者的队列的消息接收</td></tr><tr><td>@EnableBinding</td><td>指信道 channel 和 exchange 绑定在一起</td></tr></tbody></table>

### 消息生产者

要新建 3 个子模块

*   cloud-stream-rabbitmq-provide8801：作为生产者进行发消息模块
*   cloud-stream-rabbitmq-consumer8802：作为消息接收模块
*   cloud-stream-rabbitmq-consumer8802：作为消息接收模块

新建模块 cloud-stream-rabbitmq-provider8801

8801 pom 依赖：

```
<!-- stream-rabbit -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-stream-rabbit</artifactId>
</dependency>

<!--eureka-client 目前，这个不是必须的-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
    <optional>true</optional>
</dependency>
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <optional>true</optional>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
<dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
    <groupId>com.dkf.cloud</groupId>
    <artifactId>cloud-api-commons</artifactId>
    <version>${project.version}</version>
</dependency>

```

yml 配置：

```
server:
  port: 8801
  
spring:
  application:
    name: cloud-stream-provider
  cloud:
    stream:
      binders: # 在此配置要绑定的rabbitMQ的服务信息
        defaultRabbit: # 表示定义的名称，用于和binding整合
          type: rabbit  # 消息组件类型
          environment:  # 设置rabbitmq的相关环境配置
            spring:
              rabbitmq:
                host: localhost
                port: 5672
                username: guest
                password: guest
      bindings:  # 服务的整合处理
        output:   # 表示是生产者，向rabbitMQ发送消息
          destination: studyExchange  # 表示要使用的Exchange名称
          content-type: application/json  # 设置消息类型，本次是json，文本是 "text/plain"
          binder: defaultRabbit  # 设置要绑定的消息服务的具体配置
          
eureka:
  client:
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/
  instance:
    lease-renewal-interval-in-seconds: 2 # 设置心跳时间，默认是30秒
    lease-expiration-duration-in-seconds: 5 # 最大心跳间隔不能超过5秒,默认90秒
    instance-id: send-8801.com # 在信息列表显示主机名称
    prefer-ip-address: true # 访问路径变为ip地址

```

主启动类没什么特殊的注解。

业务类：（此业务类不是以前的 service，而实负责推送消息的服务类）

*   发送消息的接口类
*   发送消息接口类的实现类
*   controller

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

```
package com.atguigu.springcloud.service;

public interface IMessageProvider {
    public String send();
}

```

```
package com.dkf.springcloud.service;

import org.springframework.cloud.stream.annotation.EnableBinding;
import org.springframework.cloud.stream.messaging.Source;
import org.springframework.messaging.MessageChannel;
import org.springframework.messaging.support.MessageBuilder;

import javax.annotation.Resource;
import java.util.UUID;

@EnableBinding(Source.class)  // 定义消息的推送管道 output//不是和controller打交道的service,而是发送消息的推送服务类
public class IMessageProviderImpl implements IMessageProvider {
									     //上面是自定义的接口
    @Resource
    private MessageChannel output;//消息发送管道

    @Override
    public String send() {
        String serial = UUID.randomUUID().toString();
        output.send(MessageBuilder.withPayload(serial).build());// 绑定器
        System.out.println("******serial: " + serial);
        return null;
    }
}

```

controller:

```
@RestController
public class SendMessageController {

    @Resource // 自己的类
    private IMessageProvider messageProvider;

    @GetMapping("/sendMessage")
    public String sendMessage(){
        return messageProvider.send(); // 自己定义的方法，但是里面调用了MessageChannel.send()方法
    }
}

```

> 启动 Eureka Server 7001，再启动 8801，进行测试，看是否 rabbitMQ 中有我们发送的消息。

### 消息消费者

新建模块 cloud-stream-rabbitmq-consumer8802

pom 依赖和生产者一样。

yml 配置: 在 stream 的配置上，和生产者只有一处不同的地方，output 改成 input

```
server:
  port: 8802
spring:
  application:
    name: cloud-stream-provider
  cloud:
    stream:
      binders: # 在次配置要绑定的rabbitMQ的服务信息
        defaultRabbit: # 表示定义的名称，用于和binding整合
          type: rabbit  # 消息组件类型
          environment:  # 设置rabbitmq的相关环境配置
            spring:
              rabbitmq:
                host: localhost
                port: 5672
                username: guest
                password: guest
      bindings:  # 服务的整合处理
        input:   # 表示是消费者，这里是唯一和生产者不同的地方，向rabbitMQ发送消息
          destination: studyExchange  # 表示要使用的Exchange名称
          content-type: application/json  # 设置消息类型，本次是json，文本是 "text/plain"
          binder: defaultRabbit  # 设置要绑定的消息服务的具体配置
eureka:
  client:
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/
  instance:
    lease-renewal-interval-in-seconds: 2 # 设置心跳时间，默认是30秒
    lease-expiration-duration-in-seconds: 5 # 最大心跳间隔不能超过5秒,默认90秒
    instance-id: receive-8802.com # 在信息列表显示主机名称
    prefer-ip-address: true # 访问路径变为ip地址

```

接收消息的业务类：

```
import org.springframework.cloud.stream.annotation.EnableBinding;
import org.springframework.cloud.stream.annotation.StreamListener;
import org.springframework.cloud.stream.messaging.Sink;
import org.springframework.messaging.Message;

@Component
@EnableBinding(Sink.class)
public class ConsumerController {

    @Value("${server.port}")
    private String serverPort;

    @StreamListener(Sink.INPUT) // 消费者
    public void input(Message<String> message){
        System.out.println("消费者1号，serverport: " + serverPort + "，接受到的消息：" + message.getPayload());
    }
}

```

### 配置分组消费

新建 cloud-stream-rabbitmq-consumer8802 模块：

> 8803 就是 8802 clone 出来的。

当运行时，会有两个问题。

第一个问题，两个消费者都接收到了消息，这属于重复消费。例如，消费者进行订单创建，这样就创建了两份订单，会造成系统错误。

注意在 stream 中处同一个 group 中的多个消费者是竞争关系，就能保证消息只会被其中一个应用消费一次。

不同组是可以全面消费（重复消费）的

同一组内会发生竞争关系，只有其中一个可以消费。

> Stream 默认不同的微服务是不同的组

![](https://img-blog.csdnimg.cn/img_convert/e8673ce5d424abd401f623b921773667.png)

对于重复消费这种问题，导致的原因是默认每个微服务是不同的 group，组流水号不一样，所以被认为是不同组，两个都可以消费。

解决的办法就是自定义配置分组：

消费者 yml 文件配置：

```
	# 8802 的消费者
	bindings:
        input:   
          destination: studyExchange  
          content-type: application/json  
          binder: defaultRabbit  
          group: dkfA  # 自定义分组配置
          
    # 8803 的消费者
	bindings:
        input:   
          destination: studyExchange  
          content-type: application/json  
          binder: defaultRabbit  
          group: dkfB  # 自定义分组配置

```

[外链图片转存失败, 源站可能有防盗链机制, 建议将图片保存下来直接上传 (img-Uo13s2dc-1615737211158)(images\1597732035990.png)]

当两个消费者配置的 group 都为 dkfA 时，就属于同一组，就不会被重复消费。（两个消费者消费同一队列）

[外链图片转存失败, 源站可能有防盗链机制, 建议将图片保存下来直接上传 (img-ox51Z2Z5-1615737211160)(images\1597732238270.png)]

### 消息持久化

> 加上 group 配置，就已经实现了消息的持久化。

Sleuth
======

> 分布式请求链路跟踪，超大型系统。需要在微服务模块极其多的情况下，比如 80 调用 8001 的，8001 调用 8002 的，这样就形成了一个链路，如果链路中某环节出现了故障，我们可以使用 Sleuth 进行链路跟踪，从而找到出现故障的环节。

在微服务框架中，一个由客户端发起的请求在后端系统中会经过多个不同的的服务节点调用来协同产生最后的请求结果，每一个前段请求都会形成一条杂的分布式服务调用链路，链路中的亻刊可一环出现高延时或错误都会引起整个请求最后的失败。

> sleuth 负责跟踪，而 zipkin 负责展示。
> 
> zipkin 下载地址： http://dl.bintray.com/openzipkin/maven/io/zipkin/java/zipkin-server/2.12.9/zipkin-server-2.12.9-exec.jar
> 
> 使用 【java -jar】 命令运行下载的 jar 包，访问地址：【 http://localhost:9411/zipkin/ 】

案例
--

> 使用之前的 提供者 8001 和 消费者 80

分别给他们引入依赖：

```
	<!-- 引入sleuth + zipkin -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-zipkin</artifactId>
        </dependency>

```

yml 增加配置：

```
spring:
  zipkin:
    base-url: http://localhost:9411  # zipkin 地址
  sleuth:
    sampler:
      # 采样率值 介于0-1之间 ，1表示全部采集
      probability: 1

```

高级部分
====

SpringCloud Alibaba
===================

> alibaba 的 github 上有中文文档

spring netflix 进入维护模式。

什么是维护模式：spring cloud 团队将不会再向模块添加新功能，我们将修复 block 级别的 bug 以及安全问题，我们也会考虑并审查社区的小型 pull request。我们打算继续支持这些模块，知道 Greenwich 版本被普遍采用至少一年

SpringCloud Netflix 将不再开发新的组件

以下 spring cloud netflix 模块和响应的 starter 将进入维护模式：

*   spring-cloud-netflix-archaius
*   spring-cloud-netflix-hystrix-contract
*   spring-cloud-netflix-hystrix-dashboard
*   spring-cloud-netflix-hystrix-stream
*   spring-cloud-netflix-hystrix
*   spring-cloud-netflix-ribbon
*   spring-cloud-netflix-turbine-stream
*   spring-cloud-netflix-turbine
*   spring-cloud-netflix-zuul

这不包括 Eureka 或并发限制模块。

我们都知道 SpringCloud 版本迭代是比较快的，因而出现了很多重大 ISSUE 都还来不及 Flix 就又推另一个 RELEASE 了。进入维护模式意思就是目前以及以后一段时间 SpingCloud Netflix 提供的报务和功能就这么多了，不在开发新的组件和功能了。以后将以雏护和 Merge 分支 Full Request 为主

新组件功能将以具他替代平代替的方式实现

历史：

*   alibaba 出了 dubbo，停更
*   spring 结合 netflix 整出 spring cloud。又停更了
*   alibaba 又出马了得出 springcloud alibaba

spring cloud alibaba 带来了什么？

2018.10.31，spring cloud Alibaba 正式入驻了 Spring Cloud 官方孵化器，并在 Maven 中央库发布了第一个版本

主要功能：

*   **服务限流降级**：默认支持 WebServlet、WebFlux, OpenFeign、RestTemplate、Spring Cloud Gateway, Zuul, Dubbo 和 RocketMQ 限流降级功能的接入，可以在运行时通过控制台实时修改限流降级规则，还支持查看限流降级 Metrics 监控。
*   **服务注册与发现**：适配 Spring Cloud 服务注册与发现标准，默认集成了 Ribbon 的支持。
*   **分布式配置管理**：支持分布式系统中的外部化配置，配置更改时自动刷新。
*   **消息驱动能力**：基于 Spring Cloud Stream 为微服务应用构建消息驱动能力。
*   **分布式事务**：使用 @GlobalTransactional 注解， 高效并且对业务零侵入地解决分布式事务问题。。
*   **阿里云对象存储**：阿里云提供的海量、安全、低成本、高可靠的云存储服务。支持在任何应用、任何时间、任何地点存储和访问任意类型的数据。
*   **分布式任务调度**：提供秒级、精准、高可靠、高可用的定时（基于 Cron 表达式）任务调度服务。同时提供分布式的任务执行模型，如网格任务。网格任务支持海量子任务均匀分配到所有 Worker（schedulerx-client）上执行。
*   **阿里云短信服务**：覆盖全球的短信服务，友好、高效、智能的互联化通讯能力，帮助企业迅速搭建客户触达通道。

只需引入依赖：

```
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-alibaba-dependencies</artifactId>
            <version>2.2.3.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>

```

组件：

*   **[Sentinel](https://github.com/alibaba/Sentinel)**：把流量作为切入点，从流量控制、熔断降级、系统负载保护等多个维度保护服务的稳定性。
*   **[Nacos](https://github.com/alibaba/Nacos)**：一个更易于构建云原生应用的动态服务发现、配置管理和服务管理平台。
*   **[RocketMQ](https://rocketmq.apache.org/)**：一款开源的分布式消息系统，基于高可用分布式集群技术，提供低延时的、高可靠的消息发布与订阅服务。
*   **[Dubbo](https://github.com/apache/dubbo)**：Apache Dubbo™ 是一款高性能 Java RPC 框架。
*   **[Seata](https://github.com/seata/seata)**：阿里巴巴开源产品，一个易于使用的高性能微服务分布式事务解决方案。
*   **[Alibaba Cloud OSS](https://www.aliyun.com/product/oss)**: 阿里云对象存储服务（Object Storage Service，简称 OSS），是阿里云提供的海量、安全、低成本、高可靠的云存储服务。您可以在任何应用、任何时间、任何地点存储和访问任意类型的数据。
*   **[Alibaba Cloud SchedulerX](https://help.aliyun.com/document_detail/43136.html)**: 阿里中间件团队开发的一款分布式任务调度产品，提供秒级、精准、高可靠、高可用的定时（基于 Cron 表达式）任务调度服务。
*   **[Alibaba Cloud SMS](https://www.aliyun.com/product/sms)**: 覆盖全球的短信服务，友好、高效、智能的互联化通讯能力，帮助企业迅速搭建客户触达通道。

https://github.com/alibaba/spring-cloud-alibaba/blob/master/README-zh.md

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

Nacos
-----

nacos(NAming COnfiguration Service)：服务注册和配置中心

> Nacos = Eureka + Config + Bus
> 
> 替代 Eureka 做服务注册中心
> 
> 替代 Config 做服务配置中心

> github 地址： https://github.com/alibaba/Nacos
> 
> Nacos 地址： https://nacos.io/zh-cn/

<table><thead><tr><th>服务注册与服务框架</th><th>CAP 模型</th><th>控制台管理</th><th>社区活跃度</th></tr></thead><tbody><tr><td>Eureka</td><td>AP 高可用</td><td>支持</td><td>低 (2.x 版本闭源)</td></tr><tr><td>Zookeeper</td><td>CP 一致</td><td>支持</td><td>中</td></tr><tr><td>Consul</td><td>CP</td><td>支持</td><td>高</td></tr><tr><td>Nacos</td><td>AP（可以切换）</td><td>支持</td><td>高</td></tr></tbody></table>

nacos 可以切换 AP 和 CP , 可使用如下命令切换成 CP 模式：

```
curl -X PUT '$NACOS_SERVER:8848/nacos/v1/ns/operator/switches?entry=serverMode&value=CP'

```

下载 ：

> 下载地址： https://github.com/alibaba/nacos/releases/tag/1.1.4
> 
> 直接下载网址： https://github.com/alibaba/nacos/releases/download/1.1.4/nacos-server-1.1.4.zip
> 
> 下载压缩包以后解压，进入 bin 目录，打开 dos 窗口，执行 startup 命令启动它。
> 
> 端口号 8848
> 
> 可访问 ： 【 http://localhost:8848/nacos/index.html】地址，默认账号密码都是 nacos

### nacos 服务中心

https://nacos.io/zh-cn/docs/feature-list.html

https://spring-cloud-alibaba-group.github.io/github-pages/hoxton/en-us/index.html#_spring_cloud_alibaba_nacos_discovery

#### nacos 提供者

新建模块 `cloudalibaba-provider-payment9001`

父 pom 中

```
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-alibaba-dependencies</artifactId>
            <version>2.1.1.BUILD-SNAPSHOT</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>

```

子 pom 依赖：

```
	<dependencies>

        <!-- springcloud alibaba nacos 依赖 -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        
        <!-- springboot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <!-- 日常通用jar包 -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```

yml 配置：

```
server:
  port: 9001
spring:
  application:
    name: nacos-provider
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848
management:
  endpoints:
    web:
      exposure:
        include: '*'

```

```
@EnableDiscoveryClient // 注册
@SpringBootApplication
public class PaymentMain9001 {
    public static void main(String[] args) {
            SpringApplication.run(PaymentMain9001.class, args);
    }
}

```

```
@RestController
public class PaymentController {
    @Value("${server.port}")
    private String serverPort;

    @GetMapping(value = "/payment/nacos/{id}")
    public String getPayment(@PathVariable("id") Integer id) {
        return "nacos registry, serverPort: "+ serverPort+"\t id"+id;
    }
}

```

Nacos 自带负载均衡机制，下面创建第二个提供者 9003。也可以`-Dserver.port=9011`

新建 cloudalibaba-provider-payment9003 提供者模块，clone 9001 就可以

#### nacos 消费者

新建消费者 模块： cloudalibaba-customer-nacos-order83

```
<!--SpringCloud ailibaba nacos -->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>

```

```
server:
  port: 83

spring:
  application:
    name: nacos-order-consumer
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848


#消费者将要去访问的微服务名称(注册成功进nacos的微服务提供者)
service-url:
  nacos-user-service: http://nacos-payment-provider

```

```
@Configuration
public class ApplicationContextConfig { // nacos底层也是ribbon，注入RestTemplate
    @Bean
    @LoadBalanced // 负载均衡
    public RestTemplate getRestTemplate() {
        return new RestTemplate();
    }
}

```

controller :

```
@RestController
@Slf4j
public class OrderNacosController {
    @Resource
    private RestTemplate restTemplate;

    @Value("${service-url.nacos-user-service}")
    private String serverURL; //在yml里面写的提供者服务路径，  值为：http://nacos-provider

    @GetMapping(value = "/consumer/payment/nacos/{id}")
    public String paymentInfo(@PathVariable("id") Long id) {
        return restTemplate.getForObject(serverURL+"/payment/nacos/"+id,String.class);
    }

}

```

#### 各种服务中心对比

<table><thead><tr><th>服务注册与服务框架</th><th>CAP 模型</th><th>控制台管理</th><th>社区活跃度</th></tr></thead><tbody><tr><td>Eureka</td><td>AP</td><td>支持</td><td>低 (2.x 版本闭源)</td></tr><tr><td>Zookeeper</td><td>CP</td><td>支持</td><td>中</td></tr><tr><td>Consul</td><td>CP</td><td>支持</td><td>高</td></tr><tr><td>Nacos</td><td>AP/CP</td><td>支持</td><td>高</td></tr></tbody></table>

<table><thead><tr><th>组件名</th><th>语言</th><th>CAP</th><th>服务健康检查</th><th>对外暴露接口</th><th>SpringCloud 集合</th></tr></thead><tbody><tr><td>Eureka</td><td>java</td><td>AP</td><td>可配支持</td><td>HTTP</td><td>已集成</td></tr><tr><td>Consul</td><td>Go</td><td>CP</td><td>支持</td><td>HTTP/DNS</td><td>已集成</td></tr><tr><td>Zookeeper</td><td>java</td><td>CP</td><td>支持</td><td>客户端</td><td>已集成</td></tr></tbody></table>

NACOS 支持 CP 和 AP 切换

C 要求一致性，A 要求可用性。

何时选择使用何种模式？

一般来说，

如果不需要存储服级的信息且服务实例是通过 nacos-client 注册，并能够保持心跳上报，那么就可以选择 AP 模式。当前主流的服务如 Spring cloud 和 Dubbo 服务，都适用于 AP 模式，AP 模式为了服务的可用性而减弱了一致性，因此 AP 模式下只支持注册临时实例。

如果需要在服务级别编辑或者存储配置信息，那么 CP 是必须，K8S 服务和 DNS 服务则适用于 CP 模式。

CP 模式下则支持注册持久化实例，此时则是以 Raft 协议为集群运行模式，该模式下汪册实例之前须先注册服务，如果服务不存在，则会返回错误

切换命令：`curl -X PUT '$NACOS_SERVER:8848/nacos/v1/ns/operator/switches?entry=serverMode&value=CP'`

![](https://img-blog.csdnimg.cn/img_convert/cf83fe8efa4556a06755a6f9b519040f.png)

![](https://img-blog.csdnimg.cn/img_convert/fe93ab4dbfdc520c411ca49163d6821a.png)

### nacos 配置中心

##### 配置中心对比

<table><thead><tr><th>对比项目</th><th>Spring Cloud Config</th><th>Apollo</th><th>Nacos</th></tr></thead><tbody><tr><td>配置实时推送</td><td>支持 (Spring Cloud Bus)</td><td>支持 (HTTP 长轮询 1s 内)</td><td>支持 (HTTP 长轮询 1s 内)</td></tr><tr><td>版本管理</td><td>支持 (Git)</td><td>支持</td><td>支持</td></tr><tr><td>配置回滚</td><td>支持 (Git)</td><td>支持</td><td>支持</td></tr><tr><td>灰度发布</td><td>支持</td><td>支持</td><td>不支持</td></tr><tr><td>权限管理</td><td>支持 (依赖 Git)</td><td>支持</td><td>不支持</td></tr><tr><td>多集群</td><td>支持</td><td>支持</td><td>支持</td></tr><tr><td>多环境</td><td>支持</td><td>支持</td><td>支持</td></tr><tr><td>监听查询</td><td>支持</td><td>支持</td><td>支持</td></tr><tr><td>多语言</td><td>只支持 Java</td><td>主流语言，提供了 Open API</td><td>主流语言，提供了 Open API</td></tr><tr><td>配置格式校验</td><td>不支持</td><td>支持</td><td>支持</td></tr><tr><td>单机读 (QPS)</td><td>7(限流所致)</td><td>9000</td><td>15000</td></tr><tr><td>单击写 (QPS)</td><td>5(限流所致)</td><td>1100</td><td>1800</td></tr><tr><td>3 节点读 (QPS)</td><td>21(限流所致)</td><td>27000</td><td>45000</td></tr><tr><td>3 节点写 (QPS)</td><td>5(限流所致)</td><td>3300</td><td>5600</td></tr></tbody></table>

从配置中心角度来看，性能方面 Nacos 的读写性能最高，Apollo 次之，Spring Cloud Config 依赖 Git 场景不适合开放的大规模自动化运维 API。功能方面 Apollo 最为完善，nacos 具有 Apollo 大部分配置管理功能，而 Spring Cloud Config 不带运维管理界面，需要自行开发。Nacos 的一大优势是整合了注册中心、配置中心功能，部署和操作相比 Apollo 都要直观简单，因此它简化了架构复杂度，并减轻运维及部署工作。

> nacos 还可以作为服务配置中心，下面是案例，创建一个模块，从 nacos 上读取配置信息。
> 
> nacos 作为配置中心，不需要像 springcloud config 一样做一个 Server 端模块。

新建模块 `cloudalibaba-config-nacos-client3377`

pom 依赖：

```
 <dependencies>
     
        <!-- 以 nacos 做服务配置中心的依赖 -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
        </dependency>
     
        <!-- springcloud alibaba nacos 依赖 -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!-- springboot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <!-- 日常通用jar包 -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```

主启动类也是极其普通：

```
@EnableDiscoveryClient // 消费
@SpringBootApplication
public class NacosConfigClientMain3377{
    public static void main(String[] args) {
        SpringApplication.run(NacosConfigClientMain3377.class, args);
    }
}

```

bootstrap.yml 配置：

```
# nacos配置
server:
  port: 3377

spring:
  application:
    name: nacos-config-client
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848 #Nacos服务注册中心地址
      config:
        server-addr: localhost:8848 #Nacos作为配置中心地址
        file-extension: yaml #指定yaml格式的配置
        group: DEV_GROUP
        namespace: 7d8f0f5a-6a53-4785-9686-dd460158e5d4


# ${spring.application.name}-${spring.profile.active}.${spring.cloud.nacos.config.file-extension}
# nacos-config-client-dev.yaml

# nacos-config-client-test.yaml   ----> config.info

```

application.yml

```
spring:
  profiles:
    active: dev # 表示开发环境
    #active: test # 表示测试环境
    #active: info

```

controller 层进行读取配置测试：

```
@RestController
@RefreshScope  //支持Nacos的动态刷新
public class ConfigClientController {

    @Value("${config.info}") // 从nacos中取
    private String configInfo;

    @GetMapping("configclient/getconfiginfo")
    public String getConfigInfo(){
        return configInfo;
    }
}

```

nacos 同 springcloud-config 一样，在项目初始化时，要先从配置中心进行配置拉取，拉取配置之后，才能保证项目的正常启动。

springboot 的配置文件的加载是存在优先熟悉怒的，bootstrap 优先级高于 application。（bootstrap 中放共性，application 中放个性）

nacos 中的 dataid 的组成格式及与 springboot 配置文件中的匹配规则：

在 nacos 中，消费端要的文件怎么和 nacos 中的文件匹配呢？

在 Nacos Spring Cloud 中，`dataId` 的完整格式如下：（就是说在 nacos 端我们怎么命名文件的）

```
${prefix}-${spring.profiles.active}.${file-extension}

```

*   `prefix` 默认为 `spring.application.name` 的值，也可以通过配置项 `spring.cloud.nacos.config.prefix`来配置。
*   `spring.profiles.active` 即为当前环境对应的 profile，详情可以参考 [Spring Boot 文档](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-profiles.html#boot-features-profiles)。 **注意：当 `spring.profiles.active` 为空时，对应的连接符 `-` 也将不存在，dataId 的拼接格式变成 `${prefix}.${file-extension}`**
*   `file-exetension` 为配置内容的数据格式，可以通过配置项 `spring.cloud.nacos.config.file-extension` 来配置。目前只支持 `properties` 和 `yaml` 类型。（注意 nacos 里必须使用 yaml）

> 从上面可以看到重要的一点，配置文件的名称第二项，spring.profiles.active 是依据当前环境的 profile 属性值的，也就是这个值如果是 dev，即开发环境，它就会读取 dev 的配置信息，如果是 test，测试环境，它就会读取 test 的配置信息，就是从 spring.profile.active 值获取当前应该读取哪个环境下的配置信息。

所以要配置 spring.profiles.active，新建 application.yml 文件，添加如下配置：

```
spring:
  profiles:
    active: dev # 表示开发环境

```

综合以上说明，和下面的截图，Nacos 的 dataid（类似文件名）应为： nacos-config-client-dev.yaml (必须是 yaml)

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

注意 nacos 里不要写成 yml，要写成 yaml：

![](https://img-blog.csdnimg.cn/img_convert/5954d90819e12cafc9972a8e0977561d.png)

当修改配置值，会发现 3377 上也已经修改，Nacos 自带自动刷新功能！

nacos 的优势在哪：

*   问题 1：实际开发者，通常一个系统会准备 dev/test/prod 环境。如何保证环境启动时服务能正确读取 nacos 上相应环境的配置文件
    *   用 namespace 区分环境
*   问题 2：一个大型分布式微服务系统有很多微服务子项目，每个微服务项目又都会有相应的开发环境、测试环境、预发环境、正式环境。那怎么对微服务配置进行管理呢？
    *   用 group 把不同的微服务划分到同一个分组里面去

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

默认：Namespace=,Cluster=DEFAULT

*   namespace 环境
*   group

Service 就是微服务，一个 service 可以包含多个 cluster 集群，nacos 默认 cluster 是 DEFAULT，Cluster 是对指定微服务的一个虚拟划分。

比方说为了容灾，将 service 微服务分别部署在了杭州机房和广州机房，这是就可以给杭州机房的 service 微服务起一个集群名称 HZ

给广州的 service 微服务起一个集群名称 GZ，还可以尽量让同一个机房的微服务互相调用，以提升虚拟。

最后 instance 就是微服务的实例

##### dgn 方案

`dataid`方案（就是 nacos 的文件名）：

*   指定 spring.profile.active 和配置文件的 dataID 来使不太环境下读取不同的配置
*   配置空间 + 配置分组 + 新建 dev 和 test 两个 dataid：就是创建 - 后不同的两个文件名`nacos-config-client-dev.yaml`、`nacos-config-client-test.yaml`
*   通过 IDEA 里的 spring.profile.active 属性就能进行多环境下配置文件的读取

`Group`方案（默认 DEFAULT_GROUP）：

*   在 nacos 创建配置文件时，给文件指定分组。
*   在 IDEA 中该 group 内容
*   实现的功能：当修改开发环境时，只会从同一 group 中进行切换。

`namespace`方案（默认 public）：

*   这个是不允许删除的，可以创建一个新的命名空间，会自动给创建的命名空间一个流水号。
*   在 nacos 新建命名空间，自动出现 7d8f0f5a-6a53-4785-9686-dd460158e5d4
*   在 IDEA 的 yml 中指定命名空间 namespace: 7d8f0f5a-6a53-4785-9686-dd460158e5d4

最后，dataid、group、namespace 三者关系如下：（不同的 dataid，是相互独立的，不同的 group 是相互隔离的，不同的 namespace 也是相互独立的）

> 上面只是小打小闹，下面才是真正的高级操作。

搭建集群必须持久化，不然多台机器上的 nacos 的配置信息不同，造成系统错乱。它不同于单个 springcloud config，没有集群一说，而且数据保存在 github 上，也不同于 eureka，配置集群就完事了，没有需要保存的配置信息。

### nacos 集群 / 持久化

nacos 挂了怎么办？

https://nacos.io/zh-cn/docs/cluster-mode-quick-start.html

> 一台 linux 虚拟机：nginx 服务器（虚拟 ip），3 个 nacos 服务，一个 mysql 数据库。
> 
> nginx 的安装参考之前学，使用 ContOs7 至少需要安装 gcc 库，不然无法编译安装【yum install gcc】
> 
> nacos 下载 linux 版本的 tar.gz 包：https://github.com/alibaba/nacos/releases/download/1.1.4/nacos-server-1.1.4.tar.gz
> 
> mysql root 用户密码为 Dkf!!2020

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

VIP 是虚拟 IP，即 nginx

nginx 也该是集群

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

Nacos 支持三种部署模式 https://nacos.io/zh-cn/docs/deployment.html

*   单机模式 - 用于测试和单机试用。
*   集群模式 - 用于生产环境，确保高可用。
*   多集群模式 - 用于多数据中心场景。

单机模式支持 mysql：在 0.7 版本之前，在单机模式时 nacos 使用**嵌入式数据库**（derby，他的 pom 里有这个依赖）实现数据的存储，不方便观察数据存储的基本情况。0.7 版本增加了支持 mysql 数据源能力，具体的操作步骤：

*   1. 安装数据库，版本要求：5.6.5+
    
*   2. 初始化 mysql 数据库，数据库初始化文件：nacos/conf/nacos-mysql.sql。创建个 database 数据库 nacos_devtest
    
*   3. 修改 IDEA 中 nacos/conf/application.properties 文件 (切换数据库)，增加支持 mysql 数据源配置（目前只支持 mysql），添加 mysql 数据源的 url、用户名和密码。
    
*   ```
    # 切换数据库
    spring.datasource.platform=mysql
    
    db.num=1
    db.url.0=jdbc:mysql://11.162.196.16:3306/nacos_devtest?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
    db.user=root
    db.password=123456
    
    ```
    
*   再以单机模式启动 nacos(重启)，nacos 所有写嵌入式数据库的数据都写到了 mysql
    

单击的数据库都是独立的，我们得让他们共用一个数据库

Nacos 集群配置

环境准备：

1.  64 bit OS Linux/Unix/Mac，推荐使用 Linux 系统。
2.  64 bit JDK 1.8+；[下载](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). [配置](https://docs.oracle.com/cd/E19182-01/820-7851/inst_cli_jdk_javahome_t/)。
3.  Maven 3.2.x+；[下载](https://maven.apache.org/download.cgi). [配置](https://maven.apache.org/settings.html)。
4.  3 个或 3 个以上 Nacos 节点才能构成集群。

开始配置集群：

1.  首先对 nacos 进行持久化操作，操作如上面一致。
    
2.  修改 nacos/conf 下的 cluster.conf 文件，添加如下内容:
    
    ```
    # it is ip
    # 告诉这3个集群结点是一组的 # 不能写127.0.0.1，必须是linux hostname -i能够识别的ip
    192.168.1.2:3333
    192.168.1.2:4444
    192.168.1.2:5555
    
    ```
    
3.  修改 nacos/conf/application.properties 文件，添加设置我们的数据库信息
    
4.  模拟三台 nacos 服务，编辑 nacos 的 startup.sh 脚本，使他能够支持不同的端口启动多次。  
    集群启动，我们希望可以类似其他软件的 shell 命令，传递不同的端口号启动不同的 nacos 实例。
    
    `vim startup.sh`
    
    ![](https://img-blog.csdnimg.cn/img_convert/b39e4b09d1da87d2598bfdbf31c1d751.png)
    
    ![](https://img-blog.csdnimg.cn/img_convert/c159b991ac8444ab61bc240a6c4899bc.png)
    
    `nohup $JAVA -Dserver.port=${PORT} ${JAVA_POT} nacoas.nacos >> ${BASE_DIR}/logs/start.out 2>&1 &`
    
5.  依次执行命令启动 3 个 nacos 集群：  
    `./startup.sh -p 3333` 表示启动端口号为 3333 的 nacos 服务器实例  
    `./startup.sh -p 4444`  
    `./startup.sh -p 5555`  
    `ps -ef | grep nacos | grep -v grep | wc -l`
    
6.  修改 nginx 配置，把他作为负载均衡：
    
    ```
    vim ./nginx/conf/nginx.conf
    
    ```
    
    ![](https://img-blog.csdnimg.cn/img_convert/a377948306a03bb10de4dd9657578a22.png)
    
7.  启动 nginx：`./nginx -c ../conf/nginx.conf`
    
8.  通过 nginx 访问：192.168.1.2:1111/nacos/#/login
    
9.  使用 9002 模块注册进 Nacos 集群，并获取它上面配置文件的信息 application.yml 中的`server-addr: 192.168.1.2:1111`，进行测试。
    

Sentinel
--------

> sentinel 在 springcloud Alibaba 中的作用是实现`熔断`和`限流`。类似于 Hystrix 豪猪

> 下载地址 dashboard： https://github.com/alibaba/Sentinel/releases/download/1.7.1/sentinel-dashboard-1.7.1.jar
> 
> 下载 jar 包以后，使用【java -jar】命令启动即可。
> 
> 它使用 8080 端口，用户名和密码都为 ： sentinel

随着微服务的流行，服务和服务之间的稳定性变得越来越重要。Sentinel 以流量为切入点，从流量控制、熔断降级、系统负载保护等多个维度保护服务的稳定性。

Sentinel 具有以下特征:

*   **丰富的应用场景**：Sentinel 承接了阿里巴巴近 10 年的双十一大促流量的核心场景，例如秒杀（即突发流量控制在系统容量可以承受的范围）、消息削峰填谷、集群流量控制、实时熔断下游不可用应用等。
*   **完备的实时监控**：Sentinel 同时提供实时的监控功能。您可以在控制台中看到接入应用的单台机器秒级数据，甚至 500 台以下规模的集群的汇总运行情况。
*   **广泛的开源生态**：Sentinel 提供开箱即用的与其它开源框架 / 库的整合模块，例如与 Spring Cloud、Dubbo、gRPC 的整合。您只需要引入相应的依赖并进行简单的配置即可快速地接入 Sentinel。
*   **完善的 SPI 扩展点**：Sentinel 提供简单易用、完善的 SPI 扩展接口。您可以通过实现扩展接口来快速地定制逻辑。例如定制规则管理、适配动态数据源等。

![](https://img-blog.csdnimg.cn/img_convert/4afe83cd7157f9147f7aa969fdf17301.png)

Sentinel 分为两个部分:

*   核心库（Java 客户端）不依赖任何框架 / 库，能够运行于所有 Java 运行时环境，同时对 Dubbo / Spring Cloud 等框架也有较好的支持。
*   控制台（Dashboard）基于 Spring Boot 开发，打包后可以直接运行，不需要额外的 Tomcat 等应用容器。

### Demo

> 先启动 nacos
> 
> 新建模块 `cloudalibaba-sentinel-service8401` ，使用 nacos 作为服务注册中心
> 
> Sentinel 可以对 service 进行监控、熔断、降级
> 
> 没访问时再 sentinel 里是看不到监控的应用的，因为是懒加载，需要访问一次

pom 依赖：

```
	<dependencies>
        <!-- 后续做Sentinel的持久化会用到的依赖 -->
        <dependency>
            <groupId>com.alibaba.csp</groupId>
            <artifactId>sentinel-datasource-nacos</artifactId>
        </dependency>
        <!-- sentinel  -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
        </dependency>
        <!-- springcloud alibaba nacos 依赖,Nacos Server 服务注册中心 -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        
        <!-- springboot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <!-- 日常通用jar包 -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```

yml 配置：

```
server:
  port: 8401
spring:
  application:
    name: cloudalibaba-sentinel-service
  cloud:
    nacos:
      discovery:
        # 服务注册中心 # sentinel注册进nacos
        server-addr: localhost:8848
    sentinel:
      transport:
        # 配置 Sentinel Dashboard 的地址
        dashboard: localhost:8080
        # 默认8719 ，如果端口被占用，端口号会自动 +1，直到找到未被占用的端口，提供给 sentinel 的监控端口
        port: 8719
        
management:
  endpoints:
    web:
      exposure:
        include: '*'

```

写一个简单的主启动类，再写一个简单的 controller 测试 sentinel 的监控。

```
@RestController
@Slf4j
public class FlowLimitController {
    @GetMapping("/testA")
    public String testA() {
        return "------testA";
    }

    @GetMapping("/testB")
    public String testB() {
        log.info(Thread.currentThread().getName()+"\t"+"...testB");
        return "------testB";
    }


    @GetMapping("/testD")
    public String testD() {
//        try { TimeUnit.SECONDS.sleep(1); } catch (InterruptedException e) { e.printStackTrace(); }
//        log.info("testD 测试RT");

        log.info("testD 异常比例");
        int age = 10/0;
        return "------testD";
    }

    @GetMapping("/testE")
    public String testE() {
        log.info("testE 测试异常数");
        int age = 10/0;
        return "------testE 测试异常数";
    }

    @GetMapping("/testHotKey")
    @SentinelResource(value = "testHotKey",blockHandler = "deal_testHotKey")
    public String testHotKey(@RequestParam(value = "p1",required = false) String p1,
                             @RequestParam(value = "p2",required = false) String p2) {
        //int age = 10/0;
        return "------testHotKey";
    }
    public String deal_testHotKey (String p1, String p2, BlockException exception) {
        return "------deal_testHotKey,o(╥﹏╥)o";  //sentinel系统默认的提示：Blocked by Sentinel (flow limiting)
    }

}

```

```
@RestController
public class RateLimitController {
    @GetMapping("/byResource")
    @SentinelResource(value = "byResource",blockHandler = "handleException")
    public CommonResult byResource() {
        return new CommonResult(200,"按资源名称限流测试OK",new Payment(2020L,"serial001"));
    }
    public CommonResult handleException(BlockException exception) {
        return new CommonResult(444,exception.getClass().getCanonicalName()+"\t 服务不可用");
    }

    @GetMapping("/rateLimit/byUrl")
    @SentinelResource(value = "byUrl")
    public CommonResult byUrl() {
        return new CommonResult(200,"按url限流测试OK",new Payment(2020L,"serial002"));
    }


    @GetMapping("/rateLimit/customerBlockHandler")
    @SentinelResource(value = "customerBlockHandler",
            blockHandlerClass = CustomerBlockHandler.class,
            blockHandler = "handlerException2")
    public CommonResult customerBlockHandler() {
        return new CommonResult(200,"按客戶自定义",new Payment(2020L,"serial003"));
    }
}

```

```
public class CustomerBlockHandler {

    public static CommonResult handlerException(BlockException exception) {
        return new CommonResult(4444,"按客戶自定义,global handlerException----1");
    }

    public static CommonResult handlerException2(BlockException exception) {
        return new CommonResult(4444,"按客戶自定义,global handlerException----2");
    }
}

```

```
@EnableDiscoveryClient
@SpringBootApplication
public class MainApp8401 {
    public static void main(String[] args) {
        SpringApplication.run(MainApp8401.class, args);
    }
}

```

### 流控规则

*   资源名：唯一名称，默认请求路径
*   针对来源：sentinel 可以针对调用者进行限流，填写微服务名，默认 default（不区分来源）
*   阈值类型 / 单机值：
    *   QPS（每秒钟的请求数量）：当调用该 api 就 QPS 达到阈值的时候，进行限流
    *   线程数．当调用该 api 的线程数达到阈值的时候，进行限流
*   是否集群：不需要集群
*   流控模式：
    *   直接：api 达到限流条件时，直接限流。分为 QPS 和线程数
    *   关联：当关联的资到阈值时，就限流自己。别人惹事，自己买单
    *   链路：只记录指定链路上的流量（指定资源从入口资源进来的流量，如果达到阈值，就进行限流）【api 级别的针对来源】
*   流控效果：
    *   快速失败：直接抛异常
    *   warm up：根据 codeFactor（冷加载因子，默认 3）的值，从阈值 codeFactor，经过预热时长，才达到设置的 QPS 阈值

重要属性：

<table><thead><tr><th>Field</th><th>说明</th><th>默认值</th></tr></thead><tbody><tr><td>resource</td><td>资源名，资源名是限流规则的作用对象</td><td></td></tr><tr><td>count</td><td>限流阈值</td><td></td></tr><tr><td>grade</td><td>限流阈值类型，QPS 模式（1）或并发线程数模式（0）</td><td>QPS 模式</td></tr><tr><td>limitApp</td><td>流控针对的调用来源</td><td><code>default</code>，代表不区分调用来源</td></tr><tr><td>strategy</td><td>调用关系限流策略：直接、链路、关联</td><td>根据资源本身（直接）</td></tr><tr><td>controlBehavior</td><td>流控效果（直接拒绝 / WarmUp / 匀速 + 排队等待），不支持按调用关系限流</td><td>直接拒绝</td></tr><tr><td>clusterMode</td><td>是否集群限流</td><td>否</td></tr></tbody></table>

我们先只针对 / testA 请求进行限制

**流控模式–直接**：

![](https://img-blog.csdnimg.cn/img_convert/ed8c470859d2364e159219e3b364444f.png)

> 限流表现：当超过阀值，就会被降级。
> 
> 1s 内多次刷新网页，localhost:8401/testA
> 
> 返回 Blocked by Sentienl(flow limiting)

**流控模式–关联**：

*   当与 A 关联的资源 B 达到阀值后，就限流 A 自己
*   B 惹事，A 挂了。支付达到阈值，限流下单接口。B 阈值达到 1，A 就挂
*   用 post 访问 B 让 B 忙，访问 A 发现挂了

![](https://img-blog.csdnimg.cn/img_convert/57bc94814fa2307f6daeed7a46350dd9.png)

**流控效果–预热 Warm up**：

访问数量慢慢升高

阈值初一 coldFactor（默认 3），经过预热时长后才会达到阈值。

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

**流控效果–排队等待**：

匀速排队（Ru1eConstant.CONTROL_BEHAVIOR_RATE_LIMITER）方式会严格控制请求通过的间隔时间，即让请求以均匀的速度通过对应的是漏桶算法。详细文档可以参考流量控制 - 匀速器模式，具体的例子可以参见 PaceFlowDemo

该方式的作用如下图所示

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

这种方式主要用于处理间隔性突发的流量，伊消息列。想象一下这样的场景，在某一秒有大量的请求到来，而接下来的月耖则处于空闲状态，我们希系统能够在接下来的空闲期间逐渐处理这些请求，而不是第一秒就拒绝多余的请求

### 熔断降级

新增降级规则：降低策略：RT

RT（平均响应时间，秒级）

平均响应时间 超出阈值 且 在时间窗口内通过的请求 >=5，两个条件同时满足后触发降级

窗口期过后关闭断路器

RT 最大 4900（更大的需要通过 - Dcsp.Sentinel.statistic.max.rt=XXXX 才能生效）

异常比例（秒级）  
QPS>=5 且异常比例（秒级统计）超过阈值时，触发降级，时间窗口结束后，关闭降级

sentinel 熔断降级会在调用链路中某个资源出现不稳定状态时（例如调用超时或异常比例升高），对这个资源的调用进行限制，让请求快速失败，避免影响到其它的资源而导致级联错误。

当资源被降级后，在接下来的降级时间窗囗之内，对该资源的调用都自动熔断（默认行为是抛出 DegradeException)。

**降级策略–RT**

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAACbklEQVRoQ+2aMU4dMRCGZw6RC1CSSyQdLZJtKQ2REgoiRIpQkCYClCYpkgIESQFIpIlkW+IIcIC0gUNwiEFGz+hlmbG9b1nesvGW++zxfP7H4/H6IYzkwZFwQAUZmpJVkSeniFJKA8ASIi7MyfkrRPxjrT1JjZ8MLaXUDiJuzwngn2GJaNd7vyP5IoIYY94Q0fEQIKIPRGS8947zSQTRWh8CwLuBgZx479+2BTkHgBdDAgGAC+fcywoyIFWqInWN9BSONbTmFVp/AeA5o+rjKRJ2XwBYRsRXM4ZXgAg2LAPzOCDTJYQx5pSIVlrC3EI45y611osMTHuQUPUiYpiVooerg7TWRwDAlhSM0TuI+BsD0x4kGCuFSRVzSqkfiLiWmY17EALMbCAlMCmI6IwxZo+INgQYEYKBuW5da00PKikjhNNiiPGm01rrbwDwofGehQjjNcv1SZgddALhlJEgwgJFxDNr7acmjFLqCyJuTd6LEGFttpmkYC91Hrk3s1GZFERMmUT01Xv/sQljjPlMRMsxO6WULwnb2D8FEs4j680wScjO5f3vzrlNJszESWq2LYXJgTzjZm56MCHf3zVBxH1r7ftU1splxxKYHEgoUUpTo+grEf303rPH5hxENJqDKQEJtko2q9zGeeycWy3JhpKhWT8+NM/sufIhBwKI+Mta+7pkfxKMtd8Qtdbcx4dUQZcFCQ2I6DcAnLUpf6YMPxhIDDOuxC4C6djoQUE6+tKpewWZ1wlRkq0qUhXptKTlzv93aI3jWmE0Fz2TeujpX73F9TaKy9CeMk8vZusfBnqZ1g5GqyIdJq+XrqNR5AahKr9CCcxGSwAAAABJRU5ErkJggg==)

降级策略–异常比例：

异常比例（DEGRADE-GRADE-EXCEPTION-RATIO）：当资源的每秒请求量 >=5，并且每秒异常总数占通过的比值超过阈值（DegradeRule 中的 count）之后，资源进入降级状态，即在接下的时间窗口（DegradeRu1e 中的 timeWindow，，以 s 为单位）之内，对这个方法的调用都会自动地返回。异常 b 阈值范围是 [0.0,l.0]，代表 0％一 100％。

降级测录–异常数：

异常数（DEGRADE-GRADE-EXCEPTION-COUNT）：当资源近 1 分钟的异常数目超过阈值之后会进行熔断。注意由于统计时间窗口是分钟级别的，若 timeWindow 小于 60s, 则结束熔断状态后仍可能再进入熔断状态。

时间窗口一定要大于等于 60 秒。

时间窗口结束后关闭降级

localhost:8401/testE , 第一次访问绝对报错，因为除数不能为零，  
我们看到 error 窗口，但是达到 5 次报错后，进入熔断后降级。

[外链图片转存失败, 源站可能有防盗链机制, 建议将图片保存下来直接上传 (img-0uG4jp95-1615737211171)(images\1597821618735.png)]

### 热点 Key 限流

何为热点？热点即经常访问的数据。很多时候我们希望统计某个热点数据中访问频次最高的 TopK 数据，并对其访问进行限制。比如：

*   商品 ID 为参数，统计一段时间内最常购买的商品 ID 并进行限制
*   用户 ID 为参数，针对一段时间内频繁访问的用户 ID 进行限制

参数限流会统计传入参数中的参数，并根据配置流阈值与模式，对包含热点参数的资源调用进行限流。热点参数限流可以看做是一种特殊的流量控制，仅对包含热点参数的资源调用生效。

controller 层写一个 demo:

```
	@GetMapping("/testhotkey")
    @SentinelResource(value = "testhotkey", blockHandler = "deal_testhotkey")
    //这个value是随意的值，并不和请求路径必须一致
    //在填写热点限流的 资源名 这一项时，可以填 /testhotkey 或者是 @SentinelResource的value的值
    public String testHotKey(
            @RequestParam(value="p1", required = false) String p1,
            @RequestParam(value = "p2", required = false) String p2
    ){
        return "testHotKey__success";
    }

	//类似Hystrix 的兜底方法
    public String deal_testhotkey(String p1, String p2, BlockException e){
        return "testhotkey__fail"; 
    }

```

![](https://img-blog.csdnimg.cn/img_convert/4cf0c88905f8a3bc4c8fe4de1552e3d6.png)

![](https://img-blog.csdnimg.cn/img_convert/59c35e9cae5431ae7d9d0e52135380b3.png)

说明：

@SentinelResource ：处理的是 Sentine1 控制台配置的违规情况，有 blockHandler 方法配置的兜底处理

@RuntimeException：int age=10/0，这个是 java 运行时报出的运行时异异常 RunTimeException，@Sentine1Resource 不管

### 系统规则

> 一般配置在网关或者入口应用中，但是这个东西有点危险，不但值不合适，就相当于系统瘫痪。

系统自适应限流

Sentinel 系统自适应限流从整体维度对应用入口流量进行控制，结合应用的 Load、CPU 使用率、总体平均 RT、入口 QPS 和并发线程数等几个维度的监控指标，通过自适应的流控策略，让系统的入口流量和系统的负载达到一个平衡，让系统尽可能跑在最大吞吐量的同时保证系统整体的稳定性。

系统规则包含下面几个重要的属性：

<table><thead><tr><th>Field</th><th>说明</th><th>默认值</th></tr></thead><tbody><tr><td>highestSystemLoad</td><td><code>load1</code> 触发值，用于触发自适应控制阶段</td><td>-1 (不生效)</td></tr><tr><td>avgRt</td><td>所有入口流量的平均响应时间</td><td>-1 (不生效)</td></tr><tr><td>maxThread</td><td>入口流量的最大并发数</td><td>-1 (不生效)</td></tr><tr><td>qps</td><td>所有入口资源的 QPS</td><td>-1 (不生效)</td></tr><tr><td>highestCpuUsage</td><td>当前系统的 CPU 使用率（0.0-1.0）</td><td>-1 (不生效)</td></tr></tbody></table>

### @SentinelResource 配置

> @SentinelResource 注解，主要是指定资源名（也可以用请求路径作为资源名），和指定降级处理方法的。

例如：

```
package com.dkf.springcloud.controller;

import com.alibaba.csp.sentinel.annotation.SentinelResource;
import com.alibaba.csp.sentinel.slots.block.BlockException;
import com.dkf.springcloud.entities.CommonResult;
import com.dkf.springcloud.entities.Payment;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class RateLimitController {

    @GetMapping("/byResource")						//处理降级的方法名
    @SentinelResource(value = "byResource", blockHandler = "handleException")
    public CommonResult byResource(){
        return new CommonResult(200, "按照资源名限流测试0K", new Payment(2020L,"serial001"));
    }

    //降级方法
    public CommonResult handleException(BlockException e){
        return new CommonResult(444, e.getClass().getCanonicalName() + "\t 服务不可用");
    }
}

```

![](https://img-blog.csdnimg.cn/img_convert/2ce46af6ddef61d7127ad3e0aeadb206.png)

很明显，上面虽然自定义了兜底方法，但是耦合度太高，下面要解决这个问题。

#### 自定义全局 BlockHandler 处理类

写一个 CustomerBlockHandler 自定义限流处理类：

[外链图片转存失败, 源站可能有防盗链机制, 建议将图片保存下来直接上传 (img-khnkVraZ-1615737211177)(images\1597903188558.png)]

### 整合 openfeign 服务降级

#### 前奏

> 之前有 open-feign 和 hystrix 的整合，现在来实现 sentinel 整合 ribbon + open-feign + fallback 进行服务熔断。
> 
> 新建三个模块，两个提供者 9004、9005，和一个消费者 84
> 
> 目的：
> 
> fallback 管运行异常  
> blockHandIer 管配置违规
> 
> 上面使用 sentinel 有一个很明显的问题，就是 sentinel，对程序内部异常（各种异常，包括超时）这种捕捉，显得很乏力，它主要是针对流量控制，系统吞吐量，或者是异常比例这种，会发生降级或熔断，但是当程序内部发生异常，直接返回给用户错误页面，根本不会触发异常比例这种降级。所以才需要整合 open-feign 来解决程序内部异常时，配置相应的兜底方法

----------------------------------------------------------- 两个提供者模块一致，如下：

pom 依赖：

```
	<dependencies>
        <!-- springcloud alibaba nacos 依赖 -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        
        <!-- springboot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <!-- 日常通用jar包 -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```

yml 配置：

```
server:
  port: 9005  # / 9004
spring:
  application:
    name: nacos-payment-provider
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848
management:
  endpoints:
    web:
      exposure:
        include: '*'

```

主启动类只是启动，没有其它注解。

controller :

```
package com.dkf.sprIngcloud.controller;

import com.dkf.springcloud.entities.CommonResult;
import com.dkf.springcloud.entities.Payment;

@RestController
public class PaymentController {

    @Value("${server.port}")
    private String serverPort;

    //模拟sql查询
    public static HashMap<Long, Payment> hashMap = new HashMap<>();
    static {
        hashMap.put(1L, new Payment(1L, "xcxcxcxcxcxcxcxcxcxcxcxcxc11111111"));
        hashMap.put(2L, new Payment(2L, "xcxcxcxcggggggggg2222222222222222"));
        hashMap.put(3L, new Payment(3L, "xcxcxcxccxxcxcfafdgdgdsgdsgds33333"));
    }


    @GetMapping("/payment/get/{id}")
    public CommonResult paymentSql(@PathVariable("id")Long id){
        Payment payment = hashMap.get(id);
        CommonResult result = new CommonResult(200, "from mysql, server port : " + serverPort + " ,查询成功", payment);
        return result;
    }
}

```

—消费者：

pom 依赖：

```
	<dependencies>
        <!-- 后续做Sentinel的持久化会用到的依赖 -->
        <dependency>
            <groupId>com.alibaba.csp</groupId>
            <artifactId>sentinel-datasource-nacos</artifactId>
        </dependency>
        <!-- sentinel  -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
        </dependency>
        <!-- springcloud alibaba nacos 依赖 -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>

        <!-- springboot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <!-- 日常通用jar包 -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```

yml 配置：

```
server:
  port: 84
spring:
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848
    sentinel:
      transport:
        dashboard: localhost:8080
        port: 8719
  application:
    name: nacos-order-consumer

```

主启动类不用说了。

config 类里面注入 Resttemplate：

```
@Configuration
public class ApplicationContextConfig {
    @Bean
    @LoadBalanced
    public RestTemplate getRestTemplate(){
        return new RestTemplate();
    }
}

```

controller 层：

```
@RestController
public class OrderController {

    private static final String PAYMENT_URL="http://nacos-payment-provider";

    @Resource
    private RestTemplate restTemplate;

    @GetMapping("/consutomer/payment/get/{id}")
    public CommonResult getPayment(@PathVariable("id")Long id){
        if(id >= 4){
            throw new IllegalArgumentException("非法参数异常...");
        }else {
            return restTemplate.getForObject(PAYMENT_URL + "/payment/get/" + id, CommonResult.class);
        }
    }
}

```

上面只实现了 以 nacos 作为服务注册中心，消费者使用 ribbon 实现负载均衡调用提供者的效果。

#### 正式

只配置 fallback:

```
	@GetMapping("/consutomer/payment/get/{id}")
    @SentinelResource(value = "fallback", fallback = "handleFallback") //fallback只处理业务异常
    public CommonResult getPayment(@PathVariable("id")Long id){
        if(id >= 4){
            throw new IllegalArgumentException("非法参数异常...");
        }else {
            return restTemplate.getForObject(PAYMENT_URL + "/payment/get/" + id, CommonResult.class);
        }
    }

    //兜底方法
    public CommonResult handleFallback(@PathVariable("id")Long id, Throwable e){
        return new CommonResult(414, "---非法参数异常--", e);
    }

```

> 业务异常会被 fallback 处理，返回我们自定义的提示信息，而如果给它加上流控，并触发阈值，只能返回 sentinel 默认的提示信息。

只配置 blockHandler:

```
	//@SentinelResource(value = "fallback", fallback = "handleFallback") //fallback只处理业务异常
    @GetMapping("/consutomer/payment/get/{id}")
    @SentinelResource(value = "fallback", blockHandler = "handleblockHandler")
    public CommonResult getPayment(@PathVariable("id")Long id){
        if(id >= 4){
            throw new IllegalArgumentException("非法参数异常...");
        }else {
            return restTemplate.getForObject(PAYMENT_URL + "/payment/get/" + id, CommonResult.class);
        }
    }

//    //====fallback
//    public CommonResult handleFallback(@PathVariable("id")Long id, Throwable e){
//        return new CommonResult(414, "---非法参数异常--", e);
//    }

    //====blockHandler                                       blockHandler的方法必须有这个参数
    public CommonResult handleblockHandler(@PathVariable("id")Long id, BlockException e){
        return new CommonResult(414, "---非法参数异常--", e);
    }

```

> 这时候的效果就是，运行异常直接报错错误页面。在 sentinel 上添加一个降级规则，设置 2s 内触发异常 2 次，触发阈值以后，返回的是我们自定义的 blockhanlder 方法返回的内容。

两者都配置：

```
  //@SentinelResource(value = "fallback", fallback = "handleFallback") //fallback只处理业务异常
    @GetMapping("/consutomer/payment/get/{id}")
    @SentinelResource(value = "fallback", blockHandler = "handleblockHandler", fallback = "handleFallback")
    public CommonResult getPayment(@PathVariable("id")Long id){
        if(id >= 4){
            throw new IllegalArgumentException("非法参数异常...");
        }else {
            return restTemplate.getForObject(PAYMENT_URL + "/payment/get/" + id, CommonResult.class);
        }
    }
    //====fallback
    public CommonResult handleFallback(@PathVariable("id")Long id, Throwable e){
        return new CommonResult(414, "---非法参数异常--form fallback的提示", e);
    }

    //====blockHandler                                       blockHandler的方法必须有这个参数
    public CommonResult handleblockHandler(@PathVariable("id")Long id, BlockException e){
        return new CommonResult(414, "---非法参数异常--", e);
    }

```

> 明显两者都是有效的，可以同时配置。

#### 全局降级

> 上面是单个进行 fallback 和 blockhandler 的测试，下面是整合 openfeign 实现把降级方法解耦。和 Hystrix 几乎一摸一样！

还是使用上面 84 这个消费者做测试：

1.  先添加 open-feign 依赖：

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>

```

2.  yml 追加如下配置：

```
# 激活Sentinel对Feign的支持
feign:
  sentinel:
    enabled: true

```

3.  主启动类添加注解 ： @EnableFeignClients 激活 open-feign
4.  service :

```
@FeignClient(value = "nacos-payment-provider", fallback = PaymentServiceImpl.class)
public interface PaymentService {

    @GetMapping("/payment/get/{id}")
    public CommonResult paymentSql(@PathVariable("id")Long id);
}

```

5.  service 实现类：

```
@Component
public class PaymentServiceImpl implements PaymentService {

    @Override
    public CommonResult paymentSql(Long id) {
        return new CommonResult(414, "open-feign 整合 sentinel 实现的全局服务降级策略",null);
    }
}

```

6.  controller 层代码没什么特殊的，和普通调用 service 一样即可。
7.  测试，关闭提供者的项目，会触发 service 实现类的方法。
8.  总结: 这种全局熔断，是针对 “访问提供者” 这个过程的，只有访问提供者过程中发生异常才会触发降级，也就是这些降级，是给 service 接口上这些提供者的方法加的，以保证在远程调用时能顺利进行。而且这明显是 fallback ，而不是 blockHandler，注意区分。

> fallback 和 blockHandler 肤浅的区别：
> 
> F ： 不需要指定规则，程序内部异常均可触发（超时异常需要配置超时时间）
> 
> B : 配上也没用，必须去 Sentinel 上指定规则才会被触发。

### 异常忽略

> 这是 @SentinelResource 注解的一个值：
> 
> [外链图片转存失败, 源站可能有防盗链机制, 建议将图片保存下来直接上传 (img-0BTijmp8-1615737211178)(images\1597909285814.png)]

### 持久化

> 目前的 sentinel 当重启以后，数据都会丢失，和 nacos 类似原理。需要持久化。它可以被持久化到 nacos 的数据库中。

1.  pom 依赖：

```
<dependency>
    <groupId>com.alibaba.csp</groupId>
    <artifactId>sentinel-datasource-nacos</artifactId>
</dependency>

```

2.  yml 配置：

```
spring:
  cloud:
    sentinel:
      datasource:
        ds1:  
          nacos:
            server-addr: localhost:8848
            dataId: ${spring.application.name}
            group: DEFAULT_GROUP
            data-type: json
            rule-type: flow

```

3.  去 nacos 上创建一个 dataid , 名字和 yml 配置的一致，json 格式，内容如下：

```
[
    {
        "resource": "/testA",
        "limitApp": "default",
        "grade": 1,
        "count": 1,
        "strategy": 0,
        "controlBehavior": 0,
        "clusterMode": false
    }
]

```

resource：资源名称  
limitApp：来源应用  
grade：阈值类型，0 表示线程数，1 表示 QPS，  
count：单机阈值，  
strategy：流控模式，0 表示直接，1 表示关联，2 表示链路

controlBehavior: 流控效果，0 表示快速失败，1 表示 Warm Up,2 表示排队等待；

cIusterM0de 是否集群。

4.  启动应用，发现存在 关于 /testA 请求路径的流控规则。
5.  总结: 就是在 sentinel 启动的时候，去 nacos 上读取相关规则配置信息，实际上它规则的持久化，就是第三步，粘贴到 nacos 上保存下来，就算以后在 sentinel 上面修改了，重启应用以后也是无效的。

Seata
-----

> Seate 处理分布式事务。
> 
> 微服务模块，连接多个数据库，多个数据源，而数据库之间的数据一致性需要被保证。
> 
> 官网： http://seata.io/zh-cn/

Seata 术语： 一 + 三

Transaction ID XID：全局唯一的事务 ID

3 组件概念

*   Transaction Coordinator(TC)：事务协调器，维护全局事务的运行状态，负责协调并驱动全局事务的提交或回滚，
    
*   Transaction Manager™：控制全局事务的边界，负责开启一个全局事务，并最终发起全局提交或全局回滚的决议，
    
*   Resource Manager(RM)：控制分支事务，负责分支汪册、状态汇报，并接收事务协调器的指令，驱动分支（本地）事务提交或回滚
    

1．TM 向 TC 申请开启一个全局事务，全局事务创建成功并生成一个全局唯一的 XID;  
2，XID 在微服务调用链路的上下文中传播；  
3，RM 向 TC 汪册分支事务，将其纳入 XID 对应全局事务的管辖；  
4，TM 向 TC 发起针对 XID 的全局提交或回滚决议；  
5，TC 调度 XID 下管辖的全部分支事务完成提交或回请求。

### 下载安装

> 下载地址 ： https://github.com/seata/seata/releases/download/v1.0.0/seata-server-1.0.0.zip

我们只需要使用一个`@GlobalTransational`注解在业务方法上

### 初始化操作

1.  修改 conf/file.conf 文件：

> 主要修改自定义事务组名称 + 事务日志存储模式为 db + 数据库连接信息
> 
> ```
> service {
>   #transaction service group mapping
>   vgroup_mapping.dkf_tx_group = "default"   # 修改这里
>   #only support when registry.type=file, please don't set multiple addresses
>   default.grouplist = "127.0.0.1:8091"
>   #disable seata
>   disableGlobalTransaction = false
> }
> 
> ## transaction log store, only used in seata-server
> store {
>   ## store mode: file、db
>   mode = "db"   # 修改这里
> 
>   ## file store property
>   file {
>     ## store location dir
>     dir = "sessionStore"
>   }
> 
>   ## database store property
>   db {
>     ## the implement of javax.sql.DataSource, such as DruidDataSource(druid)/BasicDataSource(dbcp) etc.
>     datasource = "dbcp"
>     ## mysql/oracle/h2/oceanbase etc.
>     db-type = "mysql"
>     driver-class-name = "com.mysql.jdbc.Driver"
>     url = "jdbc:mysql://127.0.0.1:3306/seata"
>     user = "root"   # 修改对
>     password = "123456"
>   }
> }
> 
> ```

2.  创建名和 file.conf 指定一致的数据库。
    
3.  在新建的数据库里面创建数据表，db_store.sql 文件在 conf 目录下（1.0.0 有坑，没有 sql 文件，下载 0.9.0 的，使用它的 sql 文件即可）
    
4.  修改 conf/registry.conf 文件内容：
    
    ```
    registry {
      # file 、nacos 、eureka、redis、zk、consul、etcd3、sofa # 默认file
      type = "nacos"
    
      nacos {  # 修改nacos的端口8848
        serverAddr = "localhost:8848"
        namespace = ""
        cluster = "default"
      }
    
    ```
    
5.  先启动 nacos Server 服务，再启动 seata Server 。
    
6.  启动 Seata Server 报错，在 bin 目录创建 /logs/seata_gc.log 文件。再次双击 bat 文件启动。
    

### 案例

#### 数据库准备

这里我们会创建三个服务，一个订单服务，一个库存服务，一个账户服务。

当用户下单时，会在订单服务中创建一个订单，然后通过远程调用库存服务来扣减下单商品的库存，  
再通过远程调用账户服务来扣减用户账户里面的余额，  
最后在订单服务中修改订单状态为已完成。

该操作跨越三个数据库，有两次远程调用，很明显会有分布式事务问题。

创建三个数据库： `seata_account、seata_order、seata_storage`

每个数据库创建数据表：

order 库：

[外链图片转存失败, 源站可能有防盗链机制, 建议将图片保存下来直接上传 (img-4onCJEJp-1615737211179)(images\1597988061545.png)]

account 库：

[外链图片转存失败, 源站可能有防盗链机制, 建议将图片保存下来直接上传 (img-qJgDRh43-1615737211180)(images\1597988768251.png)]

storage 库：

[外链图片转存失败, 源站可能有防盗链机制, 建议将图片保存下来直接上传 (img-HyAlOWpT-1615737211181)(images\1597988262441.png)]

三个数据库都创建一个回滚日志表，seata/conf/ 有相应的 sql 文件（1.0.0 没有，依然使用 0.9.0 中的）。

最终效果：

*   seata
    *   branch_table
    *   global_table
    *   lock_table
*   seata_account
    *   t_account
    *   undo_log
*   seata_order
    *   t_order
    *   undo_log
*   seata_storage
    *   t_storage
    *   undo_log

#### 开发

> 实现 下订单 -> 减库存 -> 扣余额 -> 改（订单）状态
> 
> 需要注意的是，下面做了 seata 与 mybatis 的整合，所以注意一下，和以往的 mybatis 的使用不太一样。

新建模块 cloudalibaba-seata-order2001 ：

pom 依赖：

```
	<dependencies>
        <!-- seata -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
            <exclusions>
                <exclusion>
                    <artifactId>seata-all</artifactId>
                    <groupId>io.seata</groupId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>io.seata</groupId>
            <artifactId>seata-all</artifactId>
            <version>1.0.0</version>
        </dependency>
        <!-- springcloud alibaba nacos 依赖,Nacos Server 服务注册中心 -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>

        <!-- open feign 服务调用 -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>

        <!-- springboot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <!-- 持久层支持 -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <!--mysql-connector-java-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
        <!--jdbc-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <!-- mybatis -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>

        <!-- 日常通用jar包 -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.dkf.cloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
    </dependencies>

```

yml 配置：

```
server:
  port: 2001
spring:
  application:
    name: seata-order-service
  cloud:
    alibaba:
      seata:
        # 自定义事务组，需要和当时在 seata/conf/file.conf 中的一致
        tx-service-group: dkf_tx_group
    nacos:
      discovery:
        server-addr: localhost:8848
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/seata_order
    username: root
    password: 123456


# 注意，这是自定义的，原来的是mapper_locations
mybatis:
  mapperLocations: classpath:mapper/*.xml

logging:
  level:
    io:
      seata: info

```

将 seata/conf/ 下的 file.conf 和 registry.cong 两个文件拷贝到 resource 目录下。

创建 domain 实体类 ： Order 和 CommonResult 两个实体类。

dao :

```
package com.dkf.springcloud.dao;

import org.apache.ibatis.annotations.Mapper;
import com.dkf.springcloud.domain.Order;
import org.apache.ibatis.annotations.Param;

@Mapper
public class OrderDao {

    //创建订单
    public void create(Order order);

    //修改订单状态
    public void update(@Param("userId") Long userId, @Param("status") Integer status);

}

```

Mapper 文件：

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >

<mapper namespace="com.dkf.springcloud.dao.OrderDao">

    <!-- 以备后面会用到 -->
    <resultMap id="BaseResultMap" type="com.dkf.springcloud.domain.Order">
        <id column="id" property="id" jdbcType="BIGINT"></id>
        <result column="user_id" property="userId" jdbcType="BIGINT"></result>
        <result column="product_id" property="productId" jdbcType="BIGINT"></result>
        <result column="count" property="count" jdbcType="INTEGER"></result>
        <result column="money" property="money" jdbcType="DECIMAL"></result>
        <result column="status" property="status" jdbcType="INTEGER"></result>
    </resultMap>

    <insert id="create">
        insert into t_order(id, user_id, product_id, count, money, status)
        values (null, #{userId},#{productId},#{count},#{money},0)
    </insert>

    <update id="update">
        update t_order set status = 1 where user_id=#{userId} and status=#{status}
    </update>

</mapper>

```

创建 service ：

> 注意，红框标记的是通过 open-feign 远程调用微服务的 service
> 
> 远程服务接口有 AccountService、StorageServer
> 
> 而 OrderServiceImpl 实现我们的业务逻辑

serviceImpl :

```
@Service
@Slf4j
public class OrderServiceImpl  implements OrderService {

    @Resource
    private OrderDao orderDao;

    @Resource
    private StorageService storageService;

    @Resource
    private AccountService accountService;

    @Override
    public void create(Order order) {
        log.info("--------》 开始创建订单");
        orderDao.create(order);
        log.info("--------》 订单微服务开始调用库存，做扣减---Count-");
        storageService.decrease(order.getProductId(), order.getCount());
        log.info("--------》 订单微服务开始调用库存，库存扣减完成！！");
        log.info("--------》 订单微服务开始调用账户，账户扣减---money-");
        accountService.decrease(order.getUserId(),order.getMoney());
        log.info("--------》 订单微服务开始调用账户，账户扣减完成!!");
        //修改订单状态，从0到1
        log.info("--------》 订单微服务修改订单状态，start");
        orderDao.update(order.getUserId(),0);
        log.info("--------》 订单微服务修改订单状态，end");

        log.info("--订单结束--");
    }

    @Override
    public void update(Long userId, Integer status) {

    }
}

```

config （特殊点）:

```
//下面是两个配置类，这个是和mybatis整合需要的配置
@Configuration
@MapperScan({"com.dkf.springcloud.alibaba.dao"})
public class MybatisConfig {
}


//这个是配置使用 seata 管理数据源，所以必须配置
package com.dkf.springcloud.config;

import com.alibaba.druid.pool.DruidDataSource;
import io.seata.rm.datasource.DataSourceProxy;
import org.apache.ibatis.session.SqlSessionFactory;
import org.mybatis.spring.SqlSessionFactoryBean;
import org.mybatis.spring.transaction.SpringManagedTransactionFactory;

import org.springframework.core.io.support.PathMatchingResourcePatternResolver;

import javax.sql.DataSource;

@Configuration
public class DataSourceProxyConfig {

    @Value("${mybatis.mapperLocations}")
    private String mapperLocations;

    @Bean
    @ConfigurationProperties(prefix = "spring.datasource")
    public DataSource druidDataSource(){
        return new DruidDataSource();
    }

    @Bean
    public DataSourceProxy dataSourceProxy(DataSource dataSource){
        return new DataSourceProxy(dataSource);
    }

    @Bean
    public SqlSessionFactory sqlSessionFactoryBean(DataSourceProxy dataSourceProxy) throws Exception {
        SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
        sqlSessionFactoryBean.setDataSource(dataSourceProxy);
        sqlSessionFactoryBean.setMapperLocations(new PathMatchingResourcePatternResolver().getResources(mapperLocations));
        sqlSessionFactoryBean.setTransactionFactory(new SpringManagedTransactionFactory());
        return sqlSessionFactoryBean.getObject();
    }
}

```

主启动类：

```
//这里必须排除数据源自动配置，因为写了配置类，让 seata 管理数据源
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)
@EnableFeignClients
@EnableDiscoveryClient
public class SeataOrderMain2001 {

    public static void main(String[] args) {
        SpringApplication.run(SeataOrderMain2001.class,args);
    }
}

```

controller 层调用 orderService 方法即可。

先启动 nacos --》 再启动 seata --> 再启动此 order 服务，测试，可以启动。

仿照上面 创建 cloudalibaba-seata-storage2002 和 cloudalibaba-seata-account2003 两个模块，唯一大的区别就是这两个不需要导入 open-feign 远程调用其它模块。

操，累死老子啦，测试可以正常使用！

#### Seata 使用

```
	@Override
	//只需要在业务类的方法上加上该注解，name值自定义唯一即可。
    @GlobalTransactional(name = "dkf-create-order", rollbackFor = Exception.class)
    public void create(Order order) {
        log.info("--------》 开始创建订单");
        orderDao.create(order);
        log.info("--------》 订单微服务开始调用库存，做扣减---Count-");
        storageService.decrease(order.getProductId(), order.getCount());
        log.info("--------》 订单微服务开始调用库存，库存扣减完成！！");
        log.info("--------》 订单微服务开始调用账户，账户扣减---money-");
        accountService.decrease(order.getUserId(),order.getMoney());
        log.info("--------》 订单微服务开始调用账户，账户扣减完成!!");
        //修改订单状态，从0到1
        log.info("--------》 订单微服务修改订单状态，start");
        orderDao.update(order.getUserId(),0);
        log.info("--------》 订单微服务修改订单状态，end");

        log.info("--订单结束--");
    }

```

```
                      TC :seata 服务器
             
             
   TM                                     RM
  @GlobalTransational                事务的参与方
  事务的发起方

```

原理三个阶段：

[外链图片转存失败, 源站可能有防盗链机制, 建议将图片保存下来直接上传 (img-mTEm1pDL-1615737211183)(images\1597999156669.png)]

[外链图片转存失败, 源站可能有防盗链机制, 建议将图片保存下来直接上传 (img-mbIA72pS-1615737211184)(images\1597999227092.png)]