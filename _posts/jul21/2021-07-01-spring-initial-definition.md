---
layout: post
title:  "Spring - Initial Definitions"
date:   2021-07-01
categories: spring
permalink: /:categories/spring-initial-definition
---

<p style="text-align: justify;">This post will introduce the initial concepts used by Spring in every part of the framework. It is the base to have a good experience and a good understanding to make good decisions in your work. </p>

<p stale="text-align: justify;">If you don't know nothing about Spring you can see an overview about the Spring Ecosystem <a href="https://fabiana2611.github.io/spring/springecosystem">here</a>.</p>

Key Principles:
<ul>
  <li>Don't Repeat Your Self (DRY)</li>
  <li>Separation of Concerns</li>
  <li>Convention Over configuration Testability</li>
</ul>

<h3>The Inversion of Control (IoC) container</h3>

<p style="text-align: justify">The usual <a href="https://en.wikipedia.org/wiki/Control_flow">flow of control</a> is done by programmer. In other words, the programmer is the responsible for, for example, the flow of creating or binding an object and execute the functions. What the <a href="https://en.wikipedia.org/wiki/Inversion_of_control">IoC</a> does is delegate this responsibility to other one, then, the container or framework will be responsible for all lifecycle of that object. </p>

<p style="text-align: justify">The IoC is a principle that allows classes to have low coupling (minimum interdependence). It can be implemented using different patterns as factory, service locator and dependency injection (by constructor, setter or interface).</p>

<p style="text-align: justify">The Spring Framework implements the IoC by Dependence Injection (DI) which can achieved through the constructor (best practice ) and Setters. The BeanFactory and ApplicationContext are part of Spring Framework's IoC container.</p>

<blockquote>(1) The BeanFactory interface provides an advanced configuration mechanism capable of managing any type of object. (2) ApplicationContext is a sub-interface of BeanFactory. It adds easier integration with Spring's AOP features; message resource handling (for use in internationalization), event publication; and application-layer specific contexts such as the WebApplicationContext for use in web applications. <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#beans-introduction">[1]</a></blockquote>


Benefits of IoC:
<ul>
  <li>Less code</li>
  <li>Low coupling</li>
  <li>Make the tests and maintain easier</li>
</ul>


<h3>Configuring the application</h3>

<strong>ApplicationContext</strong>

<p style="text-align: justify">It is the heart of the SpringApplication. It incapsulate the BeanFactory, responsible for the injection of the beans and which handles all singleton beans. The ApplicationContext provides metadata for bean creation, as well, manage the order of creation. An application can have more then one context, as web containers.</p>

<blockquote>The interface org.springframework.context.ApplicationContext represents the Spring IoC container and is responsible for instantiating, configuring, and assembling the aforementioned beans. The ApplicationContext is the interface for an advanced factory capable of maintaining a registry of different beans and their dependencies. <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#beans-basics">[2]</a> <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#beans-factory-client">[3]</a></blockquote>

<p style="text-align: justify">Spring separate application configuration from application objects (beans), then the context manage the beans.</p>

{% highlight ruby %}
// create and configure beans from XML
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");

// create and configure beans from the configuration
// Ex 1
ApplicationContext context = SpringApplication.run(InfrastructureConfig.class);
//Ex 2
ApplicationContext context = new AnnotationConfigApplicationContext(InfrastructureConfig.class);

// retrieve configured instance
MyService service = context.getBean("myService", MyService.class);
{% endhighlight %}

<strong>POM</strong>

The dependencies necessary to use those resource is here:

{% highlight ruby %}
<properties>
  <java.version>11</java.version>
  <spring.version>5.2.3.RELEASE</spring.version>
</properties>

<dependencies>

  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>${spring.version}</version>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>${spring.version}</version>
  </dependency>
</dependencies>
{% endhighlight %}

<strong>Multiple Configurations</strong>

<p style="text-align: justify">The definition or configuration of the beans is done by Spring in separate classes with @Configuration annotation. Also, spring allows create more than one configuration class to support the best practices to separates application and infrastructure configs. The SpringApplication will use the config class which import all the configs. </p>

{% highlight ruby %}
@Configuration
public class ApplicationConfig {
  @Bean
  public MyService myService(MyRepository repository){
    return new MyServiceImpl(repository);
  }
  @Bean
  public MyRepository myRepository(DataSource dataSource){
    return new JdbcMyRepository(dataSource);
  }
}

@Configuration
public class WebConfig {}

