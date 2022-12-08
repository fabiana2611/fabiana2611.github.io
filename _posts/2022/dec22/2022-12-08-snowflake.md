---
layout: post
title:  "Snowflake - What is this?"
date:   2022-12-08
categories: infra
permalink: /:categories/snowflake
---

<p style="text-align: justify;"><em>Snowflake is an analytic data warehouse provided as Software-as-a-Service (SaaS).</em> Using SaaS, everything is manage by the provider.</p>

<blockquote>Snowflake’s Data Cloud is powered by an advanced data platform provided as Software-as-a-Service (SaaS). Snowflake enables data storage, processing, and analytic solutions that are faster, easier to use, and far more flexible than traditional offerings.</blockquote>


<p><table>
  <tr>
    <td><iframe src="https://www.youtube.com/embed/ryWCD00nLvQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe src="https://www.youtube.com/embed/slrqd4NSgpY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>
  <tr>
    <td><iframe src="https://www.youtube.com/embed/dZlBCLLL7UA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe src="https://www.youtube.com/embed/MEFlT3dc3uc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>
</table></p>

<p>It uses central data repository and processes queries using compute clusters.</p>

<ul>
  <li>Data Storage (S3): It uses Amazon S3 (usability, high availability, durability) to store table data and query results. It can have impact in latency and performance. Tables are horizontally partitioned. The data can be sorted along natural dimensions (clusters) to improve the performance.</li>
  <li>Virtual Warehouses (EC2): It handles query execution within elastic clusters of VM. They can be create or destroyed on demand.</li>
  <li>Cloud Services: services to manage virtual warehouse, queries (e.g parsing, optimization, detect failures), transactions (snapshot isolation - SI), etc.</li>
</ul>

<br />
<h3>References</h3>
<ul>
  <li><a href="https://docs.snowflake.com/">Snowflake's Documentation</a></li>
  <li><a href="https://www.udemy.com/course/snowflake-data-warehouse/">Udemy - Snowflake for Developers</a></li>
</ul>  
