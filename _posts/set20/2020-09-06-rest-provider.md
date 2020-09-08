---
layout: post
title:  "Rest - Providers and Interceptors"
date:   "2020-09-06"
category: "webservice"
permalink: /:categories/rest-provider
---

<p style="text-align: justify;">This post continues the studies about Rest Service already talked in my previous <a href="https://fabiana2611.github.io/webservice/rest">post</a>. </p>

<p style="text-align: justify;">The Rest is a stateless service which can access resources using methods (GET, POST, DELETE, PUT, etc) based on request/response communication.</p>

<p style="text-align: justify;">The Rest is a client/server architecture implemented by some API such as <a href="https://eclipse-ee4j.github.io/jersey/">Jersey</a> and <a href="https://docs.jboss.org/resteasy/docs/3.0.9.Final/userguide/html_single/index.html">RESTEasy</a>.</p>

<p style="text-align: justify;">Now, you can see an exemple of a controller that use an entity with two attributes.  </p>

{% highlight ruby %}
// File 1
public class Entity {                                           
  private String id;                                          
  private String name;                                           
  // Getters && Setters
}

//File 2
import java.net.URISyntaxException;

import javax.ws.rs.Consumes;
import javax.ws.rs.GET;
import javax.ws.rs.POST;
import javax.ws.rs.Path;
import javax.ws.rs.PathParam;
import javax.ws.rs.Produces;
import javax.ws.rs.core.MediaType;
import javax.ws.rs.core.Response;

/**
 * It is the controll
 * To access this functionality you can access by:
 * - 'http://localhost:8080/<your_app_name>/rest' + <path_method>
 * - ex: http://localhost:8080/MyRestDemoApp/rest/users/1
 * */
@Path("/rest")
public class MyRestServiceController {

  @GET
  @Path("/users/{id}")
  public Response getAllUsers(@PathParam (value="id") String id) {
    System.out.println("Start get with param and no return ... (no provider)");
    return Response.status(200).build();
  }

  @GET
  @Path("/users/")
  @Produces("text/html")
  public Response getAllUsers() {
    System.out.println("Start get without param and an txt/html return... (Provider: MessageBodyWriterInterceptor)");
    String result = "<h1>My Rest Demo</h1> Some text to not say Hello world :D !!";
    return Response.status(200).entity(result).build();
  }

  @GET
  @Path("/users2/")
  public Response getAllUsers2() {
    System.out.println("Start get with a entity return... (Providers: CustomerProviderMessageBodyWriter, CustomWriterInterceptor)");
    return Response.status(200).entity(new Entity()).build();
  }

  @POST
  @Path("/post/noreturn")
  @Consumes( MediaType.APPLICATION_JSON)
  public Response create(Entity entity) throws URISyntaxException {
    System.out.println("Start post with a entity param and no return... (Providers: CustomerProviderMessageBodyReader, CustomReaderInterceptor)");
    System.out.print("POST Create ientity: ");
    System.out.print("id: " + entity.getId());
    System.out.println(", Name: " + entity.getName());
    return Response.ok().build();
  }

  @POST
  @Path("/post/withreturn")
  @Consumes( MediaType.APPLICATION_JSON)
  public Response create2(Entity entity) throws URISyntaxException{
    System.out.println("Start post with a entity param ... (Providers: CustomerProviderMessageBodyReader, CustomReaderInterceptor)");
    System.out.println("Start post with a entity param and no return... (Providers: CustomerProviderMessageBodyWriter, CustomWriterInterceptor)");
    System.out.print("POST Create ientity: ");
    System.out.print("id: " + entity.getId());
    System.out.println(", Name: " + entity.getName());
    return Response.ok(new Entity()).build();
  }
}
{% endhighlight %}

<p style="text-align: justify;">This code is a simple example of a rest that use GET and POST methods. The code has methods to show different scenarios: with parameters, without return, with common return and with a specific return. Furthermore, you can see the (1) @Path annotation, relative the the URI of the resource, (2) @Produces, which indicate the MIME media type of the return sent back to the client, and (3) the @Consumes, relative the MIME media type that will be consumed by the service. If @Produces or @Consume are applied at the class level, all the methods will have this value by default. However, the methods have priority. If no annotation is used then the method can accept any media type.</p>

