# 一、技术体系结构

## 1.1总体技术体系

- 单一架构

    一个项目，一个工程，导出为一个war包，在一个Tomcat上运行。也叫all in one。

    ![](https://secure2.wostatic.cn/static/bnm9zUQo34z7FgXA9vAmfm/image.png?auth_key=1726644439-82FxDs5Kp82XhwNH3Mwv1n-0-4b49548f957f27144eb9dc214714aefe)

    单一架构，项目主要应用技术框架为：Spring , SpringMVC , Mybatis
- 分布式架构

    一个项目（对应 IDEA 中的一个 project），拆分成很多个模块，每个模块是一个 IDEA 中的一个 module。每一个工程都是运行在自己的 Tomcat 上。模块之间可以互相调用。每一个模块内部可以看成是一个单一架构的应用。

    ![](https://secure2.wostatic.cn/static/9NxDdZATsg76FfXNgskTFE/image.png?auth_key=1726644439-e5iWAwRt6Lb23H7ptKJeLf-0-a204d3e0306ffa80bf62c8b7eaf11e11)

    分布式架构，项目主要应用技术框架：SpringBoot (SSM), SpringCloud , 中间件等

## 1.2 框架概念和理解

框架的优点包括以下几点：

1. 提高开发效率：框架提供了许多预先设计好了的组件和工具，能够帮助开发人员快速进行开发。相较于传统手写代码，在框架提供的规范化环境中，开发者可以更快地实现项目的各种要求。
2. 降低开发成本：框架的提供标准化的编程语言、数据操作等代码片段，避免了重复开发的问题，降低了开发成本，提供深度优化的系统，降低了维护成本，增强了系统的可靠性。
3. 提高应用程序的稳定性：框架通常经过了很长时间的开发和测试，其中的许多组件、代码片段和设计模式都得到了验证。重复利用这些组件有助于减少bug的出现，从而提高了应用程序的稳定性。
4. 提供标准化的解决方案：框架通常是针对某个特定领域的，通过提供标准化的解决方案，可以为开发人员提供一种共同的语言和思想基础，有助于更好地沟通和协作。

框架的缺点包括以下几个方面：

1. 学习成本高：框架通常具有特定的语言和编程范式。对于开发人员而言，需要花费时间学习其背后的架构、模式和逻辑，这对于新手而言可能会耗费较长时间。
2. 可能存在局限性：虽然框架提高了开发效率并可以帮助开发人员解决常见问题，但是在某些情况下，特定的应用需求可能超出框架的范围，从而导致应用程序无法满足要求。开发人员可能需要更多的控制权和自由度，同时需要在框架和应用程序之间进行权衡取舍。
3. 版本变更和兼容性问题：框架的版本发布和迭代通常会导致代码库的大规模变更，进而导致应用程序出现兼容性问题和漏洞。当框架变更时，需要考虑框架是否向下兼容，以及如何进行适当的测试、迁移和升级。
4. 架构风险：框架涉及到很多抽象和概念，如果开发者没有足够的理解和掌握其架构，可能会导致系统出现设计和架构缺陷，从而影响系统的健康性和安全性。

站在文件结构的角度理解框架，可以将框架总结：**框架 = jar包+配置文件**

![](https://secure2.wostatic.cn/static/mVVMygbUkcQx9Loxs21XdC/image.png?auth_key=1726644622-iey41CioMigYUbUznvWxjP-0-10d526328b890ecdca9ea30e550f09f4)

莎士比亚说,"一千个观众眼中有一千个哈姆雷特" 即仁者见仁,智者见智.说每个人都会对作品有不同的理解，每个人对待任何事物都有自己的看法，同样的技术解决同样的问题会产生不同流程和风格的解决方案，而采用一种框架其实就是限制用户必须使用其规定的方案来实现，可以降低程序员之间沟通以及日后维护的成本！

常用的单一架构JavaEE项目框架演进，从SSH、SSH2过渡到了SSM：SpringMVC、Spring、MyBatis。

总之，框架已经对基础的代码进行了封装并提供相应的API，开发者在使用框架是直接调用封装好的API可以省去很多代码编写，从而提高工作效率和开发速度。

# 二、SpringFramework介绍

## 2.1 Spring和SpringFramework

**广义的 Spring：Spring 技术栈**（全家桶）

广义上的 Spring 泛指以 Spring Framework 为基础的 Spring 技术栈。

经过十多年的发展，Spring 已经不再是一个单纯的应用框架，而是逐渐发展成为一个由多个不同子项目（模块）组成的成熟技术，例如 Spring Framework、Spring MVC、SpringBoot、Spring Cloud、Spring Data、Spring Security 等，其中 Spring Framework 是其他子项目的基础。

这些子项目涵盖了从企业级应用开发到云计算等各方面的内容，能够帮助开发人员解决软件发展过程中不断产生的各种实际问题，给开发人员带来了更好的开发体验。

**狭义的 Spring：Spring Framework**（基础框架）

狭义的 Spring 特指 Spring Framework，通常我们将它称为 Spring 框架。

Spring Framework（Spring框架）是一个开源的应用程序框架，由SpringSource公司开发，最初是为了解决企业级开发中各种常见问题而创建的。它提供了很多功能，例如：依赖注入（Dependency Injection）、面向切面编程（AOP）、声明式事务管理（TX）等。其主要目标是使企业级应用程序的开发变得更加简单和快速，并且Spring框架被广泛应用于Java企业开发领域。

Spring全家桶的其他框架都是以SpringFramework框架为基础！

## 2.2 SpringFramework主要功能模块

SpringFramework框架结构图：

![](https://secure-bigfile.wostatic.cn/static/5D6E8yWCFE2pUa3koBp4ra/image.png?auth_key=1726644790-iwHog5wMPueiPY4LCqZ4WS-0-5de7cd42ddccd977ec66aaaaf7701133)

| 功能模块       | 功能介绍                                                    |
| -------------- | ----------------------------------------------------------- |
| Core Container | 核心容器，在 Spring 环境下使用任何功能都必须基于 IOC 容器。 |
| AOP&Aspects    | 面向切面编程                                                |
| TX             | 声明式事务管理。                                            |
| Spring MVC     | 提供了面向Web应用程序的集成功能。                           |

## 2.3 SpringFramework主要优势

1. 丰富的生态系统：Spring 生态系统非常丰富，支持许多模块和库，如 Spring Boot、Spring Security、Spring Cloud 等等，可以帮助开发人员快速构建高可靠性的企业应用程序。
2. 模块化的设计：框架组件之间的松散耦合和模块化设计使得 Spring Framework 具有良好的可重用性、可扩展性和可维护性。开发人员可以轻松地选择自己需要的模块，根据自己的需求进行开发。
3. 简化 Java 开发：Spring Framework 简化了 Java 开发，提供了各种工具和 API，可以降低开发复杂度和学习成本。同时，Spring Framework 支持各种应用场景，包括 Web 应用程序、RESTful API、消息传递、批处理等等。
4. 不断创新和发展：Spring Framework 开发团队一直在不断创新和发展，保持与最新技术的接轨，为开发人员提供更加先进和优秀的工具和框架。

因此，这些优点使得 Spring Framework 成为了一个稳定、可靠、且创新的框架，为企业级 Java 开发提供了一站式的解决方案。

Spring 使创建 Java 企业应用程序变得容易。它提供了在企业环境中采用 Java 语言所需的一切，支持 Groovy 和 Kotlin 作为 JVM 上的替代语言，并且可以根据应用程序的需求灵活地创建多种架构。从Spring Framework 6.0.6开始，Spring 需要 Java 17+。

# 三、Spring IoC容器和核心概念

## 3.1 组件和组件管理概念

### 3.1.1 什么是组件

回顾常规的三层架构处理请求流程：

![](https://secure2.wostatic.cn/static/i5cYp4uqLG3mVEKEv2qofF/image.png?auth_key=1726644971-vvMA1LVt1FFCDtGN7aCZNR-0-99c6f5fa3389d190bc7927c23a0c077e)

整个项目就是由各种组件搭建而成的：

![](https://secure2.wostatic.cn/static/8LSuy5YWXmufYmPWM894rN/image.png?auth_key=1726644971-dSP9JzK3FvC9XZbNa3tKU4-0-aeedef28024c852191a899f5b44c4e76)

### 3.1.2 Spring能做什么

- 有人替我们创建组件的对象
- 有人帮我们保存组件的对象
- 有人帮助我们自动组装
- 有人替我们管理事务
- 有人协助我们整合其他框架

### 3.1.3 Spring充当组件管理角色（IoC）

那么谁帮我们完成我们的期待，帮我们管理组件呢？

当然是Spring 框架了！

组件可以完全交给Spring 框架进行管理，Spring框架替代了程序员原有的new对象和对象属性赋值动作等！

Spring具体的组件管理动作包含：

- 组件对象实例化
- 组件属性属性赋值
- 组件对象之间引用
- 组件对象存活周期管理
- ......

我们只需要编写元数据（配置文件）告知Spring 管理哪些类组件和他们的关系即可！

注意：**组件是映射到应用程序中所有可重用组件的Java对象**，应该是可复用的功能对象！

- 组件一定是对象
- 对象不一定是组件

综上所述，Spring 充当一个组件容器，创建、管理、存储组件，减少了我们的编码压力，让我们更加专注进行业务编写！

**组件交给Spring管理的优势**

1. 降低了组件之间的耦合性：Spring IoC容器通过依赖注入机制，将组件之间的依赖关系削弱，减少了程序组件之间的耦合性，使得组件更加松散地耦合。
2. 提高了代码的可重用性和可维护性：将组件的实例化过程、依赖关系的管理等功能交给Spring IoC容器处理，使得组件代码更加模块化、可重用、更易于维护。
3. 方便了配置和管理：Spring IoC容器通过XML文件或者注解，轻松的对组件进行配置和管理，使得组件的切换、替换等操作更加的方便和快捷。
4. 交给Spring管理的对象（组件），方可享受Spring框架的其他功能（AOP,声明事务管理）等

## 3.2 Spring IoC容器和容器实现

### 3.2.1 普通和复杂容器

**普通容器**

  生活中的普通容器

  ![](https://secure2.wostatic.cn/static/t65AXJYvxmQdZB9qcKKy2H/img002.png?auth_key=1726645465-kAnRk2XmkGRyt8gAY7YCvp-0-ad247ead06d8811e5cf02af7c1964aee)

  > 普通容器只能用来存储，没有更多功能。

  程序中的普通容器

  - 数组
  - 集合：List
  - 集合：Set

**复杂容器**

  生活中的复杂容器

  ![](https://secure2.wostatic.cn/static/9DRSuBo1GprKVtd5Gu2GqU/img003.png?auth_key=1726645465-3FDb94V7Uewf2XfaZSt9b7-0-b93cfb1303ff80410ac0024ff4ee7835)

  > 政府管理我们的一生，生老病死都和政府有关。

  程序中的复杂容器

  Servlet 容器能够管理 Servlet(init,service,destroy)、Filter、Listener 这样的组件的一生，所以它是一个复杂容器。

| 名称       | 时机                                                         | 次数 |
| ---------- | ------------------------------------------------------------ | ---- |
| 创建对象   | 默认情况：接收到第一次请求  修改启动顺序后：Web应用启动过程中 | 一次 |
| 初始化操作 | 创建对象之后                                                 | 一次 |
| 处理请求   | 接收到请求                                                   | 多次 |
| 销毁操作   | Web应用卸载之前                                              | 一次 |


我们即将要学习的 SpringIoC 容器也是一个复杂容器。它们不仅要负责创建组件的对象、存储组件的对象，还要负责调用组件的方法让它们工作，最终在特定情况下销毁组件。

总结：Spring管理组件的容器，就是一个复杂容器，不仅存储组件，也可以管理组件之间依赖关系，并且创建和销毁组件等！

### 3.2.2 SpringIoC容器介绍

Spring IoC 容器，负责实例化、配置和组装 bean（组件）。容器通过读取配置元数据来获取有关要实例化、配置和组装组件的指令。配置元数据以 XML、Java 注解或 Java 代码形式表现。它允许表达组成应用程序的组件以及这些组件之间丰富的相互依赖关系。

![](https://secure2.wostatic.cn/static/mFt9PQ2ggCqB193CC57AKi/image.png?auth_key=1726645956-bQ5BruqoeVQwhFBinNegQX-0-02b72c63fef1e1947264fd57c893f4b0)

上图显示了 Spring 容器工作原理的高级视图。应用程序类与配置元数据相结合，您拥有完全配置且可执行的系统或应用程序。

### 3.2.3 SpringIoC容器具体接口和实现类

**SpringIoc容器接口**： 

`BeanFactory` 接口提供了一种高级配置机制，能够管理任何类型的对象，它是SpringIoC容器标准化超接口！

`ApplicationContext` 是 `BeanFactory` 的子接口。它扩展了以下功能：

- 更容易与 Spring 的 AOP 功能集成
- 消息资源处理（用于国际化）
- 特定于应用程序给予此接口实现，例如Web 应用程序的 `WebApplicationContext`

简而言之， `BeanFactory` 提供了配置框架和基本功能，而 `ApplicationContext` 添加了更多特定于企业的功能。 `ApplicationContext` 是 `BeanFactory` 的完整超集！

**ApplicationContext容器实现类**：

| 类型名                             | 简介                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| ClassPathXmlApplicationContext     | 通过读取类路径下的 XML 格式的配置文件创建 IOC 容器对象       |
| FileSystemXmlApplicationContext    | 通过文件系统路径读取 XML 格式的配置文件创建 IOC 容器对象     |
| AnnotationConfigApplicationContext | 通过读取Java配置类创建 IOC 容器对象                          |
| WebApplicationContext              | 专门为 Web 应用准备，基于 Web 环境创建 IOC 容器对象，并将对象引入存入 ServletContext 域中。 |

### 3.2.4 容器管理配置方式

Spring IoC 容器使用多种形式的配置元数据。此配置元数据表示您作为应用程序开发人员如何告诉 Spring 容器实例化、配置和组装应用程序中的对象。

![](https://secure2.wostatic.cn/static/mFt9PQ2ggCqB193CC57AKi/image.png?auth_key=1726646025-eK9sHnH8MVd6ZNWG9N5H8Z-0-c2768186a60f8c642b9e1d1c01036d5f)

Spring框架提供了多种配置方式：XML配置方式、注解方式和Java配置类方式

1. XML配置方式：是Spring框架最早的配置方式之一，通过在XML文件中定义Bean及其依赖关系、Bean的作用域等信息，让Spring IoC容器来管理Bean之间的依赖关系。该方式从Spring框架的第一版开始提供支持。
2. 注解方式：从Spring 2.5版本开始提供支持，可以通过在Bean类上使用注解来代替XML配置文件中的配置信息。通过在Bean类上加上相应的注解（如@Component, @Service, @Autowired等），将Bean注册到Spring IoC容器中，这样Spring IoC容器就可以管理这些Bean之间的依赖关系。
3. **Java配置类**方式：从Spring 3.0版本开始提供支持，通过Java类来定义Bean、Bean之间的依赖关系和配置信息，从而代替XML配置文件的方式。Java配置类是一种使用Java编写配置信息的方式，通过@Configuration、@Bean等注解来实现Bean和依赖关系的配置。

为了迎合当下开发环境，我们将以**配置类+注解方式**为主进行讲解！

## 3.3 Spring IoC/DI概念总结

- **IoC容器**

  Spring IoC 容器，负责实例化、配置和组装 bean（组件）核心容器。容器通过读取配置元数据来获取有关要实例化、配置和组装组件的指令。

- **IoC（Inversion of Control）控制反转**

  IoC 主要是针对对象的创建和调用控制而言的，也就是说，当应用程序需要使用一个对象时，不再是应用程序直接创建该对象，而是由 IoC 容器来创建和管理，即控制权由应用程序转移到 IoC 容器中，也就是“反转”了控制权。这种方式基本上是通过依赖查找的方式来实现的，即 IoC 容器维护着构成应用程序的对象，并负责创建这些对象。

- **DI (Dependency Injection) 依赖注入**

  DI 是指在组件之间传递依赖关系的过程中，将依赖关系在容器内部进行处理，这样就不必在应用程序代码中硬编码对象之间的依赖关系，实现了对象之间的解耦合。在 Spring 中，DI 是通过 XML 配置文件或注解的方式实现的。它提供了三种形式的依赖注入：构造函数注入、Setter 方法注入和接口注入。

# 四、SpringIoC实践和应用

## 4.1 Spring IoC/DI实现步骤

> 我们总结下，组件交给Spring IoC容器管理，并且获取和使用的基本步骤！

1. **配置元数据（配置）**

    配置元数据，既是编写交给SpringIoC容器管理组件的信息，配置方式有三种。

    基于 XML 的配置元数据的基本结构：

    <bean id="..." [1] class="..." [2]>  
    <!-- collaborators and configuration for this bean go here -->
    </bean>

```XML
<?xml version="1.0" encoding="UTF-8"?>
<!-- 此处要添加一些约束，配置文件的标签并不是随意命名 -->
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.springframework.org/schema/beans
    https://www.springframework.org/schema/beans/spring-beans.xsd">

  <bean id="..." [1] class="..." [2]>  
    <!-- collaborators and configuration for this bean go here -->
  </bean>

  <bean id="..." class="...">
    <!-- collaborators and configuration for this bean go here -->
  </bean>
  <!-- more bean definitions go here -->
</beans>
```

```xml
Spring IoC 容器管理一个或多个组件。这些 组件是使用你提供给容器的配置元数据（例如，以 XML `<bean/>` 定义的形式）创建的。

<bean /> 标签 == 组件信息声明

- `id` 属性是标识单个 Bean 定义的字符串。
- `class` 属性定义 Bean 的类型并使用完全限定的类名。
```

2.**实例化IoC容器**

提供给 `ApplicationContext` 构造函数的位置路径是资源字符串地址，允许容器从各种外部资源（如本地文件系统、Java `CLASSPATH` 等）加载配置元数据。

我们应该选择一个合适的容器实现类，进行IoC容器的实例化工作：

```Java
//实例化ioc容器,读取外部配置文件,最终会在容器内进行ioc和di动作
ApplicationContext context = 
           new ClassPathXmlApplicationContext("services.xml", "daos.xml");
```
3.**获取Bean（组件）**

`ApplicationContext` 是一个高级工厂的接口，能够维护不同 bean 及其依赖项的注册表。通过使用方法 `T getBean(String name, Class<T> requiredType)` ，您可以检索 bean 的实例。

允许读取 Bean 定义并访问它们，如以下示例所示：

```Java
//创建ioc容器对象，指定配置文件，ioc也开始实例组件对象
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");
//获取ioc容器的组件对象
PetStoreService service = context.getBean("petStore", PetStoreService.class);
//使用组件对象
List<String> userList = service.getUsernameList();
```

## 4.2 基于XML配置方式组件管理

### 4.2.1 实验一：Bean信息声明配置（IoC）

1. 目标

    Spring IoC 容器管理一个或多个 bean。这些 Bean 是使用您提供给容器的配置元数据创建的（例如，以 XML `<bean/>` 定义的形式）。

    我们学习，如何通过定义XML配置文件，声明组件类信息，交给 Spring 的 IoC 容器进行组件管理！
2. 思路

    ![](https://secure2.wostatic.cn/static/rMxd5wJzZ4WaVCyCt5Tazm/img006.png?auth_key=1726647308-jUGeB3iRKFNMuaz4wbiKEL-0-a082545411e9b4b2f356ceb69690d3f7)
3. 准备项目
    1. 创建maven工程（spring-ioc-xml-01）
    2. 导入SpringIoC相关依赖

        pom.xml

```XML
<dependencies>
    <!--spring context依赖-->
    <!--当你引入Spring Context依赖之后，表示将Spring的基础依赖引入了-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>6.0.6</version>
    </dependency>
    <!--junit5测试-->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.3.1</version>
    </dependency>
</dependencies>
```
4. 基于无参数构造函数

    > 当通过构造函数方法创建一个 bean（组件对象） 时，所有普通类都可以由 Spring 使用并与之兼容。也就是说，正在开发的类不需要实现任何特定的接口或以特定的方式进行编码。只需指定 Bean 类信息就足够了。但是，默认情况下，我们需要一个默认（空）构造函数。

    1. 准备组件类

```Java
package com.atguigu.ioc;


public class HappyComponent {

    //默认包含无参数构造函数

    public void doWork() {
        System.out.println("HappyComponent.doWork");
    }
}
```
    2. xml配置文件编写
    
        创建携带spring约束的xml配置文件
    
        ![](https://secure2.wostatic.cn/static/7eC1WeTyXz1oLaGkPfJBfh/image.png?auth_key=1726647308-5YdUsbfKgoVHRBt2GZvb2G-0-63e4e102c59890aef6d7af8ceafd8e90)
    
        编写配置文件：
    
        文件：resources/spring-bean-01.xml

```Java
<!-- 实验一 [重要]创建bean -->
<bean id="happyComponent" class="com.atguigu.ioc.HappyComponent"/>
```

        - bean标签：通过配置bean标签告诉IOC容器需要创建对象的组件信息
        - id属性：bean的唯一标识,方便后期获取Bean！
        - class属性：组件类的全限定符！
        - 注意：要求当前组件类必须包含无参数构造函数！
5. 基于静态工厂方法实例化

    > 除了使用构造函数实例化对象，还有一类是通过工厂模式实例化对象。接下来我们讲解如何定义使用静态工厂方法创建Bean的配置 ！

    1. 准备组件类

```Java
public class ClientService {
  private static ClientService clientService = new ClientService();
  private ClientService() {}

  public static ClientService createInstance() {
  
    return clientService;
  }
}
```
    2. xml配置文件编写
    
        文件：resources/spring-bean-01.xml

```XML
<bean id="clientService"
  class="examples.ClientService"
  factory-method="createInstance"/>
```

        - class属性：指定工厂类的全限定符！
        - factory-method: 指定静态工厂方法，注意，该方法必须是static方法。
6. 基于实例工厂方法实例化

    > 接下来我们讲解下如何定义使用实例工厂方法创建Bean的配置 ！

    1. 准备组建类

```Java
public class DefaultServiceLocator {

  private static ClientServiceImplclientService = new ClientServiceImpl();

  public ClientService createClientServiceInstance() {
    return clientService;
  }
}
```
    2. xml配置文件编写
    
        文件：resources/spring-bean-01.xml

```XML
<!-- 将工厂类进行ioc配置 -->
<bean id="serviceLocator" class="examples.DefaultServiceLocator">
</bean>

<!-- 根据工厂对象的实例工厂方法进行实例化组件对象 -->
<bean id="clientService"
  factory-bean="serviceLocator"
  factory-method="createClientServiceInstance"/>
```

        - factory-bean属性：指定当前容器中工厂Bean 的名称。
        - factory-method:  指定实例工厂方法名。注意，实例方法必须是非static的！
7. 图解IoC配置流程

    ![](https://secure2.wostatic.cn/static/mpqqiD6Bmbno45SpRwBNom/image.png?auth_key=1726647308-dv999VpBn6vGvFQfNEm97Q-0-629864ddde3b5033df2eb5649fa76c35)

### 4.2.2 Bean依赖注入配置（DI）

1. 目标

    通过配置文件,实现IoC容器中Bean之间的引用（依赖注入DI配置）。

    主要涉及注入场景：基于构造函数的依赖注入和基于 Setter 的依赖注入。
2. 思路

    ![](https://secure2.wostatic.cn/static/opfLAb8XnCZDyPMm9BuiMc/image.png?auth_key=1726649286-pZKKA77ux2AgTWsYygW3fd-0-515e4560fd513649cfd5338cb46dd8fb)
3. 基于构造函数的依赖注入（单个构造参数）
    1. 介绍

        基于构造函数的 DI 是通过容器调用具有多个参数的构造函数来完成的，每个参数表示一个依赖项。

        下面的示例演示一个只能通过构造函数注入进行依赖项注入的类！
    2. 准备组件类

```Java
public class UserDao {
}


public class UserService {
    
    private UserDao userDao;

    public UserService(UserDao userDao) {
        this.userDao = userDao;
    }
}

```
    3. 编写配置文件
    
        文件：resources/spring-02.xml

```XML
<beans>
  <!-- 引用类bean声明 -->
  <bean id="userService" class="x.y.UserService">
   <!-- 构造函数引用 -->
    <constructor-arg ref="userDao"/>
  </bean>
  <!-- 被引用类bean声明 -->
  <bean id="userDao" class="x.y.UserDao"/>
</beans>
```

        - constructor-arg标签：可以引用构造参数 ref引用其他bean的标识。
4. 基于构造函数的依赖注入（多构造参数解析）
    1. 介绍

        基于构造函数的 DI 是通过容器调用具有多个参数的构造函数来完成的，每个参数表示一个依赖项。

        下面的示例演示通过构造函数注入多个参数，参数包含其他bean和基本数据类型！
    2. 准备组件类

```Java
public class UserDao {
}


public class UserService {
    
    private UserDao userDao;
    
    private int age;
    
    private String name;

    public UserService(int age , String name ,UserDao userDao) {
        this.userDao = userDao;
        this.age = age;
        this.name = name;
    }
}
```
    3. 编写配置文件

```XML
<!-- 场景1: 多参数，可以按照相应构造函数的顺序注入数据 -->
<beans>
  <bean id="userService" class="x.y.UserService">
    <!-- value直接注入基本类型值 -->
    <constructor-arg  value="18"/>
    <constructor-arg  value="赵伟风"/>
    
    <constructor-arg  ref="userDao"/>
  </bean>
  <!-- 被引用类bean声明 -->
  <bean id="userDao" class="x.y.UserDao"/>
</beans>


<!-- 场景2: 多参数，可以按照相应构造函数的名称注入数据 -->
<beans>
  <bean id="userService" class="x.y.UserService">
    <!-- value直接注入基本类型值 -->
    <constructor-arg name="name" value="赵伟风"/>
    <constructor-arg name="userDao" ref="userDao"/>
    <constructor-arg name="age"  value="18"/>
  </bean>
  <!-- 被引用类bean声明 -->
  <bean id="userDao" class="x.y.UserDao"/>
</beans>

<!-- 场景2: 多参数，可以按照相应构造函数的角标注入数据 
           index从0开始 构造函数(0,1,2....)
-->
<beans>
    <bean id="userService" class="x.y.UserService">
    <!-- value直接注入基本类型值 -->
    <constructor-arg index="1" value="赵伟风"/>
    <constructor-arg index="2" ref="userDao"/>
    <constructor-arg index="0"  value="18"/>
  </bean>
  <!-- 被引用类bean声明 -->
  <bean id="userDao" class="x.y.UserDao"/>
</beans>

```
        - constructor-arg标签：指定构造参数和对应的值
        - constructor-arg标签：name属性指定参数名、index属性指定参数角标、value属性指定普通属性值
5. **基于Setter方法依赖注入**
    1. 介绍

        开发中，除了构造函数注入（DI）更多的使用的Setter方法进行注入！

        下面的示例演示一个只能使用纯 setter 注入进行依赖项注入的类。
    2. 准备组件类

```Java
public Class MovieFinder{

}

public class SimpleMovieLister {

  private MovieFinder movieFinder;
  
  private String movieName;

  public void setMovieFinder(MovieFinder movieFinder) {
    this.movieFinder = movieFinder;
  }
  
  public void setMovieName(String movieName){
    this.movieName = movieName;
  }

  // business logic that actually uses the injected MovieFinder is omitted...
}
```
    3. 编写配置文件

```XML
<bean id="simpleMovieLister" class="examples.SimpleMovieLister">
  <!-- setter方法，注入movieFinder对象的标识id
       name = 属性名  ref = 引用bean的id值
   -->
  <property name="movieFinder" ref="movieFinder" />

  <!-- setter方法，注入基本数据类型movieName
       name = 属性名 value= 基本类型值
   -->
  <property name="movieName" value="消失的她"/>
</bean>

<bean id="movieFinder" class="examples.MovieFinder"/>

```
        - property标签： 可以给setter方法对应的属性赋值
        - property 标签： name属性代表**set方法标识**、ref代表引用bean的标识id、value属性代表基本属性值

**总结：**

  依赖注入（DI）包含引用类型和基本数据类型，同时注入的方式也有多种！主流的注入方式为setter方法注入和构造函数注入，两种注入语法都需要掌握！

  需要特别注意：引用其他bean，使用ref属性。直接注入基本类型值，使用value属性。

### 4.2.3 IoC容器创建与使用

1. 介绍

    上面的实验只是讲解了如何在XML格式的配置文件编写IoC和DI配置！

    如图：

    ![](https://secure2.wostatic.cn/static/ngQZT7qhVfAzTxrr2oX1ny/image.png?auth_key=1726650527-qkteJV94qvk4vhFGw9gv7Z-0-d1a969af1493266195c44affda04bb1f)

    想要配置文件中声明组件类信息真正的进行实例化成Bean对象和形成Bean之间的引用关系，我们需要声明IoC容器对象，读取配置文件，实例化组件和关系维护的过程都是在IoC容器中实现的！
2. 容器实例化

```Java
//方式1:实例化并且指定配置文件
//参数：String...locations 传入一个或者多个配置文件
ApplicationContext context = 
           new ClassPathXmlApplicationContext("services.xml", "daos.xml");
           
//方式2:先实例化，再指定配置文件，最后刷新容器触发Bean实例化动作 [springmvc源码和contextLoadListener源码方式]  
ApplicationContext context = 
           new ClassPathXmlApplicationContext();   
//设置配置配置文件,方法参数为可变参数,可以设置一个或者多个配置
iocContainer1.setConfigLocations("services.xml", "daos.xml");
//后配置的文件,需要调用refresh方法,触发刷新配置
iocContainer1.refresh();           

```
3. Bean对象读取

```Java
//方式1: 根据id获取
//没有指定类型,返回为Object,需要类型转化!
HappyComponent happyComponent = 
        (HappyComponent) iocContainer.getBean("bean的id标识");
        
//使用组件对象        
happyComponent.doWork();

//方式2: 根据类型获取
//根据类型获取,但是要求,同类型(当前类,或者之类,或者接口的实现类)只能有一个对象交给IoC容器管理
//配置两个或者以上出现: org.springframework.beans.factory.NoUniqueBeanDefinitionException 问题
HappyComponent happyComponent = iocContainer.getBean(HappyComponent.class);
happyComponent.doWork();

//方式3: 根据id和类型获取
HappyComponent happyComponent = iocContainer.getBean("bean的id标识", HappyComponent.class);
happyComponent.doWork();

根据类型来获取bean时，在满足bean唯一性的前提下，其实只是看：『对象 instanceof 指定的类型』的返回结果，
只要返回的是true就可以认定为和类型匹配，能够获取到。
```

p24

## 4.3 基于注解方式管理Bean

## 4.4 基于配置类方式管理Bean

## 4.5 三种配置方式总结

## 4.6 整合Spring5-Test5搭建测试环境

# 五、Spring AOP面向切面编程

# 六、Spring声明式事务

# 七、Spring核心掌握总结