@Configuration
@import ({ApplicationConfig.class, WebConfig.class})
public class InfrastructureConfig {
  @Bean
  public DataSource dataSource(){
    BasicDataSource dataSource = new BasicDataSource();
    dataSource.setDriverClassName("org.postgresql.Driver");
    dataSource.setUrl("jdbc:postgresql://localhost/myservicedb");
    dataSource.setUsername("user");
    dataSource.setPassword("pwd");
    return dataSource;
  }
}
{% endhighlight %}

<strong>Environment</strong>

<p style="text-align: justify">Other import resource given by framework is the possibility to use properties files to the configuration. Environment bean represents that properties. Additional properties can be declared using @PropertySource annotation.</p>

{% highlight ruby %}
// Ex 1
@Value {"${db.driver}"}
private String driver;
@Value {"${db.url}"}
private String url;
@Value {"${db.user}"}
private String user;
@Value {"${db.password}"}
private String password;

// Ex 2
@Bean
public DataSource dataSource(Environment env){
  BasicDataSource ds = new BasicDataSource();
  ds.setDriverClassName(env.getProperty("db.driver"));
  ds.setUrl(env.getProperty("db.url"));
  ds.setUser(env.getProperty("db.use"));
  ds.setPassword("db.password"));
}

//Ex 3
@Bean
public DataSource dataSource(
  @Value ("${db.driver}") String driver,
  @Value ("${db.url}") String url,
  @Value ("${db.user}") String user,
  @Value ("${db.password}") String password){
  BasicDataSource ds = new BasicDataSource();
  ds.setDriverClassName(driver);
  ds.setUrl(url);
  ds.setUser(user);
  ds.setPassword(password);
}
{% endhighlight %}  

<strong>Profiles</strong>

<p style="text-align: justify">The <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#beans-definition-profiles">profiles</a> are a resource used by containers to have different beans by environment.</p>

{% highlight ruby %}
#### 1. Example by Class ####
// CLASS 1
@Configuration
@Profile("development")
public class StandaloneDataConfig {
  @Bean
  public DataSource dataSource() {
    return new EmbeddedDatabaseBuilder()
      .setType(EmbeddedDatabaseType.HSQL)
      .addScript("classpath:com/bank/config/sql/schema.sql")
      .build();
    }
}
// CLASS 2
@Configuration
@Profile("production")
public class JndiDataConfig {
  @Bean(destroyMethod="")
  public DataSource dataSource() throws Exception {
    Context ctx = new InitialContext();
    return (DataSource) ctx.lookup("java:comp/env/jdbc/datasource");
  }
}

#### 2. Example by methods ####
@Configuration
public class AppConfig {
  // Using default name
  @Bean("dataSource")
  @Profile("default")
  public DataSource standaloneDataSource() {
    return new EmbeddedDatabaseBuilder()
      .setType(EmbeddedDatabaseType.HSQL)
      .addScript("classpath:com/bank/config/sql/schema.sql")
      .build();
    }

    // Using specific environment name
    @Bean("dataSource")
    @Profile("production")
    public DataSource jndiDataSource() throws Exception {
        Context ctx = new InitialContext();
        return (DataSource) ctx.lookup("java:comp/env/jdbc/datasource");
    }

    // Using exclusion condition
    @Bean
    @Profile("!development")
    public MyService myService(){
      return new MyService();
    }
}

// 3. Activing the profile
AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext();
ctx.getEnvironment().setActiveProfiles("development");
ctx.register(SomeConfig.class, StandaloneDataConfig.class, JndiDataConfig.class);
ctx.refresh();

{% endhighlight %}  
<em>PS: Those examples are in Spring documentation</em>

<strong>Spring Expression Language (SpEL)</strong>

<p style="text-align: justify">The <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#expressions">SpEL</a> is another resource to give support to the configuration. It uses expressions to evolve logic and to return a value.</p>

{% highlight ruby %}
@Value("#{ new Boolean(environment['spring.profiles.active'] != 'dev') }")
private String isDevelopment;
{% endhighlight %}  

<h3>Component Scanning</h3>

<p style="text-align: justify">The use of the root annotation @Component indicate the class should be loaded into the BeanFactory. The @Component is a generic stereotype. Its specialization are @Repository, @Service, @Controller, @RestController, @Configuration. </p>

<p style="text-align: justify">The process scan the package and loads configuration for each bean found. So, it goes through @Autowired, @Qualifier, @Value annotation. The scanning happing in the startup.</p>

