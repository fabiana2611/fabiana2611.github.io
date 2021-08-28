---
layout: post
title:  "Spring Security"
date:   2021-08-28
categories: spring
permalink: /:categories/spring-security
---

<p style="text-align: justify;">Spring Security is part of <a href="https://fabiana2611.github.io/spring/springecosystem">Spring Ecosystem</a> that will help manage an application's <a href="https://auth0.com/docs/get-started/authentication-and-authorization">Authentication and Authorization</a> requirements, as well as protection against <a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#exploits">common exploits</a>.</p>

<p style="text-align: justify;">The authentication validates WHO can enter the application, and the authorization verifies WHAT the authorized user can access. Some techniques used to authenticate a user are <a href="https://docs.oracle.com/cd/E19424-01/820-4811/gdzeq/index.html">Password-based authentication</a>, <a href="https://auth0.com/docs/connections/passwordless">Passwordless authentication</a>, <a href="https://auth0.com/blog/what-is-and-how-does-single-sign-on-work/">Single sign-on (SSO)</a> and <a href="https://auth0.com/learn/social-login/">Social authentication</a>. Some techniques of authorization are <a href="https://auth0.com/docs/authorization/rbac/">Role-based access controls (RBAC)</a>, <a href="https://auth0.com/docs/tokens/json-web-tokens">JSON web token (JWT)</a>, <a href="https://auth0.com/blog/how-saml-authentication-works/">SAML</a>, <a href="https://auth0.com/docs/protocols/openid-connect-protocol">OpenID</a> and <a href="https://www.csoonline.com/article/3216404/what-is-oauth-how-the-open-authorization-framework-works.html">OAuth</a>.</p>

<blockquote>Spring Security is a powerful and highly customizable authentication and access-control framework.  Like all Spring projects, the real power of Spring Security is found in how easily it can be extended to meet custom requirements <a href="https://spring.io/projects/spring-security">[1]</a></blockquote>

<table>
  <tr>
    <th>What is Spring Security</th>
    <th>Authentication vs authorization</th>
  </tr>
  <tr>
    <td>
        <iframe width="310" height="215" src="https://www.youtube.com/embed/sm-8qfMWEV8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </td>
    <td>
      <iframe width="310" height="215" src="https://www.youtube.com/embed/I0poT4UxFxE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </td>
  </tr>
</table>

<h3>Dependencies</h3>

<p style="text-align: justify;"><b>spring-security-core</b> gives support to authentication and access control. It supports non-web applications, method level security and JDBC. Web security infrastructure is available using <b>spring-security-web</b> dependency. The <b> spring-security-config</b> dependency is necessary to use Spring Security XML namespace and annotations. The different ways to guarantee the secirity have their own dependencies: <b>spring-security-ldap, spring-security-acl, spring-security-cas, spring-security-oauth, spring-security-openid</b>.</p>

<em><u><b>With Spring Boot</b></u></em>

{% highlight ruby %}
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-security</artifactId>
  <version>${spring-security.version}</version>
</dependency>
{% endhighlight %}

<em><u><b>Without Spring Boot</b></u></em>

{% highlight ruby %}
<dependency>
  <groupId>org.springframework.security</groupId>
  <artifactId>spring-security-core</artifactId>
  <version>${spring-security.version}</version>
</dependency>
<dependency>
  <groupId>org.springframework.security</groupId>
  <artifactId>spring-security-web</artifactId>
  <version>${spring-security.version}</version>
</dependency>
<dependency>
  <groupId>org.springframework.security</groupId>
  <artifactId>spring-security-config</artifactId>
  <version>${spring-security.version}</version>
</dependency>
{% endhighlight %}

<p>All modules you can see <a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#modules">here</a>.</p>

<p><center>
  <iframe width="100%" height="215" src="https://www.youtube.com/embed/PhG5p_yv0zs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center></p>

<h3>Initial Config</h3>

<p style="text-align: justify;">The first step is to create a class that extends from WebSecurityConfigurerAdapter and with annotation @EnableWebSecurity in case you need integration with MVC. After that we can override the method to use the HttpSecurity instance. </p>

<p style="text-align: justify;">The example bellow says to any request the user have to be authenticated, and the way to authenticate is HTTP Basic. You also can use formLogin.</p>

{% highlight ruby %}
public class MySecurityConfig extends WebSecurityConfigurerAdapter{

  @Override
  public void configure(final HttpSecurity http) throws Exception {
    http.authorizeRequests().anyRequest().authenticated()
      .and()
      .httpBasic();
      //.formLogin();
  }

