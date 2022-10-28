---
layout: post
title:  "Energy Efficiency attention points for development"
date:   2022-10-28
categories: beyond
permalink: /:categories/patterns-energy-and-measure
---

<p style="text-align: justify;">In my first post about GreenIT I started an overview about the theme. There are many areas to explore. For now I'm going to explore the environment near from the developers.</p>

<p style="text-align: justify;">Some solutions such as <a href="https://www.thoughtworks.com/what-we-do/enterprise-modernization-platforms-cloud/green-cloud">Carbon footprint</a> and <a href="https://aws.amazon.com/es/aws-cost-management/aws-customer-carbon-footprint-tool/">AWS Customer Carbon Footprint </a> are solutions that run in the cloud after the commits. Considering that the CI/CD process has energy consumption, the developers can act before this happen and be more effective.</p>

<p style="text-align: justify;">Unfortunately, most of the work that involves this scope is in academic articles. Also, some solutions that look like good solutions were not found on the market or in a shared code to do some testing (at least at the time of this writing), but that doesn't decrease the importance of the works.</p>

<p style="text-align: justify;">This post is a kind of survey around my personal point of interest: guidance/solutions to give support to developers while is coding.</p>

<br />
<h3>Survey</h3>

<p style="text-align: justify;">For this post, I've focused more on Design Patterns (DP) and tried to understand the impact of the choice on energy efficiency. DP are solutions to help the developers in terms of, for instance, readability and maintainability. It is not so simple in terms of performance and energy consumption.</p>

<p style="text-align: justify;">There are many works analyzing them and compare with anti-patterns solutions. The general results is that use the patterns is better than alternative solutions in most cases. However, some DP can negatively impact the energy consumption. </p>

<ul>
  <li>[1]: compared many of DP and detect that <b>Observer, Mediator and Decorator</b> consume more energy comparing the others. The authors propose to optimize the DP at the compiler considering their dynamic voltage scaling. Focus on the compiler, the code will no be changed.</li>
  <li> [2] checked the <b>Facade, Prototype, Template Method, Flyweight and Decorator</b>. It identify that the three first patterns have negligible impact on performance and energy efficiency, the Flyweight improve both performance and energy efficiency, and Decorator get worse both criteria.</li>
  <li>[3]: checked <b>Singleton, Facade, Abstract Factory and Observer</b>. It identify that Singleton have increased the energy consumption. The authors suppose that happen because of <em>"in the Singleton pattern an object remains present in memory during the lifecycle of an application. This is opposed to lazy instantiation where an object is created on demand."</em>. For the others patterns they identify a reduction of the energy consumption. Their supposition to Abstract factory is <em>because rather than passing object references among classes, now we have a single place to get the required objects".</em> For Observer, they believe the reason to the improvement <em>is due to the nature of the changes made for the implementation of pattern.</em>. For Facade, the positive result seems to be in the fact <em>it becomes the center point of interaction. This means a fewer number of temporary objects are created that are required for pass by value.</em></li>
  <li>[4]: checked <b>Facade, Observer, Template Method, Prototype and Decorator</b>. The first three didn't show  no difference as the last two show a large difference in time and energy. The author justify the difference by <em>large amount of objects instantiations and method calls of the pattern-based system.</em></li>
  <li>[5]: provides an overview for each phase of the SDLC. The highlights I can give you are: (1) <u><a href="https://www.researchgate.net/publication/320436353_Energy_efficiency_across_programming_languages_how_do_energy_time_and_memory_relate">programming language</a></u>, raised up in the <a href="">last post</a>, where C is the best result, Java and TypeScript in the middle position (but Java being in a better position) and Phyton in the end of the line; (2) <u>Parallel Programming</u> that can improve the performance and energy efficiency if in the right configuration; (3) <u>data structure</u>, that can be impacted by the number of objects or if is using thread-safe or not, and even about the use of primitive data types, which can be more energy-inefficient comparing with objects in most of the cases while consuming less memory than objects; (4) <u>Coding Practices</u>, like the use of <em>For loop</em> with length (variable as the loop termination condition), or accessing class variables without using getter/setter functions, or the practice of static invocation (avoids
  the lookup overhead for calling methods through an existing object), or  put the application to sleep, or select the right API, or reducing the expensive database operations, save energy; (5) <u>refactoring techniques</u>, that may increase or decrease the energy consumption. The technique <em>Extend Local Variables</em> always reduces energy consumption as the others or don't make difference or the difference is very low (<em>Refactoring Techniques: Dead Local Variable, Non Short Circuit, Parameter By Value, Repeated Conditionals, Self Assignment Variable, Convert Local Variable to Field, Extract Local Variable, Extract Method, Introduce Indirection, In line Method, Introduce Parameter Object, Replace Method with Method Object and Encapsulate Collection). However, to work mention techniques applied to Android that save energy (Loop Unrolling, Loop Unswitching, Method Inline). This work also discuss about some tools that I list them in the next section.</li>
  <li>[6]: compared the <b>State, Strategy and the Template Method</b> with alternative solutions and the results show that the use of the DP improve the efficiency.</li>
  <li>[7]: it analyze <b>Abstract Factory, Builder, Factory method, Prototype, Singleton, Bridge, Composite, Decorator, Flyweight, Proxy, Command, Mediator Observer, Strategy, and Visitor</b> and conclude that <em>the use of DP can increased or decreased the energy consumption, there are no relations between the categories and it is not possible to precisely estimate the impact of design patterns on energy consumption
  when only considering artifacts on design-level</em>.</li>
