---
layout: post
title:  "Spring Batch"
date:   2019-06-19
categories: spring
permalink: /:categories/springbatch
---

<p style="text-align: justify;">Some application has processes that spend a lot of time to execute and can to compromise the performance of the app. Also can exist processes that need to execute in a specific time (<a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/5/html/deployment_guide/ch-autotasks">automated task</a> ). <a href="https://spring.io/projects/spring-batch">Spring Batch</a>, which is part of the <a href="https://fabiana2611.github.io/spring/springecosystem">Spring EcoSystem</a>, can give this support.</p>

<blockquote>
<p style="text-align: justify;"><em>A lightweight, comprehensive batch framework designed to enable the development of robust batch applications vital for the daily operations of enterprise systems.</em></p>
</blockquote>

<p style="text-align: justify;">The spring batch executes a set of jobs without user interaction. It's useful when is necessary, for example, process periodic events that can impact the performance of the application.  So, the process can be scheduled to be processed in moments where the access to the application is not so intense.</p>

<p style="text-align: justify;">Using this kind of framework is possible to process a huge number of transactions as a set and restart in the last point where the process can be interrupted. In other words, automatic retry after failure.</p>

<p style="text-align: justify;">The process is a job that can have one or more steps. The steps usually follow the sequence: read, process and write.</p>

<h2>Architecture</h2>
The <a href="https://docs.spring.io/spring-batch/3.0.x/reference/html/spring-batch-intro.html#springBatchArchitecture">architecture</a> of Spring Batch has three parts:

<ul>
	<li style="text-align: justify;"><strong>Application</strong>: contains all batch jobs and custom code written by developers</li>
	<li style="text-align: justify;"><strong>Core</strong>: contains the core runtime classes necessary to launch and control a batch job</li>
	<li style="text-align: justify;"><strong>infrastructure</strong>: contains common readers and writers, and services used both by application developers and the core framework itself</li>
</ul>

<center>
  <a href="https://docs.spring.io/spring-batch/3.0.x/reference/html/spring-batch-intro.html#springBatchArchitecture" ><img src="https://docs.spring.io/spring-batch/3.0.x/reference/html/images/spring-batch-layers.png" width="211" height="221" /></a>
</center>

<h2>Components</h2>

The mains <a href="https://www.tutorialspoint.com/spring_batch/spring_batch_architecture.htm">components</a> of Spring Batch are:

<ul>
	<li><strong>Job</strong>: it is the batch process to be executed. It can be divided into steps.</li>
	<li><strong>Step</strong>: independent part of a job with information used in the job. The step is composed of:
<ul>
	<li style="text-align: justify;"><em><span style="color: #993366;">ItemReader: </span></em>it reads data from a particular source</li>
	<li style="text-align: justify;"><em><span style="color: #993366;">ItemProcessor</span></em>: optional - it processes the data read - a process to each record. A <span style="color: #993366;">tasklet</span> can act as a processor when no reader and writer are given, processing only a single task</li>
	<li style="text-align: justify;"><em><span style="color: #993366;">ItemWriter</span></em>: it writes data to a particular destination.</li>
</ul>
</li>
	<li><strong>Job Launcher</strong>: interface to use parameters. <span style="color: #993366;">SampleJoblauncher</span> implements it.</li>
	<li><strong>Job Repository</strong>: It provides CRUD operations for the <em><span style="color: #993366;">JobLuncher</span></em>, <em><span style="color: #993366;">Job</span></em> and <em><span style="color: #993366;">STEP</span></em> implementations. If you don’t want to persist in the database, you can configure the <a href="https://docs.spring.io/spring-batch/4.0.x/reference/html/index-single.html#inMemoryRepository">in-memory</a> version of the jobRepository.</li>
	<li><strong>Job Instance</strong>: represents the <em>logical</em> <em>run</em> of a <em>job</em>.</li>
	<li><strong>Job Execution</strong>: represents the <em>execution</em> of a <em>job</em></li>
	<li><strong>Step Execution</strong>: represents the <em>execution</em> of a <em>step</em></li>
</ul>

<center>
  <a href="https://www.tutorialspoint.com/spring_batch/images/components.jpg" ><img  src="https://www.tutorialspoint.com/spring_batch/images/components.jpg" width="526" height="243" /></a>
</center>
<br/>

<h2>Example [CSV to XML]</h2>
<p style="text-align: justify;">For now, I'm going to show you an example and the first step is to add de dependencies into the <span style="color: #993366;">pom</span> file.</p>

{% highlight ruby %}
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-oxm</artifactId>
  <version>5.0.3.RELEASE</version>
</dependency>
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-jdbc</artifactId>
  <version>5.0.3.RELEASE</version>
</dependency>
<dependency>
  <groupId>org.springframework.batch</groupId>
  <artifactId>spring-batch-core</artifactId>
  <version>4.0.0.RELEASE</version>
</dependency>
{% endhighlight %}

<p style="text-align: justify;">After that, you need to create a configuration file (it can be more than one to organize your project) inside of the <em>resources</em> folder. Let's run an app that read from a CSV file to write into an XML file. Good different examples you can find <a href="https://www.tutorialspoint.com/spring_batch/spring_batch_application.htm">here</a>.</p>

{% highlight ruby %}
101, Joao, Learn Java, 06/05/2019
102, Maria F, Learn MySQL, 19/04/2019
103, Karlos Soares, Learn JavaFX, 06/07/2019
{% endhighlight %}

<p style="text-align: justify;">The configuration file will contain <span style="color: #993366;">job</span>, <span style="color: #993366;">step</span>, <span style="color: #993366;">beans</span> (readers and writers), <span style="color: #993366;">JobLauncher</span>, <span style="color: #993366;">JobRepository</span>, <span style="color: #993366;">Transaction Manager</span> and <span style="color: #993366;">Data Source</span>. It's possible to configure using XML file or Java class. The example is using XML config, but you can see an example using java in <a href="https://github.com/fabiana2611/spring-batch/blob/master/spring.batch/src/main/java/br/study/spring/batch/basic/SpringConfig.java">here</a>.</p>

<p style="text-align: justify;">The example below map a reader, a writer and a processor. The example read a csv, then the class used in the reader is the <span style="color: #993366;"><i>FlatFileItemReader </i></span>and a mapper to parse the file<i>. </i>for the writer in an XML is used <i><span style="color: #993366;">StaxEventItemWriter </span></i>and  a <a href="https://docs.spring.io/spring-ws/site/reference/html/oxm.html"><span class="emphasis"><em>marshaller</em></span></a> for serializing the object to XML<i>. </i>To see all possible classes you can see <i><a href="https://www.tutorialspoint.com/spring_batch/spring_batch_readers_writers_processors.htm">here</a>.</i></p>

{% highlight ruby %}
<batch:job id="jobTest">
   <batch:step id="step1">
     <batch:tasklet>
       <batch:chunk reader="cvsFileItemReader" writer="xmlItemWriter"
          processor="itemProcessor" commit-interval="10">
       </batch:chunk>
     </batch:tasklet>
   </batch:step>
</batch:job>

<bean id="cvsFileItemReader"
  class="org.springframework.batch.item.file.FlatFileItemReader">
  <property name="resource" value="classpath:datasource.csv" />
  <property name="lineMapper">
    <bean
       class="org.springframework.batch.item.file.mapping.DefaultLineMapper">
       <property name="lineTokenizer">
         <bean
            class="org.springframework.batch.item.file.transform.DelimitedLineTokenizer">
            <property name="names"
               value="id, author, title, submission_date" />
         </bean>
       </property>
       <property name="fieldSetMapper">
         <bean class="br.study.spring.batch.Mapper" />
       </property>
     </bean>
  </property>
</bean>

<bean id="itemProcessor" class="br.study.spring.batch.Processor" />

<bean id="xmlItemWriter"
  class="org.springframework.batch.item.xml.StaxEventItemWriter">
   <property name="resource" value="file:out/testBatch.xml" />
   <property name="marshaller" ref="reportMarshaller" />
   <property name="rootTagName" value="javaBean" />
</bean>

<bean id="reportMarshaller"
  class="org.springframework.oxm.jaxb.Jaxb2Marshaller">
  <property name="classesToBeBound">
    <list>
      <value>br.study.spring.batch.JavaBean</value>
    </list>
  </property>
</bean>

<bean id="jobRepository"
  class="org.springframework.batch.core.repository.support.MapJobRepositoryFactoryBean">
  <property name="transactionManager" ref="transactionManager" />
</bean>

<bean id="transactionManager"
  class="org.springframework.batch.support.transaction.ResourcelessTransactionManager" />

<bean id="jobLauncher"
  class="org.springframework.batch.core.launch.support.SimpleJobLauncher">
  <property name="jobRepository" ref="jobRepository" />
</bean>
{% endhighlight %}

After that, we need to create java classes:
<ul>
	<li><strong>Mapper Class</strong>: get data from the reader and set it to a Java Bean</li>
	<li><strong>Java Bean</strong>: represents the data used by batch</li>
	<li><strong>Tasklet/Processor</strong>: code to process the application (receive the data read, processes it, and return)</li>
	<li><strong>Launcher Class</strong>: run the application</li>
</ul>

| :------------- | :------------- |
| <img class="alignnone size-full wp-image-904" src="/img/spring/springBatch/javaBean.png" alt="javaBean" width="1026" height="520" />       |  <img src="/img/spring/springBatch/mapper.png" width="378" height="156" /> <img src="/img/spring/springBatch/launcher.png" width="358" height="174" /><img src="/img/spring/springBatch/processor.png" width="322" height="96" />       |

In case you are using a java class to config you just need to remove the lines in Launcher class related to xml file and to add the reference of the java class config. The complete example you can see <a href="https://github.com/fabiana2611/spring-batch/blob/master/spring.batch/src/main/java/br/study/spring/batch/basic/AppConfigJava.java">here</a>.

{% highlight ruby %}
AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
context.register(SpringConfig.class);
context.refresh();
{% endhighlight %}

The result of the execution is:

{% highlight ruby %}
<javaBeans>
   <javaBean id="101">
      <author>Joao</author>
      <submission_date>06/05/2019</submission_date>
      <title>Learn Java</title>
   </javaBean>
   <javaBean id="102">
      <author>Maria F</author>
      <submission_date>19/04/2019</submission_date>
      <title>Learn MySQL</title>
   </javaBean>
   <javaBean id="103">
      <author>Karlos Soares</author>
      <submission_date>06/07/2019</submission_date>
      <title>Learn JavaFX</title>
   </javaBean>
</javaBeans>
{% endhighlight %}

<h2>Example [XML to Database]</h2>

<p style="text-align: justify;">Now, to use a database to write the output you will need to change the itemWriter adding the SQL that will be used and to change the datasource reference. The example is based on <a href="https://www.tutorialspoint.com/spring_batch/spring_batch_xml_to_mysql.htm">tutorialspoint</a></p>

{% highlight ruby %}
# WRITER REFERENCE
<bean id="dbItemWriter"
	class="org.springframework.batch.item.database.JdbcBatchItemWriter">
	<property name="dataSource" ref="dataSource" />
	<property name="sql">
	  <value><![CDATA[
      insert into details.tutorials (tutorial_id, tutorial_author, tutorial_title, submission_date, tutorial_icon, tutorial_description)
      values (:tutorial_id, :tutorial_author, :tutorial_title, :submission_date, :tutorial_icon, :tutorial_description)]]></value>
	</property>

	<property name="itemSqlParameterSourceProvider">
		<bean class="org.springframework.batch.item.database.BeanPropertyItemSqlParameterSourceProvider" />
	</property>
</bean>

# DATASOURCE References

<bean id="dataSource"
	class="org.springframework.jdbc.datasource.DriverManagerDataSource">
	<property name="driverClassName" value="org.h2.Driver" />
	<property name="url" value="jdbc:h2:file:/tmp/jpadb" />
	<property name="username" value="sa" />
	<property name="password" value="" />
</bean>

<!-- create job-meta tables automatically -->
<jdbc:initialize-database data-source = "dataSource">   
   <jdbc:script location = "org/springframework/batch/core/schema-drop-h2.sql"/>   
      <jdbc:script location = "org/springframework/batch/core/schema-h2.sql"/>
</jdbc:initialize-database> 	
{% endhighlight %}

<h2>Run</h2>

<p style="text-align: justify;">The examples run the application using a class with the main method. Another way to execute the example batch job is by using <strong>CommandLineJobRunner</strong>, which is provided by Spring Batch.</p>

<img src="/img/spring/springBatch/main.png" width="900" height="250" />

The arguments receive the config XML and the job name. If you have some other config file you should insert on VM Arguments.

<img src="/img/spring/springBatch/arguments.png" width="900" height="250" />

The complete code you will see in <a href="https://github.com/fabiana2611/spring-batch">my github</a>.

<h2>Conclusion</h2>
Spring batch is a very important resource to run schedule process. There are mach more resource to use. This post show you just the first step. Now you have a world to explore.

Go deeply!!!

<h2>References</h2>
<ul>
	<li><a href="https://spring.io/projects/spring-batch">Spring Batch</a></li>
	<li><a href="https://docs.spring.io/spring-batch/4.0.x/reference/html/index-single.html#batchProcessingStrategy">DOC</a></li>
	<li><a href="https://spring.io/guides/gs/batch-processing/">Creating a Batch Service</a></li>
	<li><a href="https://www.baeldung.com/introduction-to-spring-batch">Introduction to Spring Batch</a></li>
	<li><a href="https://www.tutorialspoint.com/spring_batch/index.htm">SPring Batch Tutorial</a></li>
	<li><a href="https://howtodoinjava.com/spring-batch/java-config-multiple-steps/">HowToDoInJava - Example</a></li>
	<li><a href="https://www.toptal.com/spring/spring-batch-tutorial">Example</a></li>
	<li><a href="https://stackoverflow.com/questions/44238232/define-an-in-memory-jobrepository">jobRepository in-memory</a></li>
	<li><a href="https://keyholesoftware.com/2012/06/25/getting-started-with-spring-batch-part-two/">Getting Started</a></li>
	<li><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/5/html/deployment_guide/ch-autotasks">Deployment Guide</a></li>
</ul>
