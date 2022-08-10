---
layout: post
title:  "Legacy Displacement"
date:   2022-08-08
categories: foundation
permalink: /:categories/legacy-displacement
---

<p>This post is a small review of the post written by Ian Cartwright, Ron Horn and James Lewis. Their post is not only a description of good practices but also you can hear a good podcast where they discuss the subject: <a href="https://martinfowler.com/articles/patterns-legacy-displacement/">Patterns Legacy Displacement.</a></p>

<p>They prepared a set of patterns (or suggestions) to help to make decisions when we are working with legacy code. I'll not go deeply here because their explanation is very complete and helpful. More details you can go directly to the original post. Here, I want to take some notes to make my life easier when I need to review the concepts. Maybe it can help you too.</p>

<br />
<h3>init()</h3>

<blockquote>The technology is at most only 50% of the legacy problem, ways of working, organization structure and leadership are just as important to success.</blockquote>

<p>Some points that can lead to failures:<p>

<ul>
  <li>Change the technology but not change the other parts involved (structure, way to work, leadership).</li>
  <li>The gap between what the business actually needed and what was actually signed off at the start of the plans.</li>
  <li>Feature Parity: What exist should continues working in the same way. It is the "as-is" functionality, The challenge here can be in the definition and agreements.</li>
</ul>

<p>The Feature Parity is to delivery the same functionality but with different technology. It can be very useful, for sure. However, the team can be loosing opportunity to improve the system and cut not used features.<p>


<p>The authors give as alternative the approaches:</p>
<ul>
  <li>Extract Product Lines or Extract Value Streams: <em>give strategies for identifying thin slices through an existing system. By splitting by product we are taking advantage of the fact that changes to multiple products can be made simultaneously, and reducing risk by avoiding the combinatorial explosion of changes that may introduce defects in unwanted places.</em></li>
  <ul>
    <li>Identify the product or product lines within the system.</li>
    <li>Identify shared capabilities.</li>
    <li>Choose who goes first.</li>
    <li>Identify your target software architecture</li>
    <li>Identify your technical migration strategy.</li>
  </ul>
  <li><em>Looking at the business value and making sure that is represented in any architectural decisions can often highlight issues with Feature Parity driven approaches.</em></li>
  <li><em>Treating technology and business process as part of the same problem. Just replacing the tech will leave at least half the problem unsolved.</em></li>
</ul>

<br />
<h3>logger.info("Starting....")</h3>

<p>Categories of direction to identify the priority:</p>
<ul>
  <li>Reducing the cost of change, </li>
  <li>Improving the business process, </li>
  <li>Retire an old system,</li>
  <li>Imminent Disruption (external event)</li>
  <li>Newer technology </li>
  <li>Decide how to break the problem up into smaller parts</li>
  <li>Successfully deliver the parts</li>
  <li>Change the organization to allow this to happen on an ongoing basis</li>
</ul>

<p>Resources to break the problem in smaller parts and which will help to understand it:</p>
<ul>
  <li>Event Storming</li>
  <li>Wardley Mapping</li>
  <li>Business Capability Mapping</li>
  <li>Domain Mapping</li>
</ul>

<br />
<h3>The patterns</h3>

<p>Here I just print the patterns discussed in the article by the authors.</p>

<p><center>
  <img src="/img/legacycode/patterns.png" />
  <br />
  <em>Ref: <a href="https://martinfowler.com/articles/patterns-legacy-displacement/">Patterns of Legacy Displacement</a></em>
</center></p>


<p>And here some other patterns: </p>

<ul>
  <li>Versioned Value: to validate the most recent data</li>
  <li>Write-Ahead Log: Provide durability guarantee without the storage data structures to be flushed to disk, by persisting every state change as a command to the append only log</em></li>
  <li>Leader and followers: Replicate the write-ahed log:</li>
  <li>Segmented Log: <em>Split log into multiple smaller files instead of a single large file for easier operations.</em></li>
  <li>Low-Water Mark: <em>An index in the write ahead log showing which portion of the log can be discarded.</em></li>
  <li>Singular Update Queue: <em>Use a single thread to process requests asynchronously to maintain order without blocking the caller.</em></li>
  <li>State Watch: <em>Notify clients when specific values change on the server</em></li>
</ul>


<br />
<h3>exit()</h3>

<p> The article has two podcasts about the subject. Take a look at those links.</p>

<br />
<h3>REFERENCE</h3>

<ul>
  <li><a href="https://martinfowler.com/articles/patterns-legacy-displacement/">Patterns of Legacy Displacement</a></li>
  <li><a href="https://gotoaarhus.com/2022/sessions/2070/patterns-of-legacy-displacement">goto - presentation</a></li>
  <li><a href="https://martinfowler.com/articles/patterns-legacy-displacement/feature-parity.html">Feature Parity</a></li>
  <li><a href="https://martinfowler.com/articles/patterns-legacy-displacement/extract-product-lines.html">Extract Product Lines</a></li>
  <li><a href="https://martinfowler.com/articles/patterns-legacy-displacement/extract-value-streams.html">Extract Value Streams</a></li>
  <li><a href="https://fabiana2611.github.io/foundation/books/legacy-code">Working with legacy code</a></li>
  <li><a href="https://martinfowler.com/articles/patterns-of-distributed-systems/versioned-value.html">Versioned Value</a></li>
  <li><a href="https://martinfowler.com/articles/patterns-of-distributed-systems/wal.html">Write-Ahead Log</a><li>
  <li><a href="https://martinfowler.com/articles/patterns-of-distributed-systems/log-segmentation.html">Segmented Log</a><li>
  <li><a href="https://martinfowler.com/articles/patterns-of-distributed-systems/low-watermark.html">Low-Water Mark</a><li>
  <li><a href="https://martinfowler.com/articles/patterns-of-distributed-systems/singular-update-queue.html">Singular Update Queue</a><li>
  <li><a href="https://martinfowler.com/articles/patterns-of-distributed-systems/state-watch.html">State Watch</a><li>
  <li><a href="https://martinfowler.com/articles/patterns-legacy-displacement/divert-the-flow.html">Divert the Flow</a><li>
  <li><a href="https://martinfowler.com/articles/patterns-legacy-displacement/transitional-architecture.html">Transitional Architecture</a><li>
  <li><a href="https://martinfowler.com/articles/patterns-legacy-displacement/revert-to-source.html">Revert to Source</a><li>
  <li><a href="https://martinfowler.com/bliki/BranchByAbstraction.html">BranchByAbstraction</a><li>
</ul>