<p style="text-align: justify;">You can test your first Rest Service using RESTEasy here: <a href="https://howtodoinjava.com/resteasy/resteasy-jboss-7-hello-world-application/">using JBOSS</a> or <a href="https://howtodoinjava.com/resteasy/resteasy-tomcat-hello-world-application/">using Tomcat</a>.</p>

<p style="text-align: justify;">To access the methods you can use the Postman tool. Also, to test the GET method you can access directly by your browser: <em>http://localhost:8080/&lt;name_your_application&gt;/rest/users</em></p>

<p style="text-align: justify;">And the post you can create a class to run with the method:</p>

{% highlight ruby %}
public static void main(String[] args) throws IOException {
	  execute("noreturn");
    //execute("withreturn");
}

public static void execute(String path) throws IOException {
  final String POST_PARAMS = "{\n   \"id\": 101,\r\n  \"name\": \"Test Name\" \n}";
  System.out.println(POST_PARAMS);
	URL obj = new URL("http://localhost:8080/MyRESTDemoApp/rest/post/"+path);
	HttpURLConnection postConnection = (HttpURLConnection) obj.openConnection();
	postConnection.setRequestMethod("POST");
	postConnection.setRequestProperty("Content-Type", "application/json");
	postConnection.setDoOutput(true);
	OutputStream os = postConnection.getOutputStream();
	os.write(POST_PARAMS.getBytes());
	os.flush();
	os.close();
	int responseCode = postConnection.getResponseCode();
	System.out.println("POST Response Code :  " + responseCode);
	System.out.println("POST Response Message : " + postConnection.getResponseMessage());
}
{% endhighlight %}

<h2>Providers</h2>

<p style="text-align: justify;">The providers are resources to map the Http Request and Http Response. The providers are MessageBodyReader (MBR) and MessageBodyWriter (MBW). The MBR map the request to the method parameter. The MBW map the return value to the response body. </p>

<strong>MBR:</strong> <em>"conversion of HTTP request content to a Java type"</em> [<a href="https://abhishek-gupta.gitbook.io/rest-assured-with-jaxrs/jax-rs-providers-part-i#mbr">1</a>]

<strong>MBW:</strong> <em>"transforms a Java type to an on-wire format to be returned to the client"</em> [<a href="https://abhishek-gupta.gitbook.io/rest-assured-with-jaxrs/jax-rs-providers-part-i#mbw">2</a>]

{% highlight ruby %}
import java.io.IOException;
import java.io.InputStream;
import java.lang.annotation.Annotation;
import java.lang.reflect.Type;

import javax.ws.rs.WebApplicationException;
import javax.ws.rs.core.MediaType;
import javax.ws.rs.core.MultivaluedMap;
import javax.ws.rs.ext.MessageBodyReader;
import javax.ws.rs.ext.Provider;

@Provider
public class CustomerProviderMessageBodyReader  implements MessageBodyReader<Entity>{

  public boolean isReadable(Class<?> type, Type genericType,
    Annotation[] annotations, MediaType mediaType) {
    System.out.println("CustomerProviderMessageBodyReader isReadable... ");
    return true;
  }

  public Entity readFrom(Class type, Type genericType,
    Annotation[] annotations, MediaType mediaType, MultivaluedMap httpHeaders,
    InputStream entityStream) throws IOException, WebApplicationException {
    System.out.println("CustomerProviderMessageBodyReader readFrom...");
    Entity entity = new Entity();
    entity.setId("1");
    entity.setName("New Name");
    return entity;
  }
}
{% endhighlight %}

Now, let's see an example to MBW. It'll map the response.

{% highlight ruby %}
import java.io.IOException;
import java.io.OutputStream;
import java.lang.annotation.Annotation;
import java.lang.reflect.Type;