</ul>

<br />
<h3>Tools</h3>

<p style="text-align: justify;">Here I split the tools I found into two categories: academic and testable. It is an informal category that I defined based on my experience to try to apply or just test them.  The tools classified as academic are the tools that I found only the article but not the code or even if the code seems deprecated (long time without commits). Most part of those tools were mention in [5].</p>

<h4>Academic:</h4>
<ul>
  <li><b>GREEN</b> [8][9][5]: It is a framework focused on Computations and loop termination that try to optimize expensive loops and functions considering user-defined Quality of Service (QoS) requirements. It has as output a new version of the program.</li>
  <li><b>Chisel</b> [10][11][5]: Focused on Computational kernel operations : <em>acts in an automated manner by selecting approximate kernel operations that result in energy, reliability, and accuracy optimizations. Chisel is utilizing the approximate memory of its running platform to increase energy savings by sacrificing some of its quality output.</em></li>
  <li><b>Parrot</b> [12][5]: Focused on Optimizes regions of imperative code. <em>It is a neural network model that identifies imperative code regions and offloads them to neural processing unit, instead of CPU, to increase energy and run-time performance.</em></li>
  <li><b>Axilog</b> [13][14][15][5]: Focused on Source code parts. <em>It is a Verilog extension composing brief and high-level annotations for full control and governance of approximate hardware.</em></li>
  <li><b>EnerJ</b> [16][17][18][19][20][5]: Computations, Data Storage, and Algorithmica: <em> By declaring variables and objects as approximate,
  EnerJ maps them to approximate memory and generates low-cost energy code by using approximate operations and algorithms</em></li>
  <li><b>GreenAdvisor</b> [22][23][5]: (Android) <em>is a profiler system calls that predicts behavior, run-time performance, and energy-related modifications of an application. To predict energy-related changes, GreenAdvisor compares the number of system calls on a current version of a software and its previous one. GreenAdvisor compares the energy consumption of different versions of a product and points out the system calls that caused the change</em>.</li>
  <li>eLens [24][25][26][5]: <em>estimates energy consumption via program analysis and per-instruction power modeling. The authors use program analysis to obtain execution-related information such as bytecode or API calls from various smart-phone components (e.g., CPU, RAM, GPS, 3G). eLens provides energy measurements at various levels of granularity: application, method, class, path, and source code lines. </em></li>
  <li>Jalen [27][28][29][5]: <em>Java-based agent for software energy monitoring at the source code level. Jalen measures selected methods and classes. Additionally, it provides measurements on explicit hardware components (e.g., CPU and HDD) and estimates the energy consumption of software by analyzing executed Java instructions.</em></li>
  <li>PEEK [30][31][32][33][34][5]: <em>PEEK fully automates energy measurement tasks and suggests program-code improvements at development time by providing automatically generated energy optimization hints. Our approach is based on a combined software and hardware infrastructure to automatically determine energy demand of program code and pinpoint energy faults, thereby integrating seamlessly into existing software development environments. PEEK’s energy-associated hints are related to power management mechanisms (e.g.,  sleep state, idle state, program-code logic, libraries, and compiler). PEEK analyzes source code at function granularity</em></li>
  <li>SEEDS [35][36][37][5]: <em>a decision support framework that create instances of an application under development using different queue data structures, to find the most energy efficient ones. SEEDS’ suggestions are limited to Java Collection Libraries (JCL), algorithms, or refactoring parts of the source code. SEEDS offers to developers the possibility to set a code block range for analysis. </em></li>
