---
layout: post
title:  "Fundamentals of Software Architecture - Part I"
date:   2022-03-19
categories: arch
permalink: /:categories/sw-arch
---

<p style="text-align: justify;">If the architecture is your target... the Fundamentals are your step 0. The post will not go deep inside the concepts because they are not new. The idea is to organize the concepts in terms of architecture using the book <a href="https://fundamentalsofsoftwarearchitecture.com/">Fundamentals of Software Architecture</a> as a guide. </p>

<h2>Architect vs Architecture</h2>

<p style="text-align: justify;">An application architecture define the way the data, logic and presentation are distributed between clients and servers (how end user interact with the software). The architect is involved on that definition with a different view comparing with the developer. The architect has a view focus on business.</p>

<h2>The Architect</h2>

<p style="text-align: justify;">The authors give to us a guideline how to become an architect. The figures and videos below were done by Mark Rechards who explain it. You have to be aware of what is it, develop yourself with technical and soft skills, you will have to have domain over some technologies and at least a good understanding about others to be capable to make decisions, you have to be aware you can not solve all the problems (sometimes you have to decide what win and what lose).</p>

<table>
  <tr>
    <td colspan="2"><img src="/img/architecture/becomearch.png" width="70%" height="70%"/></td>
  </tr>

  <tr>
    <td colspan="2"><img src="/img/architecture/roadmap.png" width="70%" height="70%"/></td>
  </tr>

  <tr>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/FKYKeqWfyIs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/olMSYbBP4y8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>

  <tr>
    <td><iframe src="https://www.youtube.com/embed/KyaU47XJNIk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe src="https://www.youtube.com/embed/fS8Ejg3qsJI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>

  <tr>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/G6TBHYPGTls" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe src="https://www.youtube.com/embed/2MeAxl2skpI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>

</table>

<p>Here is what is expecting from an architect:</p>

- Make architecture Decisions
- Continually analyze the Architecture
- Keep current with latest trends
- Ensure compliance with Decisions
- Diverse exposure and experience
- Have business domain knowledge
- Posses interpersonal skills
- Understand and navigate politics

<h2>The Architecture</h2>

<p style="text-align: justify;">The <a href="https://fundamentalsofsoftwarearchitecture.com/">Mark/Neal's book</a> define the architecture as a combination of structure, characteristics, design principles (components) and decisions.</p>

<p style="text-align: justify;">The <b>Structure</b> is regarding the type of architecture style (e.g: microservice, layred, microkernel). The design/components is a guideline to the development. The <b>Decision</b> is the path to follow to define the architecture trying to make it more stable and more useful the the business.</p>

<p style="text-align: justify;">The <b>Characteristics</b> are regarding non-domain requirements (non-functional requirement), it can influence the structure and is critical or important to the application. The authors categorized some of them:</p>

- Operational: Availability, continuity, performance, recoverability, reliability, robustness, scalability
- Structural: configurability, extensibility, installability, reuse, localization, maintainability, portability, supportability, upgradeability
- Cross-cutting: accessibility, archivability, authentication, authorization, legal, privacy, security, supportability, usability

<p>The <a href="https://oreil.ly/SKc_Y">ISO 25000</a> organized by capability.</p>

<table>
  <tr>
    <td><img src="/img/architecture/structure.png"/></td>
    <td><img src="/img/architecture/characteristics.png"/></td>
    <td><img src="/img/architecture/decisions.png"/></td>
    <td><img src="/img/architecture/design.png"/></td>
  </tr>
  <tr>
    <td colspan="4">
      <iframe width="100%" height="50%" src="https://www.youtube.com/embed/U6rfJjd8714" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </td>
  </tr>
</table>

<h2>The Measures</h2>

<p style="text-align: justify;">The modularity is the a key point in the architecture. The architect try to make the architecture more modular to facilitate the maintainability and reuse. Three concepts guide to it: <a href="https://www.geeksforgeeks.org/software-engineering-coupling-and-cohesion/">cohesion, coupling</a> and <a href="https://connascence.io/">connascence</a>.</p>

<h3>Cohesion</h3>