import javax.ws.rs.WebApplicationException;
import javax.ws.rs.core.MediaType;
import javax.ws.rs.core.MultivaluedMap;
import javax.ws.rs.ext.MessageBodyWriter;
import javax.ws.rs.ext.Provider;

@Provider
public class CustomerProviderMessageBodyWriter implements MessageBodyWriter<Entity>{

  public boolean isWriteable(Class<?> type, Type genericType,
    Annotation[] annotations, MediaType mediaType) {
    System.out.println("CustomerProviderMessageBodyWriter isWriteable ...");
    return true;
  }

  public long getSize(Entity t, Class<?> type, Type genericType,
    Annotation[] annotations, MediaType mediaType) {
    System.out.println("CustomerProviderMessageBodyWriter GetSize...");
    return 0;
  }

  public void writeTo(Entity t, Class<?> type, Type genericType,
    Annotation[] annotations, MediaType mediaType, MultivaluedMap<String, Object> httpHeaders, OutputStream entityStream) throws IOException, WebApplicationException {
      System.out.println("CustomerProviderMessageBodyWriter writeTo ...");
    }
}

{% endhighlight %}


<h2>Interceptors</h2>

<em> It... [<a href="https://abhishek-gupta.gitbook.io/rest-assured-with-jaxrs/jax-rs-providers-part-ii">3</a>]</em>
<ul>
  <li><em>"works in tandem with (intercept) Message Body Readers and Writers"</em></li>
  <li><em>"used to manipulate HTTP message payloads"</em></li>
</ul>  

<p style="text-align: justify;">Let's see below an ReaderInterceptor. Same as MessageBodyReader, this provider is called to process before the method start.</p>

{% highlight ruby %}}
import org.jboss.resteasy.annotations.interception.ClientInterceptor;
import org.jboss.resteasy.annotations.interception.ServerInterceptor;
import org.jboss.resteasy.spi.interception.MessageBodyReaderContext;
import org.jboss.resteasy.spi.interception.MessageBodyReaderInterceptor;

@Provider
@ServerInterceptor
@ClientInterceptor
public class CustomReaderInterceptor implements MessageBodyReaderInterceptor{

  public Object read(MessageBodyReaderContext context) throws IOException, WebApplicationException {
    System.out.println("CustomReaderInterceptor read...");
    Entity newEntity = new Entity();
    newEntity.setId("newId");
    newEntity.setName("NewName");
    return newEntity;
  }
}
{% endhighlight %}

<p style="text-align: justify;">And now, a WriterInterceptor. As well as MessageBodyWriter, this provider is called to process the response, after the method finish.</p>

{% highlight ruby%}
import java.io.IOException;

import javax.ws.rs.WebApplicationException;
import javax.ws.rs.ext.Provider;

import org.jboss.resteasy.annotations.interception.ClientInterceptor;
import org.jboss.resteasy.annotations.interception.ServerInterceptor;
import org.jboss.resteasy.spi.interception.MessageBodyWriterContext;
import org.jboss.resteasy.spi.interception.MessageBodyWriterInterceptor;

@Provider
@ServerInterceptor
@ClientInterceptor
public class CustomWriterInterceptor implements MessageBodyWriterInterceptor{

  public void write(MessageBodyWriterContext context) throws IOException, WebApplicationException{
    System.out.println("CustomWriterInterceptor writer... (method return an entity)");
    context.getHeaders().add("My-Header", "custom");
    context.proceed();
  }
}

{% endhighlight %}

<h2>The console after run ...</h2>

<h4>GET</h4>
<p style="text-align: justify;">After run the first GET method, no provider is called. It was not necessary. It is a method with a simple parameter and no return inside the response.</p>

{% highlight ruby %}
Start get with param and no return ... (no provider)
{% endhighlight %}

<p style="text-align: justify;">The second GET method has a simple return, already known by rest API (text/html). Then, only one provider is called.</p>

{% highlight ruby %}
Start GET without param and an txt/html return... (Provider: MessageBodyWriterInterceptor)
CustomWriterInterceptor writer... (method return an entity)
{% endhighlight %}