  @Override
  public void configure(AuthenticationManagerBuilder builder) throws Exception {
    builder.inMemoryAuthentication()
      .withUser("maria").password("123").roles("USER")
      .and()
      .withUser("jose").password("123").roles("USER");
    }
}
{% endhighlight %}

<p style="text-align: justify;">This post will use in-memory authentication to test, that's why we also override the second configure method. After that you can run the app and do your first test.</p>

<p>
  <table>
    <tr>
      <th>httpBasic()</th>
      <th>formLogin()</th>
    </tr>
    <tr>
      <td><img src="/img/spring/login_httpbasic.png" width="60%"/></td>
      <td><img src="/img/spring/formlogin.png" width="60%"/></td>
    </tr>
  </table>
</p>

<p style="text-align: justify;">In case to improve the access rules you can add it in the configure method. In this case you start to work with authorization.</p>

{% highlight ruby %}
@Override
public void configure(final HttpSecurity http) throws Exception {
  http.authorizeRequests()
      .antMatchers("/test/**").hasRole("USER")
      .antMatchers("/anonymous*").anonymous()
      .antMatchers("/login*").permitAll()
  .anyRequest().authenticated().and().httpBasic();
}
{% endhighlight %}

<p style="text-align: justify;">In case to use JDBC, one example of how to authenticate the use is below, where you inform the datasource, some encoder and you queries.</p>

{% highlight ruby %}
@Override
protected void configure(AuthenticationManagerBuilder builder) throws Exception {
  builder
      .jdbcAuthentication()
      .dataSource(dataSource)
      .passwordEncoder(new BCryptPasswordEncoder())
      .usersByUsernameQuery(<YOUR_QUERY>)
      .authoritiesByUsernameQuery(<YOUR_QUERY>)
      .groupAuthoritiesByUsername(<YOUR_QUERY>)
      .rolePrefix("ROLE_");
}
{% endhighlight %}

<p style="text-align: justify;">That example use passwordEncoder. It is a way to allow the password to be stored securely. Before Spring Security 5.0, the default was NoOpPasswordEncoder, now it can be BCryptPasswordEncoder. The Spring Security has <a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#authentication-password-storage-dpe">DelegatingPasswordEncoder</a> to make possible work with legacy and modern formats. Here the example gotten from spring doc.</p>

{% highlight ruby %}
String idForEncode = "bcrypt";
Map encoders = new HashMap<>();
encoders.put(idForEncode, new BCryptPasswordEncoder());
encoders.put("noop", NoOpPasswordEncoder.getInstance());
encoders.put("pbkdf2", new Pbkdf2PasswordEncoder());
encoders.put("scrypt", new SCryptPasswordEncoder());
encoders.put("sha256", new StandardPasswordEncoder());

PasswordEncoder passwordEncoder =
    new DelegatingPasswordEncoder(idForEncode, encoders);

// Test the pws by comparation
String result = encoders.get(idForEncode).encode("myPassword");
assertTrue(encoder.matches("myPassword", result));
{% endhighlight %}

<p style="text-align: justify;">However, many application use JPA. In this case, the application can use the UserDetailsService interface. The override method search by user and Spring Security will validate the password.</p>

{% highlight ruby %}
public class MyUserDetailsService implements UserDetailsService{
  @Override
  public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
    User user = usersRepository.findByLogin(username);
    if(user == null) {
      throw new RuntimeException();
    }
    return new MyUserSystem(user.getLogin(), user.getPassword(), searchPermission(user));
  }
}
{% endhighlight %}


<table>
  <tr>
    <th>Config Authentication - AuthenticationManagerBuilder</th>
    <th>Config Authorization - HttpSecurity</th>
  </tr>
  <tr>
    <td>
        <iframe width="310" height="215" src="https://www.youtube.com/embed/iyXne7dIn7U" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </td>
    <td>
      <iframe width="310" height="215" src="https://www.youtube.com/embed/payxWrmF_0k" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </td>
  </tr>
</table>

<h3>Architecture</h3>

<p style="text-align: justify;">The Spring <a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#servlet-architecture">architecture</a> is based on <a href="">Servlet Filters</a>.</p>

<blockquote>
The client sends a request to the application, and the container creates a FilterChain which contains the Filters and Servlet that should process the HttpServletRequest based on the path of the request URI. In a Spring MVC application the Servlet is an instance of DispatcherServlet. At most one Servlet can handle a single HttpServletRequest and HttpServletResponse
</blockquote>

