---
layout: post
title:  "Spring Test"
date:   2021-07-15
categories: spring
permalink: /:categories/spring-test
---

<p style="text-align: justify;">Keeping going on the series about Spring, last one regarding to <a href="https://fabiana2611.github.io/spring/spring-initial-definition">spring concepts</a>, here I start the Spring Test, going around the unit tests, integration tests and configuring the application to test.</p>

<h3>Introduction</h3>

<p style="text-align: justify;">Test is an important part of the development and Spring give to the developers a good support to that activities. The IoC principle used by spring is the key of the benefits. But what to test?</p>

<p style="text-align: justify;">If you are working in a Spring Boot Application you are following a <a href="https://fabiana2611.github.io/foundation/architecture#NTier">N-Tiers</a> architecture because Spring Boot Applications have three layers (Web, Business and Persistence). The test should be created to test each one of those layers individually and integrated. In the same way, you should test the communication with external service or database. </p>

<p style="text-align: justify;">The <strong>unit test</strong> target a small unit of code. Any dependencies are removed from it. The <strong>integration test</strong> target the interaction between the unit parts or different layers.</p>

<table>
  <colgroup>
    <col width="45%" span="1">
    <col width="55%" span="1">
  </colgroup>
  <tr>
    <th>Unit Test</th>
    <th>Integration Test</th>
  </tr>
  <tr>
    <td>
      Test one unit of functionality, <br/>
      Minimal dependencies, <br/>
      Isolated from the environment, <br/>
      Uses stubs/mocks for dependencies.
    </td>
    <td>
      The integration tests will test the interaction of multiple units of work and to test application classes.<br />
      - Goals <a href = "https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/testing.html#integration-testing-goals">[1]</a>:
      <em>
      <li>To manage Spring IoC container caching between tests.</li>
      <li>To provide Dependency Injection of test fixture instances. </li>
      <li>To provide transaction management appropriate to integration testing.</li>
      <li>To supply Spring-specific base classes that assist developers in writing integration tests.</li>
      </em>
    </td>
  </tr>
</table>

<p style="text-align: justify;">When you test a component you have multiple units of test. However, you also can have tests of multiple layers to test the interaction between controller and business, for example, or between the business and repository/API/folders. The same way, you can test the full path, from the controller to repository.</p>

<p><center>
  <img src="/img/spring/teststypes.png" />
</center></p>

<br />

<h3>Good Practices</h3>

<p> The good practices are independent if you use spring or not.</p>

<p style="text-align: justify"><b><u>TDD: </u></b> The Test Driven Design is a way to start the development by the test: (1) RED - start write a test will fail (2) GREEN - Write code enough to pass (3) REFACTOR - Improve code.<a href="https://www.thinktocode.com/2018/02/05/what-is-tdd/">[2]</a></p>

<p style="text-align: justify"><b><u>Builder Pattern: </u></b>Use this pattern improve the test and give support to the reuse of code, scenarios. I'll let here some post with explanation and examples about that. <a href="https://www.javacodegeeks.com/2012/12/using-builder-pattern-in-junit-tests.html">[3]</a></p>

<p style="text-align: justify"><b><u>BDD: </u></b> bahavior-driven development. A good test should be readable by humans. It should be clear and follow a natural language. The methodology <strong>given-when-then</strong> using BDDMockito and AssertJ helps to achieve that goal.<a href="https://en.wikipedia.org/wiki/Behavior-driven_development">[4]</a></p>

<ul>
  <li><strong>given:</strong> precondition and requirements for the application</li>
  <li><strong>when:</strong> the action to be tested.</li>
  <li><strong>then:</strong> verification of the result after execute the action</li>
</ul>

{% highlight ruby %}
# Mockito:
when(methodCall).then(soSomething)
# BDDMockito:
given(methodCall).will(doSomething)
# JUnit:
assertEquals("MyText", obj.getName());
# AssertJ:
assertThat(user.getAge())
  .as("%s should be 100", obj.getName())
  .isEqualTo(100);
# BDDAssertions:
then(obj.getAge()).isEqualTo(40);
{% endhighlight %}

<p><b><u>Libraries</u></b></p>

<ul>
  <li><a href="https://junit.org/junit5/">JUnit 5:</a> <b>@Test, @BeforAll, @Nested, @DisplayName</b></li>
  <li><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.testing">SpringBootTest:</a> <b>@SpringBootTest, @DataJpaTest, @WebMvcTest, @MockBean</b></li>
  <li><a href="https://site.mockito.org/">Mockito:</a> <b>@Mock, @InjectMock</b></li>
  <li><a href="https://assertj.github.io/doc/">AssertJ:</a> <b>assertThat</b></li>
  <li><a href="https://jsonassert.skyscreamer.org/">JSON assertions</a></li>
  <li><a href="https://github.com/json-path/JsonPath">JSONPathe</a></li>