</ul>

<h4>Testable:</h4>
<ul>
  <li>PowerAPI [38][39][5]: <em>real-time monitor in process-level energy consumption. Jalen has PowerAPI as the core component for extracting energy measurements.</em></li>
  <li>Running Average Power Limit (RAPL/jRAPL) [40][41][42][5]: monitors and controls energy consumption via performance counters by exposing kernel subsystems, hardware devices, and device driver information. jRAPL use Java. Some tools use this RAPL as a core to measure the energy.
  <li>top[43][44]: it is a command line tool that list all running processes on the system doing a periodic measurements. Similar to <a href="https://support.apple.com/en-au/guide/activity-monitor/welcome/mac">Activity Monitor</a>, a tool with graphical interface to MACOS, you can see data as CPU, memory and power.</li>
  <li>ioreg [45][46]: <em>The I/O Registry is a dynamic database that describes a collection of “live” objects (nubs or drivers) and tracks the provider-client relationships between them.</em> With this native tool is possible collect information about energy consumption.</li>
  <li>EcoAndroid [47]: IntelliJ plugin for android aplication. <em>EcoAndroid suggests automated refactorings for reducing the energy consumption of Java Android applications. It is based on the idea of <a href="https://tqrg.github.io/energy-patterns/#/">energy pattern</a> (Dynamic Retry Delay, Push Over Poll, Reduce Size, Cache, Avoid Graphics Animations)</em></li>
</ul>


<br />
<h3>Hands-On</h3>

<p style="text-align: justify;">A good starting point is to explore the project <a href="https://sites.google.com/view/energy-efficiency-languages">Energy Efficiency in Programming Languages</a> done by <a href="https://greenlab.di.uminho.pt/">Green Software Lab</a>. It is a good project to compare the energy efficiency between programming languagesthat. The <a href="https://github.com/greensoftwarelab/Energy-Languages">code</a> is available and give the possibilitiy to test and compare 28 different languages in different scenarios.  It uses the <a href="https://www.intel.com/content/www/us/en/developer/articles/technical/software-security-guidance/advisory-guidance/running-average-power-limit-energy-reporting.html?wapkw=RAPL">Intel’s Running Average Power Limit (RAPL) tool as the core to estimate the energy consumption.</p>

<p style="text-align: justify;">If you have an Intel you just need to do a simple configuration and it's ready to test locally. But if you are using a MAC like me you need other steps to do.</p>

<p style="text-align: justify;">This <a href="https://blog.mozilla.org/nnethercote/2015/08/26/what-does-the-os-x-activity-monitors-energy-impact-actually-measure/">article</a> has a good discussion about how measure the energy in MAC. The Activity Monitor tool is available in MACOS. It is a graphical tool where you can see the values of the PC. A similar tool is the <a href="https://gridpane.com/kb/how-to-use-the-top-command-to-monitor-system-processes-and-resource-usage/">top</a> that you can have similar values but using command line.</p>

<p style="text-align: justify;">A second alternative or complementary is the <a href="https://developer.apple.com/library/archive/documentation/DeviceDrivers/Conceptual/IOKitFundamentals/TheRegistry/TheRegistry.html">ioreg</a> (I/O Registry). This <a hreh="https://www.rdegges.com/2022/how-to-calculate-the-energy-consumption-of-a-mac/">post</a> has a good discussion about how to measure the energy consumption using ioreg in MAC.</p>.

<p style="text-align: justify;">The commands are calls from the application. However, it's using a <a href="//https://github.com/rogerbf/ioreg">lib of ioreg</a>. It's necessary install it.</p>

<pre>
$npm install ioreg
</preb>