<p style="text-align: justify;"><a href="https://en.wikipedia.org/wiki/Cohesion_(computer_science)">Definition</a>: the degree to which the elements inside a module belong together. Or how focused the module is on a single scope.</p>

<p><u> 1 Strong Cohesion</u>:</p>
- Functional Cohesion: <em>parts of a module are grouped because they all contribute to a single well-defined task of the module</em>

<p><u>2 Medium Cohesion</u>:</p>
- Communicational Cohesion:<em>parts of a module are grouped because they operate on the same data</em>
- Procedural Cohesion: <em>parts of a module are grouped because they always follow a certain sequence of execution </em>
- Sequential Cohesion:<em>parts of a module are grouped because the output from one part is the input to another part like an assembly line</em>

<p><u>3 Weak Cohesion</u>:
- Coincidental Cohesion: <em>parts of a module are grouped arbitrarily; the only relationship between the parts is that they have been grouped together </em>
- Temporal Cohesion: <em> parts of a module are grouped by when they are processed - the parts are processed at a particular time in program execution</em>
- Logical Cohesion: <em>parts of a module are grouped because they are logically categorized to do the same thing even though they are different by nature</em>


<h3>Coupling</h3>

<p style="text-align: justify;"><a href="https://en.wikipedia.org/wiki/Coupling_(computer_programming)">Definition</a>: coupling is the degree of interdependence between software modules; a measure of how closely connected two routines or modules are.</p>

<p><u>1 Tight Coupling</u>: strong dependence, hard to change, hard to track bugs.</p>
- Content Coupling: <em>one module uses the code of another module</em>
- Common Coupling: <em>several modules have access to the same global data</em>
- External Coupling: <em>several modules have direct access to the same external Input/Output</em>

<p><u>2 Medium Coupling</u>: medium dependence</p>
- Control Coupling: <em>data is passed that influences the internal logic of another module</em>
- Data Structure Coupling: <em>multiple modules share the same data-structure</em>

<p><u>3 Loose Coupling</u>: low level</p>  
- Data Coupling: <em>two modules share the same data</em>
- Message Coupling: <em>messages or commands are passed between modules</em>
- No Coupling: <em>No communication between modules whatsoever</em>


<table>
  <tr>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/lUrgx6UIsWk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/XnBhVwm_Lws" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>
</table>

<h3>Connascence</h3>

<p style="text-align: justify;"><a href="https://en.wikipedia.org/wiki/Connascence">Definition:</a>two components are connascent if a change in one would require the other to be modified in order to maintain the overall correctness of the system.</p>

<p><u>1 Static</u>: source-code-level coupling</p>  
- Name: multiple components must agree on the name of an entity.
- Type: multiple components must agree on the type of an entity.
- Meaning/Convention: multiple components must agree on the meaning of particular values.
- Position: multiple components must agree on the order of values.
- Algorithm: multiple components must agree on a particular algorithm.

<p><u>2 Dynamic</u>:
- Types:
<ul>
  <li>Execution: the order of execution of multiple components is important.</li>
  <li>Timing: the timing of the execution of multiple components is important.</li>
  <li>Values: several values must change together.</li>
  <li>Identity: multiple components must reference the entity.  </li>
</ul>
- Properties: strength (how can be refactored), locality, degree

<br/><br/><br/><br/>
<h1 style="font-size: 24px; color: SlateBlue;"><b><em> Be continued ... </em></b></h1>
<br /><br />

<h2>Reference</h2>

<ul>
  <li><a href="https://fundamentalsofsoftwarearchitecture.com/">Fundamentals of Software Architecture - Mark Richards & Neal Ford</a></li>
  <li><a href="https://developertoarchitect.com/">Developer to Architect</a></li>
  <li><a href="https://www.youtube.com/watch?v=KUsl38hURdI&list=PLzNpWnYwBqfHuiTG0Ftjg2H1mlSu07Wwe&index=4">Soft Skills Videos</a></li>
  <li><a href="https://github.com/zhangjunhd/reading-notes/blob/master/software/FundamentalsOfSoftwareArchitecture.md">FundamentalsOfSoftwareArchitecture.md</a></li>
</ul>