</ul>

@WebMvcTest: Auto configures MockMvc, no need for HTTP server, can be combined with @MockBean to mok=ck collaborators.

<br />

<h3>Spring Support</h3>

<h4><u>Unit Test</u></h4>

<p><b><a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/testing.html#mock-objects">Packages</a></b></p>

<ul>
  <li><b>Environment:</b> <em>"contains mock implementations of the Environment and PropertySource abstractions"</em>.  Tests specifics when you need test specific properties by environment.</li>
  <li><b>JNDI:</b> <em>"contains a partial implementation of the JNDI SPI, which you can use to set up a simple JNDI environment for test suites or stand-alone applications"</em></li>
  <li><b>Servlet API:</b> <em>"contains a comprehensive set of Servlet API mock objects that are useful for testing web contexts, controllers, and filters."</em></li>
  <li><b>Spring Web Reactive:</b> used to mock request and response.</li>
</ul>

<p><b><a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/testing.html#unit-testing-support-classes">Classes</a></b></p>

<ul>
  <li><b>General Testing Utilities:</b> org.springframework.test.util</li>
  <li><b>Spring MVC Testing Utilities:</b> org.springframework.test.web</li>
</ul>

<h4><u>Integration Test</u></h4>

<p><b>Context Management and Caching</b></p>
<ul>
  <li><em>The Spring TestContext Framework provides consistent loading of Spring ApplicationContext instances and WebApplicationContext instances as well as caching of those contexts. By default, once loaded, the configured ApplicationContext is reused for each test. Thus, the setup cost is incurred only once per test suite, and subsequent test execution is much faster.</em><a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/testing.html#testing-ctx-management">[5]</a></li>
</ul>

<p><b>Dependency Injection of Test Fixtures</b></p>
<ul>
  <li><em>When the TestContext framework loads your application context, it can optionally configure instances of your test classes by using Dependency Injection. This provides a convenient mechanism for setting up test fixtures by using preconfigured beans from your application context.</em> <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/testing.html#testing-fixture-di">[6]</a></li>
</ul>

<b>Transaction Management</b>
<ul>
  <li>It is a resource to manage the database state. If you need to test using a real database it will run a rolls back to avoid change the database. <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/testing.html#testing-tx">[7]</a></li>
</ul>

<br />

<h3>Annotations</h3>

<p style="text-align: justify">Spring has a huge number of <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/testing.html#integration-testing-annotations">annotations</a> to help the development. Here a list only some of them with the copy of description that you will find in the spring documentation. In the documentation you can see the complete list.</p>

<ul>
  <li>
    Spring Testing Annotations:
    <ul>
      <li><em><b>@ContextConfiguration</b> defines class-level metadata that is used to determine how to load and configure an ApplicationContext for integration tests. </em></li>
      <li><em><b>@WebAppConfiguration</b>  is a class-level annotation that you can use to declare that the ApplicationContext loaded for an integration test should be a WebApplicationContext. The resource base path is used behind the scenes to create a MockServletContext. </em></li>
      <li><em><b>@ActiveProfiles</b> is a class-level annotation that is used to declare which bean definition profiles should be active when loading an ApplicationContext for an integration test.</em></li>
      <li><em><b>@TestPropertySource</b> is a class-level annotation that you can use to configure the locations of properties files and inlined properties to be added to the set of PropertySources in the Environment for an ApplicationContext loaded for an integration test.</em></li>
      <li><em><b>@DirtiesContext</b> indicates that the underlying Spring ApplicationContext has been dirtied during the execution of a test and should be closed. </em></li>
    </ul>
  </li>
  <li>Standard Annotation Support:
    <ul><li>This category of annotations you can use in the tests and around all the Spring application as @Autowired, @Qualifier, @Value, etc.</li></ul>
  </li>
  <li>Spring JUnit 4 Testing Annotations
    <ul><li>Annotations supported when used with SpringRunner, Spring’s JUnit 4 rules, or Spring’s JUnit 4 support classes: @Timed, @Repeat, @IfProfileValue, @ProfileValueSourceConfiguration </li></ul>
  </li>
  <li>Spring JUnit Jupiter Testing Annotations
    <ul>
      <li><em><b>@SpringJUnitConfig</b> is a composed annotation that combines @ExtendWith(SpringExtension.class) from JUnit Jupiter with @ContextConfiguration from the Spring TestContext Framework. It can be used at the class level as a drop-in replacement for @ContextConfiguration.</em></li>
      <li><em><b>@SpringJUnitWebConfig</b> is a composed annotation that combines @ExtendWith(SpringExtension.class) from JUnit Jupiter with @ContextConfiguration and @WebAppConfiguration from the Spring TestContext Framework. You can use it at the class level as a drop-in replacement for @ContextConfiguration and @WebAppConfiguration.</em></li>
    </ul>
  </li>