<p style="text-align: justify;">Here I'm using ioreg and top but it doesn't mean they are dependents. It's only a test to check the outcomes.</p>

<h4>Doing a simple test</h4>

<p style="text-align: justify;">For a simple test, a portion of the the project "Energy Efficiency in Programming Languages" was extracted. The goal is not test the language but see how to measure the energy considering a MACOS. So, for this test was used ontly four Benchmark from TypeScript.</p>

<p style="text-align: justify;">For that, I extracted the code for another project using NestJS, and my calls are done by a controller. Furthermore, I do my tests using <b>top</b> and <b>ioreg</b>. As I said before, my idea is just to run the tools to catch the values and have my first experience doing that activity. Even so, the logic is the same: have a starting point to make it step 0 and start to count the values and have a step where the count stops to be done and exposes the values.</p>

<p style="text-align: justify;">Here is the core to catch the values. It's not the best solution but it works to the goal. The complete code you can see <a href="https://github.com/fabiana2611/energy-consumption-poc/tree/master/energy-measure-js">here</a>.</p>

<p><center>
  <img src="/img/green/measuremethod.png" />
</center></p>

<h4>Result</h4>

<p style="text-align: justify;">The values get in the end of the process was the average from top and one execution of the ioreg. The image is regarding the execution of the binarytrees but you can do the same with the others benchmarcks implemented.</p>

<p><center>
  <img src="/img/green/result_poc.png" />
</center></p>

<h3>Conclusion</h3>

<p style="text-align: justify;">There are some trade-offs when we are coding in terms of energy efficiency. The good parts is in terms of Design Patterns we can use it without too many restrictions. Only pay attention in some of them like Decorator, observer and mediator.</p>

<p style="text-align: justify;">As a good practices, some point can help to improve the efficiency as the Parallel programming. It's not a silver bullet but can help in some scenarios.</p>

<p style="text-align: justify;">How to measure is one of the trick points because it influenced by the CPU and OS.</p>

<p style="text-align: justify;">This post tried to do an overview about the theme and some ideas how to check the energy consumption. Next post let's put everything together.</p>


<br />
<h3>Reference</h3>

<ul>
  <li>[1] <a href="https://homepages.inf.ed.ac.uk/arajan/My-Pubs/ICSE15.pdf">A. Noureddine and A. Rajan. 2015. Optimising Energy Consumption of Design Patterns. In 2015 IEEE/ACM 37th IEEE International Conference on Software Engineering (ICSE), Vol. 2. 623–626. DOI:http://dx.doi.org/10.1109/ICSE.2015.208</a></li>
  <li>[2] Maleki, Sepideh et al. “Understanding the Impact of Object Oriented Programming and Design Patterns on Energy Efficiency.” 2017 Eighth International Green and Sustainable Computing Conference (IGSC) (2017): n. pag. Web.</li>
  <li>[3] <a href="https://sciendo.com/pdf/10.2478/acss-2021-0001">Evaluating the Impact of Design Pattern Usage on Energy Consumption of Applications for Mobile Platform</a></li>
  <li>[4] <a href="https://fb-swt.gi.de/fileadmin/FB/SWT/Softwaretechnik-Trends/Verzeichnis/Band_33_Heft_2/01-BunseStiemer.pdf">On the Energy Consumption of Design Patterns</a></li>
  <li>[5] <a href="https://stefanos1316.github.io/my_curriculum_vitae/GRS19.pdf">Software Development Life Cycle for Energy-Efficiency: Techniques and Tools</a></li>
  <li>[6] <a href="https://fse.studenttheses.ub.rug.nl/13676/1/Thesis_R_Alders_v1.0.0.pdf">Energy Efficient Design Patterns</a></li>
  <li>[7] Cagri Sahin, Furkan Cayci, Irene Lizeth Manotas Guti ́errez, James Clause, Fouad Kiamilev, Lori Pollock, and Kristina Winbladh. Initial explorations on design pattern energy usage. In Green and Sustainable Software (GREENS), 2012 First International Workshop on, pages 55–61. IEEE, 2012.</li>
  <li>[8] <a href="https://slideplayer.com/slide/4843991/">GREEN - presentation</a></li>
  <li>[9] <a href="https://www.microsoft.com/en-us/research/wp-content/uploads/2016/12/green.pdf">Green: A Framework for Supporting Energy-Conscious
