---
layout: post
title:  "Hexagonal Architecture - Hands On"
date:   2021-04-01
categories: foundation
permalink: /:categories/hexa-arch-handson
---

<p style="text-align: justify;">In my previous post about architectures, I gave an short view about the <a href="https://fabiana2611.github.io/foundation/architecture#Hexagonal">hexagonal architecture</a>. However, it's difficult to identify the base structure of this architecture, mainly if you work in a legacy code. This post is to show a suggestion of a skeleton to guide you to create the first version of your project.</p>

<p><center><img src="/img/architecture/hexagonal.png" width = "350" height = "150"/><br/>
<em> Sources: <a href="https://reflectoring.io/spring-hexagonal/">Tom Hombergs - reflectoring.io</a></em></center></p>

<p style="text-align: justify;">Bringing back some concepts, this architecture has three parts:</p>
<ul>
  <li><b>Left side:</b> communication with actors (GUI, API, etc)</li>
  <li><b>Core:</b> Isolated business logic</li>
  <li><b>Right Side:</b> communication with back service (database, external service, etc)</li>
</ul>  

<p>To ensure the isolation, the approach use more three concepts:</p>
<ul>
  <li><b>Adapters:</b> point to intermediate the communication between different technologies from front to the core.</li>
  <li><b>Port:</b> Interface to define the contract to access core, front and back service.</li>
  <li><b>usecase:</b> it should be implemented inner hexagonon and specify functions and events from application. The ports should be mapped to usecases.</li>
</ul>

<p>Now, with that in your mind let's go to the code.</p>

<h2>Skeleton</h2>

<p>Here is an option how it can be structured. The image show a structure with three main packages: backservice, core and frontend.</p>

<p><center><img src="/img/architecture/hexaskeleton.png" width = "550" height = "450"/></center></p>

<p style="text-align: justify;">The backservice has the implementation using specific characteristics of an technology. The repository implementation could be a communication with oracle or some external service, for example.<p>

<p style="text-align: justify;">The core package has all the business logic. The example has three functionalities: client, contract and investment. Inside each functionality there are more two packages: business and adapter. </p>

<p style="text-align: justify;">The business has the (1) domain, the main part of the business; (2) the port, with the interface to communicate with back service (the example has a communication with repository); and (3) the usecase, which communicate with frontend.</p>

<p style="text-align: justify;">Note that the interface to communicate with backservice is inside the core, but the implementation is out side the core. It is in the backservice package. It happens to keep the core Isolated.</p>

<p style="text-align: justify;">The same way, usecase has the interface to communicate with frontend, but has an implementation. The detail of technology should be inside the frontend.</p>

<p style="text-align: justify;">The adapter has the implementation to make the communication possible. The example implement an adapter to be the database mock. When the project start, maybe the database is not defined. It is an option to not let the development team waiting for implementation. In this case, you are using the mock and not the repository implementation.</p>

{% highlight ruby %}
public class AdapterInvestmentMockeImp implements IInvestmentRepository {

	private Map<Long, Investment> database = new HashMap<>();

    public AdapterInvestmentMockeImp() {
    		Client client = new Client("A", TypeClient.INDIVIDUAL);
		Investment investment = new Investment(new Contract("Vie", client));
		investment.setInvestValue(51d);

        database.put(10L, investment);

        Client client2 = new Client("C", TypeClient.COMPANY);
		Investment investment2 = new Investment(new Contract("Vie", client2));
		investment2.setInvestValue(151d);
        database.put(20L, investment2);
    }

	@Override
	public Investment consult(Long id) {
		return database.get(id);
	}

	@Override
	public Investment insert(Investment investment) {
		investment.setId(30L);
		database.put(30L, investment);
		return investment;
	}

}
{% endhighlight %}  


<p style="text-align: justify;">The frontend has a package with adapters and implementations. The adapter can be a way to simulate the calls to the system. The example show an adapter simulate an user interface or even integration tests. The hexagonal architecture has the origin in Agile mind and has a strong idea to use TDD. Then integration test is a weapon to start project when you don't have the interfaces to call the system.</p>

<h2>Run</h2>

<p style="text-align: justify;">So, let's start to run the example. If you are in the first step you are develop using integration test. The example show the integration test from investment. This test call the adapter from frontend to start the process.</p>

{% highlight ruby %}
public class InvestmentIntegrationTest {

	AdapterIntegrationTest adapter;

	@BeforeEach
	void setup() {
		adapter = new AdapterIntegrationTest();
	}