</ul>

<p>Go directly to the spring documentation to see detail about the annotation you need.</p>

<br />

<h3>Hands On</h3>

<p style="text-align: justify">I'll present you short examples of unit test, integration test, caching test and test with database. The complete code you can access <a href="https://github.com/fabiana2611/demo-test">here</a>.</p>

<p><li><b><em>Unit Test</em></b></li></p>

<p style="text-align: justify;">Here is one example of a unit test using mocks to simulate a service. </p>

{% highlight ruby %}
@SpringJUnitConfig
public class StudentServiceTest {

  @Mock
  private StudentRepository studentRepository;
  @InjectMocks
  private StudentService service;

  @Test
  void getStudentById_forSavedStudent_isReturned() {

    // given
    Student student = new Student(1L,"Joao", true, 100);
    Mockito.when(studentRepository.findById(1L))
      .thenReturn(Optional.of(student));

    // when
    Student result = service.getStudentById(1L);

    // then
    assertThat(result.getName()).isNotNull();
    assertThat(result.getName()).isEqualTo("Joao");

  }
}
{% endhighlight %}

<br />
<p><li><b><em>Integration Test</em></b></li></p>

<p style="text-align: justify;">Here is an example of an integration test going through the service. The navigation really go inside the service and repository classes. Pay attention to the class annotation and the services annotation. They are different.</p>

{% highlight ruby %}
@SpringBootTest (webEnvironment = WebEnvironment.NONE)
@Transactional
public class StudentServiceTest {

  @Autowired
  private StudentRepository studentRepository;
  @Autowired
  private StudentService studentService;

  @DisplayName("Returning saved student from service layer")
  @Test
  void getStudentById_forSavedStudent_isReturned() {

    // given
    Student savedStudent = studentRepository
      .save(new Student(null, "Joao", true, 100));

    // when
    Student student = studentService.getStudentById(savedStudent.getId());

    // then
    then(student.getName()).isEqualTo("Joao");
    then(student.getId()).isNotNull();

  }
}
{% endhighlight %}

<br />
<p><li><b><em>Rest Test</em></b></li></p>

<p style="text-align: justify;">Here we have an example how to test an rest service using <a href="https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/web/client/TestRestTemplate.html">TestRestTemplate</a>.</p>


{% highlight ruby %}
@Autowired
private TestRestTemplate restTemplate;

@Autowired
private StudentRepository studentRepository;

@Test
public void shouldRetrieveStudent() throws JsonProcessingException {

  Student savedStudent = studentRepository.save(new Student(null, PARAM_QUERY, true, 100));

  ResponseEntity<Student> response = restTemplate.getForEntity("/students/" + PARAM_QUERY, Student.class);

  assertThat(response.getStatusCode()).isEqualTo(HttpStatus.OK);
  assertThat(response.getBody().getId()).isEqualTo(savedStudent.getId());
}
{% endhighlight %}

<p style="text-align: justify;">You can see another example <a href="https://www.baeldung.com/restclienttest-in-spring-boot">here</a>but using <a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/testing.html#spring-mvc-test-client">RestClientTest with MockRestServiceServer</a>. It is a more verbose solution and is necessary to know more detail about the implementation.</p>

<br />
<p><li><b><em>Caching Test</em></b></li></p>

<p style="text-align: justify;">This example verify if your application is using cache. To make it works your main class application should be using the annotation @EnableCaching and the method of the service should be using the @Cacheable("student") annotation. Pay attention now is using <a href="https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/mock/mockito/MockBean.html">@MockBean</a> to the repository. You can see a discussion about use @Mock or @MockBean you can see <a href="https://www.baeldung.com/java-spring-mockito-mock-mockbean">here</a>.</p>

{% highlight ruby %}
@SpringBootTest(webEnvironment = WebEnvironment.NONE)
public class StudentCacheTest {

  @Autowired
  private StudentService service;

  @MockBean
  private StudentRepository repository;

  @Test
  void getStudentById_forMultipleRequests_isRetrievedFromCache() {

    Long id = 123L;
    given(repository.findById(id)).willReturn(Optional.of(new Student(1L,"Joao", true, 100) ));

    service.getStudentById(id);
    service.getStudentById(id);
    service.getStudentById(id);

    then(repository).should(times(1)).findById(id);

  }
}
{% endhighlight %}