<p style="text-align: justify">You can make your class to be autodetected using @ComponentScan(basePackages = "org.example") annotation.</p>

<p style="text-align: justify">Spring adding those new annotation and you can see the benefits to use them instead the standard annotation <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#beans-standard-annotations-limitations">here</a></p>

<p style="text-align: justify">If you needs adding some behavior at startup or shutdown you can use @PostConstruct and @PreDestroy annotation, which are not specific of the Spring. The sequence of the call is:

<p><li>Constructor Injection </li>
<li>Setter Injection</li>
<li>PostConstructor method. </li>
<li>PreDestroy method is called when ConfigurableApplicationContext is closed.</li></p>

<h3>Bean</h3>

<p style="text-align: justify"><a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#beans-definition">BeanDefinition</a> represents the bean's metadadata and contain a package-qualified class name, bean behavioral configuration elements (scope, lifecycle callbacks, etc.), references to other beans and other configuration settings.</p>

<p style="text-align: justify">The instantiating of a bean is done by container through configuration metadata. It can be done using the constructor. By default, the instantiation of beans are eagerly.</p>

<blockquote>When you create a bean by the constructor approach, all normal classes are usable by and compatible with Spring.<a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#beans-factory-class-ctor">[4]</a></blockquote>

{% highlight ruby %}
@component
public class MyClass {

  private FirstService firstService;
  private SecondService secondService;

  @Autowired
  public MyClass(MyService service){
    this.service = service;
  }

  @Autowired
  public void setSecondService(SecondService secondService){
    this.secondService = secondService;
  }

}
{% endhighlight %}

<p style="text-align: justify">Constructor inject make the tests esier comparing to do by fields. It is the priority also comparing to the <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#beans-setter-injection">setter option</a> because ensures required dependencies are not null. One example where setter injection should be used insted constructor injection is to avoid circular dependency.</p>

<strong>Bean Scopes</strong>

<p style="text-align: justify">The beans can be defined using one of the different
<a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#beans-factory-scopes">bean scopes</a>.</p>

<ul>
<li>Singleton: "Scopes a single bean definition to a single object instance for each Spring IoC container."</li>
<li>Prototype: "Scopes a single bean definition to any number of object instances."</li>
<li>Request: "Scopes a single bean definition to the lifecycle of a single HTTP request. "</li>
<li>Session: "Scopes a single bean definition to the lifecycle of an HTTP Session"</li>
<li>Application: "Scopes a single bean definition to the lifecycle of a ServletContext"</li>
<li>WebSocket: "Scopes a single bean definition to the lifecycle of a WebSocket"</li>
</ul>

<strong>The bean lifecycle</strong>

<p>The understanding of the <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#beans-factory-lifecycle">lifecycle</a> helps to define your strategy to develop your application.<p>

Spring Bean container runs through three phases:
<ul>
  <li><strong>Initialization:</strong> creating beans and DI process. It beginnings with creation of ApplicationContext. After that happen the BeanFactory initialization phase (load and process bean definition). Then, it's time of the beans initialization and instantiation, where the beans are really created and managed by the framework.</li>
  <li><strong>Usage:</strong> beans are available</li>
  <li><strong>Destruction:</strong> beans ready for Garbage Collection.</li>
</ul>

<p><center>
  <img src="/img/spring/beanlifecycle.png" width="100%" height="509" />
</center></p>

<br/>
<h3>Spring Pattern</h3>

<p>Here is a list of some patterns you can find in the Spring framework.</p>

<ul>
  <li><b>Inversion Of Control(IoC) Pattern:</b> It is an architectural pattern and it is the core pattern of the Spring wich one the runtime of the framework is based on. It makes Spring manages the dependencies. The objects are injected in runtime. ApplicationContext is the IoC Container.</li>
  <li><b>Factory Pattern:</b> IoC container is a factory. BeanFactory is a data factory.</li>
  <li><b>Builder Patter:</b> A creational pattern used, for example, in MockMvc.</li>
  <li><b>Singleton and Prototype:</b> Most of the configurations use them. Every bean is a singleton by default. The bean configuration is used as prototype.</li>
  <li><b>Adapter:</b> Used in Spring Integration to support communication between two different systems.</li>
  <li><b>Decorator:</b> the framework itself uses decorator. The @Qualifier is a way to use the decorator. It allows add behavior without code modification</li>
  <li><b>Proxy Patter:</b> involved in every object managed by Spring. Allows add new behaviors to improve the use of the framework. Every bean created gets a proxy. Creating proxies in Spring usually resolves around aspect-oriented programming. It is important when operations should be protected and called only when necessary, or to remove object access</li>
  <li><b>Repository:</b> It is a pattern introduced by DDD and used by <a href="https://fabiana2611.github.io/spring/spring-data">Spring Data</a>.</li>
  <li><b>Template Pattern:</b> Most used in remote calls. JDBC and REST are the most common scenario.</li>
  <li><b>MVC:</b> All the Web framework is based on this.</li>
  <li><b>Observer:</b> One example of use is by ApplicationListener interface to observe if ApplicationContext is changed.</li>
  <li><b>Command:</b> One example is in AbstractCommandController in MVC.</li>
  <li><b>Mediator:</b> One example is use this when you need set state of many components at once.</li>
  <li><b>Interpreter:</b> Used by Spring Expression Language.</li>