<p style="text-align: justify;">The third GET has a return inside the response of a specific entity. It needs to be translate. Because of that, now is called the writers.</p>

{% highlight ruby %}
Start get with a entity return... (Providers: CustomerProviderMessageBodyWriter, CustomWriterInterceptor)
CustomerProviderMessageBodyWriter isWriteable ...
CustomerProviderMessageBodyWriter isWriteable ...
CustomerProviderMessageBodyWriter GetSize...
CustomWriterInterceptor writer... (method return an entity)
CustomerProviderMessageBodyWriter writeTo ...
{% endhighlight %}

<h4>POST</h4>

<p style="text-align: justify;">On the first post method, a specific parameter is given to the method and no return to the response. Because of that, only reader providers are needed.</p>

{% highlight ruby %}
CustomerProviderMessageBodyReader isReadable...
CustomReaderInterceptor read...
Start post with a entity param and no return... (Providers: CustomerProviderMessageBodyReader, CustomReaderInterceptor)
POST Create ientity: id: newId, Name: NewName
{% endhighlight %}

<p style="text-align: justify;">And the last scenario the method receive an entity as parameter and return an entity. So, readers and writers are called.</p>

{% highlight ruby %}
CustomerProviderMessageBodyReader isReadable...
CustomReaderInterceptor read...
Start post with a entity param ... (Providers: CustomerProviderMessageBodyReader, CustomReaderInterceptor)
Start post with a entity param and no return... (Providers: CustomerProviderMessageBodyWriter, CustomWriterInterceptor)
POST Create ientity: id: newId, Name: NewName
CustomerProviderMessageBodyWriter isWriteable ...
CustomerProviderMessageBodyWriter isWriteable ...
CustomerProviderMessageBodyWriter GetSize...
CustomWriterInterceptor writer... (method return an entity)
CustomerProviderMessageBodyWriter writeTo ...
{% endhighlight %}

<h2>Pipeline</h2>

<p style="text-align: justify;">For all the process, since start the method to return the result, you can apply filters and interceptors. The figure below show that idea. More detail you can see <a href="https://abhishek-gupta.gitbook.io/rest-assured-with-jaxrs/jax-rs-for-power-users-part-i">here.</a></p>

<center>
<img src="/img/rest/pipeline.png" high="400" width="400">
</center>

<p style="text-align: justify;"></p>

<p style="text-align: justify;"></p>

<h2>References</h2>

<ul>
  <li>
  <a href="https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/6.4/html/development_guide/sect-resteasy_interceptors">RESTEASY INTERCEPTORS</a>
  </li>
  <li>
  <a href="https://abhishek-gupta.gitbook.io/rest-assured-with-jaxrs/">REST assured with JAX-RS</a>
  </li>
  <li>
  <a href="https://docs.oracle.com/cd/E19798-01/821-1841/6nmq2cp1v/index.html">Building RESTful Web Services with JAX-RS</a>
  </li>
  <li>
  <a href="https://howtodoinjava.com/resteasy/resteasy-tomcat-hello-world-application/">RESTEasy example tutorial for beginners</a>
  </li>
  <li>
  <a href="https://www.baeldung.com/resteasy-tutorial">A Guide to RESTEasy</a>
  </li>
  <li>
  <a href="https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/6.4/html/development_guide/sect-resteasy_interceptors">RESTEASY CONFIGURATION</a>
  </li>
</ul>

<strong>Code References:<strong>
<ul>
<li><a href="https://abhishek-gupta.gitbook.io/rest-assured-with-jaxrs/jax-rs-providers-part-i">adhishek-gupta-gitbook - providers</a></li>
<li><a href="https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/6.4/html/development_guide/sect-resteasy_interceptors">redhat - interceptors</a></li>
<li><a href="https://dzone.com/articles/how-to-implement-get-and-post-request-through-simp">dzone - get and post rest</a></li>
<li><a href="https://howtodoinjava.com/resteasy/resteasy-tomcat-hello-world-application/">howtodoinjava - RESTEasy example tutorial for beginners</a></li>
</ul>