<p style="text-align: justify;">The DelegatingFilterProxy is one filter implemented by Sprint to delegate all the work to a Spring Bean. It allows the controls by ApplicationContext.</p>

<p style="text-align: justify;">The FilterChainProxy is a filter to delegate Filter instances through SecurityFilterChain, which is responsible to define the Spring Security Filter (beans registered with FilterChainProxy) to be invoked. The ExceptionTranslationFilter (translation of AccessDeniedException and AuthenticationException into HTTP Response) is inserted into the FilterChainProxy.</p>

<p><center>
  <iframe width="100%" height="215" src="https://www.youtube.com/embed/caCJAJC41Rk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center></p>

<h3>Components and Mechanisms</h3>

<p style="text-align: justify;">The support to authentication on Spring is possible by many <b>components</b> as <u>SecurityContextHolder, Authentication, ProviderManager</u>. </p>

<p style="text-align: justify;">Furthermore, Spring gives support to a few sorts of <b>authentication mechanisms</b> as: </p>

<ul>
  <li>Username/Password - has different ways to read data from HttpServletRequest: by <b>Form Login, Basic Authentication and Digest Authentication</b>. The mechanism to storage those data are <b>In-Memory Authentication, JDBC Authentication, UserDetailsService and LDAP Authentication</b></li>
  <li>OAuth 2.0: capability to have users log in to the application by using existing account (e.g. google account) </li>
  <li>Remember Me - remember the identity of a principal between sessions </li>
  <li>Central Authentication Server (CAS) - enterprise-wide single sign on system </li>
  <li>SAML (Security Assertion Markup Language): enables single sign-on (SSO) </li>
  <li>JAAS (Java Authentication and Authorization Service) - extension library that use the standard Pluggable Authentication Module (PAM)</li>
  <li>OpenID - as form-based login but adding openid provider </li>
  <li>X.509 - when server use ssl: using certificate</li>
</ul>

<p style="text-align: justify;">All the components and Authentication Mechanisms you can find <a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#servlet-authentication">here</a>.</p>

<p style="text-align: justify;">The Spring Security can be integrated with all the other parts os Spring as Spring Data and Spring MVC. More detail about the integration you can see <a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#integrations">here</a>. If you need to test methods based security you can find more information <a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#test">here</a></p>


<p style="text-align: justify;"></p>

<h2>Protection agains CSRF</h2>

<p style="text-align: justify;">Sprint give supports to protect your application agains the common exploits as <a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#csrf">CSRF</a> (Cross Site Request Forgery). You will see in one of my previous post about <a href="https://fabiana2611.github.io/java/vulnerability#csrf">vulnerability</a> that CSRF is a vulnerability which permits an attacker to force another logged-in user of the app to perform actions.</p>

<p style="text-align: justify;"><em>"This attack is possible because the HTTP request from the victim’s website and the request from the attacker’s website are exactly the same. To protect against CSRF attacks we need to ensure there is something in the request that the evil site is unable to provide so we can differentiate the two requests."</em><a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#csrf-protection">[1]</a></p>

Resources provided by Spring:
<ul>
  <li><a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#csrf-protection-stp">Synchronizer Token Patter</a>: The HTTP request have to have the session cookie and the CSRF token, a secure random generated value.</li>
  <li><a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#csrf-protection-ssa">Same Site Attribute</a>: <em>"A server can specify the SameSite attribute when setting a cookie to indicate that the cookie should not be sent when coming from external sites"</em>.</li>
</ul>

<p style="text-align: justify;">Other ponints of exploits protection are: <a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#headers">Security HTTP Response Headers</a> (defaults, cache, content type, etc), also give support to <a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/#http">HTTPS</a>.</p>


<h3>Conclusion</h3>

<p>All the play list of the videos shown in this post you will find <a href="https://www.youtube.com/watch?v=sm-8qfMWEV8&list=PLqq-6Pq4lTTYTEooakHchTGglSvkZAjnE">here</a>.</p>

<h3>References</h3>

<ul>
	<li><a href="https://docs.spring.io/spring-security/site/docs/current/reference/html5/">Spring Security Reference</a></li>
  <li><a href="https://blog.algaworks.com/spring-security/" >O que é Spring Security?</a></li>
  <li><a href="https://www.baeldung.com/spring-security-login" >Spring Security Form Login</a></li>
  <li><a href="https://spring.io/guides/topicals/spring-security-architecture" >Spring Security Architecture</a></li>
  <li><a href="https://www.linkedin.com/learning/spring-spring-security" >Linkeding Lerning - Spring Security Architecture</a></li>
</ul>