<br />
<p><li><b><em>Tests with Database</em></b></li></p>

<p style="text-align: justify">This kind of test use in-memory databases. The data should be loaded before the execution. In this case, is not necessary to use the SpringBooTest because it doesn't need all the application context. Then, the @DataJpaTest annotation is enough.</p>

<p style="text-align: justify">The scenario wants to test the attribute name. The test uses a bean given by Spring, the TestEntityManager. It loads the data before the test. The commented line indicates how NOT to do. The direct use of your repository object will give a wrong answer of the test because the repository object are interacting with the first level cache of jpa repository. The TestEntityManager test entity manager to flush data and make possible the test. To works correctly, the entity Student has to have a default constructor inside the entity class.</p>


{% highlight ruby %}
@DataJpaTest
public class StudentRepositoryTest {

  @Autowired
  private StudentRepository studentRepository;
  @Autowired
  private TestEntityManager testEntityManager;

  @Test
  void testGetObjectByName_ReturnObj() {

    // given
    #Student savedStudent = studentRepository.save(new Student(null, "Joao"));
    Student savedStudent = testEntityManager.persistFlushFind(new Student(null, "Joao", true, 0));

    // when
    Student student = studentRepository.getStudentByName("Joao");

    // then
    then(student.getId()).isNotNull();
    then(student.getName()).isEqualTo(savedStudent.getName());
  }
}
{% endhighlight %}

<p style="text-align: justify">Also, is possible to use the annotation @Sql to define files with queries to prepare the in-memory database to the tests. </p>

<p style="text-align: justify">When the SQL annotation is on the class declaration then the scripts will run before each @Test method. The Sql on the method has priority over the Sql of the class.</p>

{% highlight ruby %}
@SpringIUnitConfig(...)
@Sql({"/scripts/schema.sql", "/scripts/load-data.sql"})
public class MyTest{
  @Test
  @Sql("/scripts/test-data.sql")
  @Sql("/scripts/cleanup-data.sql", executionPhase=Sql.ExecutionPhase.AFTER_TEST_METHOD)
  public void insertNewRecord(){
    ...
  }
}

{% endhighlight %}


<br />

<h3>References</h3>

<ul>
	<li><a href="https://www.linkedin.com/learning/advanced-spring-effective-integration-testing-with-spring-boot">Advanced Spring: Effective Integration Testing with Spring Boot</a></li>
  <li><a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/testing.html#testing" >Spring Doc: Spring Tes</a></li>
  <li><a href="https://www.baeldung.com/bdd-mockito" >BDDMockito</a></li>
  <li><a href="https://www.guru99.com/test-driven-development.html" >What is Test Driven Development (TDD)? Tutorial with Example</a></li>
  <li><a href="https://www.kenneth-truyers.net/2013/07/15/flexible-and-expressive-unit-tests-with-the-builder-pattern/">Flexible and expressive unit tests with the builder pattern</a></li>
  <li><a href="https://arleypadua.medium.com/builder-pattern-applied-to-testing-60e009c427c6">Builder Pattern applied to Unit Testing</a></li>
  <li><a href="https://www.tricentis.com/blog/bdd-behavior-driven-development/">What is BDD (Behavior-Driven Development)?</a></li>
  <li><a href="https://www.departmentofproduct.com/blog/writing-bdd-test-scenarios/">Writing BDD Test Scenarios</a></li>
  <li><a hre="https://rieckpil.de/difference-between-mock-and-mockbean-spring-boot-applications/">Difference Between @Mock and @MockBean (Spring Boot Applications)</a></li>
  <li><a href="https://reflectoring.io/spring-boot-web-controller-test/">Testing MVC Web Controllers with Spring Boot and @WebMvcTest</a></li>
  <li><a href="https://www.arhohuttunen.com/spring-boot-webmvctest/">Testing Web Controllers With Spring Boot @WebMvcTest</a></li>
  <li><a href="https://www.quora.com/What-is-the-difference-between-TestRestTemplate-which-is-present-in-spring-boot-test-dependency-and-a-rest-assured-library">What is the difference between TestRestTemplate, which is present in spring-boot-test dependency, and a rest assured library?</a></li>
  <li><a href="http://www.masterspringboot.com/testing/testing-spring-boot-with-testresttemplate/">Testing Spring Boot with TestRestTemplate</a></li>
  <li><a href="https://www.baeldung.com/spring-mock-rest-template">Mocking a RestTemplate in Spring</a></li>
</ul>