	@Test
	void findInvestment() {
		Investment result = adapter.findInvestment(10L);
		assertEquals(result.getContract().getClient().getType(), TypeClient.INDIVIDUAL);
		assertEquals(result.getContract().getLabel(), "Vie");
	}

	@Test
	void insertInvest() {
		Client client = new Client("New Client", TypeClient.INDIVIDUAL);
		Contract contract = new Contract("New Contract", client);
		Investment invest = new Investment(contract);
		invest.invest(100);

		Investment result = adapter.insertInvestment(invest);

		assertNotNull(result.getId());
	}

	@Test
	void invest() {
		Client client = new Client("New Client", TypeClient.INDIVIDUAL);
		Contract contract = new Contract("New Contract", client);
		Investment invest = new Investment(contract);
		invest.invest(100);

		adapter.invest(invest);

		assertEquals(invest.getInvestValue(), invest.getValue());
	}


}
{% endhighlight %}  

<p style="text-align: justify;">The adapter will do what is necessary to test the application. That will abstract technical issues to test the business.</p>

{% highlight ruby %}
public class AdapterIntegrationTest {


	InvestmentRestService service;
	IPortInvertmentService port;
	IInvestmentRepository repository;
	InvestmentService investmentService;

	public AdapterIntegrationTest() {
		repository = new AdapterInvestmentMockeImp();
		investmentService = new InvestmentService();
		port = new PortInvestmentServiceImp(repository, investmentService);
		service = new InvestmentRestService(port);
	}


	public Investment findInvestment(Long id) {
		return port.getInvestment(id);
	}

	public Investment insertInvestment(Investment investment) {
		return port.inset(investment);
	}

	public void invest(Investment invest) {
		investmentService.process(invest);
	}
}
{% endhighlight %}  

<p><em>PS: In a real app you will use framework to instantiate by @Inject. Here, I just want a simple code.</em></p>

<p>The sequence of calls happen as show bellow.</p>

<p><center><img src="/img/architecture/sequence.png" width = "800" height = "100"/></center></p>

<p style="text-align: justify;">The same idea happens if you start by AdapterUI. It will use the same sequence. The difference is how to start because will be specific by technology. By the example, the solutions are similar because the idea is to be simple.</p>

{% highlight ruby %}
public class AdapterUI {

	static InvestmentRestService service;
	static IPortInvertmentService port;
	static IInvestmentRepository repository;
	static InvestmentService investmentService;

	public void init() {
		repository = new AdapterInvestmentMockeImp();
		investmentService = new InvestmentService();
		port = new PortInvestmentServiceImp(repository, investmentService);
		service = new InvestmentRestService(port);
	}


	public Investment findInvestment(Long id) {
		return port.getInvestment(id);
	}

	public Investment insertInvestment(Investment investment) {
		return port.inset(investment);
	}

	public void invest(Investment invest) {
		investmentService.process(invest);
	}

	public static void main(String[] args) {

		AdapterUI adapter = new AdapterUI();
		adapter.init();

		Investment invest = adapter.getOne();

		investmentService.process(invest);
		Investment result = port.inset(invest);

		Investment investUpdated = port.getInvestment(result.getId());

		System.out.println("Process OK: " + !isNull(investUpdated));


	}

	private Investment getOne() {
		Client client = new Client("New Client", TypeClient.INDIVIDUAL);
		Contract contract = new Contract("New Contract", client);
		Investment invest = new Investment(contract);
		invest.invest(100);
		return invest;
	}

}
{% endhighlight %}  

<h2>Conclusion</h2>

<p style="text-align: justify;">This post suggests a structure to the hexagonal architecture but is not 100%  right. It will depend on each project. The post wants only to give an overview of how the skeleton can be created.</p>

<p>All the code you can see in my github <a href="https://github.com/fabiana2611/skeleton">here</a>.</p>

<h2>Other example</h2>

<p>
  <center>
    <iframe width="460" height="315" src="https://www.youtube.com/embed/UmdOjbyYOX0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
  </center>
</p>

<h2>References</h2>

<ul>
<li><a href="https://fabiana2611.github.io/foundation/architecture#Hexagonal">Hexagonal architecture - overview</a></li>
<li><a href="https://alistair.cockburn.us/hexagonal-architecture/">Hexagonal architecture</a></li>
<li><a href="https://reflectoring.io/spring-hexagonal/">Hexagonal Architecture with Java and Spring</a></li>
<li><a href="https://www.udemy.com/course/arquitetura-hexagonal-com-java-1/">Udemy - Arquitetura Hexagonal com Java - C1</a></li>
</ul>