Programming using Controlled Approximation</a></li>
  <li>[10] Sasa Misailovic, Michael Carbin, Sara Achour, Zichao Qi, and Martin C. Rinard. 2014. Chisel: Reliability and Accuracy-aware Optimization of Approximate Computational Kernels. In Proceedings of the 2014 ACM International Conference on Object Oriented Programming Systems Languages & Applications (OOPSLA ’14). ACM, New York, NY, USA, 309–328.</li>
  <li>[11] <a href="https://people.csail.mit.edu/rinard/paper/oopsla14.pdf">Chisel: Reliability- and Accuracy-Aware Optimization of Approximate Computational Kernels</a></li>
  <li>[12] H. Esmaeilzadeh, A. Sampson, L. Ceze, and D. Burger. 2012. Neural Acceleration for General-Purpose Approximate Programs. In 2012 45th Annual IEEE/ACM International Symposium on Microarchitecture. 449–460. DOI:http://dx.doi.org/10.1109/MICRO.2012.48</li>
  <li>[13] A. Yazdanbakhsh, D. Mahajan, B. Thwaites, J. Park, A. Nagendrakumar, S. Sethuraman, K. Ramkrishnan, N. Ravindran, R. Jariwala, A. Rahimi, H. Esmaeilzadeh, and K. Bazargan. 2015. Axilog: Language support for approximate hardware design. In 2015 Design, Automation Test in Europe Conference Exhibition (DATE). 812–817. DOI:http://dx.doi.org/10.7873/DATE.2015.0513</li>
  <li>[14] <a href="https://cseweb.ucsd.edu/~hadi/doc/paper/2015-date-axilog.pdf">Axilog: Language Support for Approximate Hardware Design</a></li>
  <li>[15] <a href="https://slideplayer.com/slide/9008960/">Axilog - presentation</a></li>
  <li>[16] Adrian Sampson, Werner Dietl, Emily Fortuna, Danushen Gnanapragasam, Luis Ceze, and Dan Grossman. 2011. EnerJ: Approximate Data Types for Safe and General Low-power Computation. In Proceedings of the 32Nd ACM SIGPLAN Conference on Programming Language Design and Implementation (PLDI ’11). ACM, New York, NY, USA, 164–174. DOI:http://dx.doi.org/10.1145/1993498.1993518</li>
  <li>[17] <a href="https://homes.cs.washington.edu/~luisceze/publications/Enerj-pldi2011.pdf">EnerJ: Approximate Data Types for Safe and General Low-Power Computation</a></li>
  <li>[18] <a href="https://github.com/sampsyo/enerj">EnerJ - Github</a></li>
  <li>[19] <a href="https://github.com/pminervini/EnerJ">EnerJ - Github 2</a></li>
  <li>[20] <a href="https://github.com/sjalander/approximate-enerj">EnerJ - Github 3</a></li>
  <li>[21] K. Aggarwal, A. Hindle, and E. Stroulia. 2015. GreenAdvisor: A tool for analyzing the impact of software evolution on energy consumption. In 2015 IEEE International Conference on Software Maintenance and Evolution (ICSME). 311–320. DOI:http://dx.doi.org/10.1109/ICSM.2015.7332477<li>
  <li>[22] <a href="https://softwareprocess.es/homepage/papers/2015-karan2015icsme2015gatfatioseoec/">GreenAdvisor: A Tool for Analyzing the Impact of Software Evolution on Energy Consumption</a></li>
  <li>[23] <a href="https://github.com/kaggarwal/GreenAdvisor">GreenAdvisor - Github</a></li>
  <li>[24] S. Hao, D. Li, W. G. J. Halfond, and R. Govindan. 2013. Estimating mobile application energy consumption using program analysis. In 2013 35th International Conference on Software Engineering (ICSE). 92–101. DOI:http://dx.doi.org/10.1109/ICSE.2013.6606555</li>
  <li>[25] <a href="https://viterbi-web.usc.edu/~halfond/papers/hao13icse.pdf">Estimating mobile application energy consumption using program analysis</a></li>
  <li>[26] <a href="https://pdfs.semanticscholar.org/30ff/c7c6aab3bbd1f5af69fb97a7d151509d0a52.pdf">eLens - Presentation</a></li>
  <li>[27] A. Noureddine, A. Bourdon, R. Rouvoy, and L. Seinturier. 2012b. Runtime monitoring of software energy hotspots. In 2012 Proceedings of the 27th IEEE/ACM International Conference on Automated Software Engineering (ASE). 160–169.DOI:http://dx.doi.org/10.1145/2351676.2351699</li>
  <li>[28] <a href="https://github.com/adelnoureddine/jalen">Jalen - Github</a></li>
  <li>[29] <a href="https://www.noureddine.org/research/jalen">Jalen - Homepage</a></li>
  <li>[30] Timo Honig, Heiko Janker, Christopher Eibel, Oliver Mihelic, and R  ̈udiger Kapitza. 2014. Proactive Energy-Aware Programming with PEEK.</li>
  <li>[31] <a href="https://www4.cs.fau.de/Publications/2014/hoenig_14_trios.pdf">Proactive Energy-Aware Programming with PEEK</a></li>
  <li>[32] <a href="https://www.usenix.org/conference/trios14/technical-sessions/presentation/hoenig">PEEK page</a></li>
  <li>[33] <a href="https://opus4.kobv.de/opus4-fau/frontdoor/index/index/docId/8992">PEEK - dissertation</a></li>
  <li>[34] <a href="https://www4.cs.fau.de/Research/SEEP/">SEEP - homepage</a></li>
  <li>[35] Irene Manotas, Lori Pollock, and James Clause. 2014. SEEDS: A Software Engineer’s Energy-optimization Decision Support Framework. In Proceedings of the 36th International Conference on Software Engineering (ICSE 2014). ACM, New York, NY, USA, 503–514.</li>
  <li>[36] <a href="https://www4.cs.fau.de/Research/SEEP/">SEEDS: A Software Engineer’s Energy-optimization Decision Support Framework</a></li>
  <li>[37] <a href="https://pdfs.semanticscholar.org/4e6f/6d18f91c20660a19c65bee73c4cce801122e.pdf">SEEDS - Presentation</a></li>
  <li>[38] <a href="https://github.com/Spirals-Team/powerapi">PwerAPI - Github</a></li>
  <li>[39] A. Bourdon, A. Noureddine, R. Rouvoy, and L. Seinturier. 2012. PowerAPI: A Software Library to Monitor the Energy Consumed at the Process-Level. (2012). [Online]. Available: http://ercim-news.ercim.eu/en92/special/powerapi-a-software-library-to-monitor\-the-energy-consumed-at-the-process-level. [Accessed: 2016-06-13].</li>
  [40] S. Pandruvada. 2014. Running Average Power Limit — RAPL textbar 01.org. (2014). [Online]. Available: https://01.org/blogs/tlcounts/2014/running-average-power-limit---rapl. [Accessed: 2016-06-28].
  <li>[41] <a href="https://github.com/kliu20/jRAPL">jRAPL - Github</a></li>
  <li>[42] Kenan Liu, Gustavo Pinto, and Yu David Liu. 2015. Data-Oriented Characterization of Application-Level Energy Optimization. In Fundamental Approaches to Software Engineering, Alexander Egyed and Ina Schaefer (Eds.). Number 9033 in Lecture Notes in Computer Science. Springer Berlin Heidelberg, 316–331. DOI:10.1007/978-3-662-46675-9 21.</li>
  <li>[43] <a href="https://ss64.com/osx/top.html">MACOS manual</a></li>
  <li>[44] <a href="https://manpages.ubuntu.com/manpages/xenial/man1/top.1.html">Ubuntu Manual</a></li>
  <li>[45] <a href="https://developer.apple.com/library/archive/documentation/DeviceDrivers/Conceptual/IOKitFundamentals/TheRegistry/TheRegistry.html">The I/O Registry - Documentation</a></li>
  <li>[46] <a href="http://sbs-forum.org/specs/sbdat110.pdf">Smart Battery Data Specification</a></li>
  <li>[47] <a href="https://plugins.jetbrains.com/plugin/15637-ecoandroid">EcoAndroid</a></li>
</ul>
