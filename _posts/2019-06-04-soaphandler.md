---
layout: post
title:  "SOAP Handler"
date:   2019-06-04
categories: webservice
permalink: /:categories/soaphandler
---

<p style="text-align: justify;">The handler is an Interface from <strong><em><span style="color: #993366;">JAX-WS</span></em></strong> to intercept the <em>request</em> and <em>response</em> SOAP messages. Sometimes can be necessary to access SOAP message to additional process. The SOAP message Handler provides a mechanism for intercepting the SOAP message.</p>

The two types of handler supported by JAX-WS are:

<ol>
	<li><strong>SOAPHandler</strong>: can access the<em> soap messages</em> and <em>headers</em> (access the entire SOAP message)</li>
	<li><strong>LogicHandler</strong>: can access just the <em>payload</em> of the messages.</li>
</ol>

<blockquote>
<p style="text-align: justify;"><em>If SOAP handlers are used in conjunction with policies (security, WS-ReliableMessaging, MTOM, and so on), for inbound messages, the policy interceptors are executed before the user-defined message handlers. For outbound messages, this order is reversed. [<a href="https://docs.oracle.com/cd/E17904_01/web.1111/e13734/handlers.htm#WSADV161">1</a>]</em></p>
</blockquote>

<h2>Add SOAP Message Handlers</h2>

<em><strong>1. Design the handlers and handler chains</strong></em>
<p style="text-align: justify;">You should define the number of handlers you need and the sequence of the execution.</p>

<a href="https://examples.javacodegeeks.com/enterprise-java/jws/jax-ws-logging-with-handler-example/" ><img src="/img/soaphandler/handlerxml.png" width="590" height="112" /></a>
<p style="text-align: center;"><em><a href="https://examples.javacodegeeks.com/enterprise-java/jws/jax-ws-logging-with-handler-example/" >handler.xml</a></em></p>

<p style="text-align: justify;"><em><strong>2. For each handler in the handler chain, create a Java class that implements the SOAP message handler interface.</strong></em></p>

<ul>
	<li style="text-align: justify;">The <span style="color: #993366;">handleMessage</span> method is called to intercept a SOAP message request before and after it is processed by the back-end component.</li>
	<li style="text-align: justify;">The <span style="color: #993366;">MessageContext</span> properties allow the handlers in a handler chain to determine if a message is inbound or outbound and to share processing state.</li>
	<li style="text-align: justify;">Each context object extends <span style="color: #993366;">javax.xml.ws.handler.MessageContext</span>, which enables you to access a set of runtime properties of a SOAP message handler from the client application or Web service.
    <ul>
    	<li style="text-align: justify;">You can use the <span style="color: #993366;">MessageContext.MESSAGE_OUTBOUND_PROPERTY</span><span style="color: var(--color-text);"> property to determine if the message is an inbound or outbound request because it holds a Boolean value. </span><span style="color: var(--color-text);">The property would be true when accessed by a client-side handler or false when accessed by a server-side handler.</span></li>
    </ul>
  </li>
	<li>The method <span style="color: #993366;">handleFault</span> is executed in case of exception.</li>
</ul>

<p style="text-align: justify;">After the method is processed you can invoke the next handler from the handler-chain returning true, or block processing returning false.</p>

<a href="https://examples.javacodegeeks.com/enterprise-java/jws/jax-ws-logging-with-handler-example/" ><img src="/img/soaphandler/soapClass.png" width="552" height="564" /></a>

<p style="text-align: center;"><em><a href="https://examples.javacodegeeks.com/enterprise-java/jws/jax-ws-logging-with-handler-example/">Soap Class</a></em></p>

<strong><em>3. Update your JWS file, adding annotations to configure the SOAP message handlers.</em></strong>

| :------------- | :------------- |
| <a href="https://examples.javacodegeeks.com/enterprise-java/jws/jax-ws-logging-with-handler-example/" ><img src="/img/soaphandler/interface.png" width="900" height="100" /></a>       | <a href="https://examples.javacodegeeks.com/enterprise-java/jws/jax-ws-logging-with-handler-example/" ><img src="/img/soaphandler/class.png" width="916" height="150" /></a>       |

<ul>
	<li>Configure Handler Chains
<ul>
	<li style="text-align: justify;">You can use the @javax.jws.HandlerChain annotation to configure a handler chain for a Web service. Use the <em style="text-align: justify; color: var(--color-text);">file</em><span style="text-align: justify; color: var(--color-text);"> attribute to specify an external file that contains the configuration of the handler chain. The configuration includes the list of handlers in the chain, the order in which they execute, the initialization parameters, and so on.</span></li>
</ul>
</li>
	<li>Create the Handler Chain Configuration File</li>
	<li>Configure the Client-side SOAP Message Handlers
<ul>
	<li>Set a handler chain directly on the javax.xml.ws.BindingProvider,</li>
	<li>Implement a javax.xml.ws.handler.HandlerResolver on a Service instance</li>
	<li>Create a customization file that includes an element that contains a handler chain description.</li>
	<li>The schema for the element is the same for both handler chain files (on the server) and customization files.</li>
</ul>
</li>
</ul>

<h2>Steps to execute</h2>

When the WS is invoked to be executed on server-side[<a href="https://docs.oracle.com/cd/E17904_01/web.1111/e13734/handlers.htm#WSADV169">2</a>], the steps are:

<ul>
	<li style="text-align: justify;">Execute all the inbound methods for handlers in the handler chain. Any of them might change the SOAP message request.</li>
	<li style="text-align: justify;">As soon as the last handler executes, the back-end component that implements are executed.</li>
	<li style="text-align: justify;">After the back-end component has finished executing, the outbound methods are executed in the reverse order specified by the JWS annotation. Any of them might change the SOAP message response.</li>
	<li style="text-align: justify;">The final SOAP message response is returned to the client application as soon as the first handler in the handler chain executes.</li>
</ul>

<h2>Conclusion</h2>

<p style="text-align: justify;">If you are working on <a href="https://fabiana2611.github.io/webservice/soap">XML-Based Web Service</a>, SOAP, and need to do some process before the service, it is a great solution for you. This and the <a href="https://fabiana2611.github.io/java/logger/">Logger</a> are powerful tools for your system.</p>

<h2>References</h2>
<ul>
	<li>https://stackoverflow.com/questions/1945618/tracing-xml-request-responses-with-jax-ws</li>
	<li>https://docs.oracle.com/cd/E17904_01/web.1111/e13734/handlers.htm#WSADV160</li>
	<li>https://examples.javacodegeeks.com/enterprise-java/jws/jax-ws-logging-with-handler-example/</li>
	<li>http://java.boot.by/scdjws5-guide/ch09s05.html</li>
</ul>