</ul>

<br/>

<h3>Aspect-Oriented Programming in Spring <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#aop">(AOP)</a></h3>

<blockquote>Aspect-oriented Programming (AOP) complements Object-oriented Programming (OOP) by providing another way of thinking about program structure. The key unit of modularity in OOP is the class, whereas in AOP the unit of modularity is the aspect. Aspects enable the modularization of concerns that cut across multiple types and objects.
</blockquote>

<p>"(1) Provide declarative enterprise services. (2) Let users implement custom aspects, complementing their use of OOP with AOP"</p>

<p>AOP allows reusable blocks of code inject in runtime.</p>

<table>
  <tr>
    <th>Common Applications of Aspects</th>
    <th>Parts of <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#aop-introduction-defn">Spring Aspects</a></th>
  </tr>
  <tr>
    <td>
      <li>Logging</li>
      <li>Transaction management</li>
      <li>Caching</li>
      <li>Security</li>
    </td>
    <td>
    <li>Join point</li>
    <li>Advice</li>
    <li>Pointcut</li>
    </td>
  </tr>
</table>

<p><center>
  <iframe width="560" height="315" src="https://www.youtube.com/embed/Ft29HgsePfQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center></p>

<br />
<h3>Summary</h3>

<p> Here is a good summary about beans. It is in portugues, but I could not left it behind. They are very good.</p>

<table>
  <tr>
    <th>O que é um bean Spring Framework</th>
    <th>Quando Utilizar @Bean em Spring</th>
  </tr>
  <tr>
    <td><iframe width="250" height="150" src="https://www.youtube.com/embed/-PT-pXe-7UM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe width="250" height="150" src="https://www.youtube.com/embed/S6ljIhE6mfY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>
  <tr>
    <th>Profiles</th>
    <th>Cache</th>
  </tr>
  <tr>
    <td><iframe width="250" height="150" src="https://www.youtube.com/embed/Op4SRM3t0nw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe width="250" height="150" src="https://www.youtube.com/embed/cWqNeANzEz0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>
</table>


<h3>References</h3>

<ul>
	<li><a href="https://www.linkedin.com/learning/spring-framework-in-depth-2">Linkedin - Spring: Framework in Depth</a></li>
  <li><a href="https://www.linkedin.com/learning/spring-design-patterns">Linkedin - Spring: Desing Pattern</a></li>
  <li><a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/core.html#spring-core" >Spring Doc: The IoC container</a></li>
  <li><a href="https://martinfowler.com/articles/injection.html" >martinfowler - Inversion of Control Containers and the Dependency Injection pattern</a></li>
  <li><a href="https://www.educative.io/edpresso/what-is-inversion-of-control" >Edutative: What is Inversion of Control?</a></li>
  <li><a href="https://www.tutorialsteacher.com/ioc/inversion-of-control" >TutorialsTeacher - Inversion of Control</a></li>
  <li><a href="https://howtodoinjava.com/spring-core/spring-ioc-vs-di/" >Spring – Inversion of Control vs Dependency Injection</a></li>
  <li><a href="https://www.baeldung.com/inversion-control-and-dependency-injection-in-spring" >Baeldung - Intro to Inversion of Control and Dependency Injection with Spring</a></li>
  <li><a href="https://www.perfomatix.com/inversion-of-controlioc-and-dependency-injection-java-development-services/" >Perfomatix - Inversion of Control(IoC) and Dependency injection(DI) in Java Development Services</a></li>
  <li><a href="https://www.baeldung.com/constructor-injection-in-spring" >Constructor Dependency Injection in Spring</a></li>
</ul>
