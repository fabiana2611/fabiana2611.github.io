---
layout: post
title:  "PL/SQL - Using a sql result"
date:   2019-07-17
categories: database
permalink: /:categories/plsql-example
---

<blockquote>
  <p style="text-align: justify;">PL/SQL is a powerful, yet straightforward database programming language. It is easy to both write and read and comes packed with lots of out-of-the-box optimizations and security features. <a href="https://www.oracle.com/database/technologies/appdev/plsql.html">[1]</a>
</p>
</blockquote>

<p style="text-align: justify;">This post is not to speak about PL/SQL in a deep way. There are many tutorials that you can find to learn how to program with that. What I'd like to do in this post is to share a scenario that I needed.
It's a simple example that will make you get an idea of the use. PS: It's a beginner scenario.</p>

<p style="text-align: justify;">The PL/SQL is a great option when you need a complex SQL with dependencies.
A common scenario is when you need to select a list of results and use this in another select.</p>

<p style="text-align: justify;">Of course, you can just run a simple SQL. The best choice will depend on what you need.</p>

{% highlight ruby %}
DECLARE
  quantity integer :=0;
BEGIN
  SELECT count(\*) INTO quantity
  FROM TABLE_TESTE
  WHERE TABLE_TESTE.TYPE = 'Type A';
  dbms_output.put_line ('Quantity: ' ||quantity );
END;
{% endhighlight %}

<p style="text-align: justify;">An example where you need to use the result of a query is when you need a list of IDs to use in another query.</p>
<p style="text-align: justify;">The first example is using cursor. The code below iterates in the cursor and create a string with ids split by comma.</p>
<p style="text-align: justify;">The string will be used in the second SQL inside the 'EXECUTE IMMEDIATE'. The second result will be stored in 'quantity' attribute.</p>

{% highlight ruby %}
DECLARE
  CURSOR c_tableTest is
    SELECT IDTESTE FROM TABLE_TESTE
    WHERE TTYPE_TESTE = 'Type A';
  listIds_str varchar2(1000);
  quantity integer :=0;

  BEGIN

    FOR id IN c_tableTest LOOP
        listIds_str := id.idteste || ',' || listIds_str;
    END LOOP;

    listIds_str := Substr(listIds_str, 0, Length(listIds_str)-1);

    dbms_output.put_line(listIds_str);

    execute immediate 'SELECT count(\*)
         FROM TABLETESTE_TABLESUPERTESTE
         WHERE TABLETESTE_TABLESUPERTESTE.IDTESTE IN ( '||listIds_str|| ' )'
         INTO quantity;

    dbms_output.put_line ( 'Quantity: ' ||quantity );

END;
{% endhighlight %}

If you don't want to use CURSOR, another option is..

{% highlight ruby %}
DECLARE
  TYPE IdsList IS TABLE OF NUMBER;
  ids IdsList;
  quantity integer :=0;
BEGIN

  EXECUTE IMMEDIATE 'SELECT IDTESTE FROM TABLE_TESTE
  WHERE TYPE_TESTE = ''Type A'' '
  BULK COLLECT INTO ids;

  FORALL i IN ids.first..ids.last
    execute immediate
      'SELECT count(\*)
       FROM TABLETESTE_TABLESUPERTESTE
       WHERE TABLETESTE_TABLESUPERTESTE.IDTESTE = :1'
       USING ids(i);
    END;
{% endhighlight %}

<p style="text-align: justify;">In my case, the scenario that I had to solve, I had to storage attributes to reuse in the second query. To this case, the query that I used was...</p>

{% highlight ruby %}
DECLARE
  TYPE IdsCurTyp IS REF CURSOR;
  TYPE IdsTesteAList IS TABLE OF NUMBER;
  TYPE IdsTesteBList IS TABLE OF NUMBER;
  ids_cv IdsCurTyp;
  testea IdsTesteAList;
  testeb IdsTesteBList;
  sql_stm VARCHAR(1000);
BEGIN

  sql_stm := 'SELECT TESTEA_TESTEB.IDTESTEA, TESTEA_TESTEB.IDTESTEB
              FROM TESTEA
                JOIN TESTEA_TESTEB ON TESTEA.IDTESTEA = TESTEA_TESTEB.IDTESTEB
                JOIN TESTEA_TESTEB ON TESTEA_TESTEB.IDTESTEB = TESTEB.TESTEB
              WHERE CDTESTEA.TYPE_TESTE = ''Type A'' ';

  OPEN ids_cv FOR sql_stm;
  FETCH ids_cv BULK COLLECT INTO testeb, testea;
  CLOSE ids_cv;

  dbms_output.put_line('testea.count: ' || testea.count);
  dbms_output.put_line('testeb.count: ' || testeb.count);

  FORALL i IN testea.first..testea.last
     execute immediate
       'DELETE FROM TESTEA_TESTEB WHERE TESTEA_TESTEB.IDTESTEA = :1 and TESTEA_TESTEB.IDTESTEB = :2'
     USING testea(i), testeb(i);

END;
{% endhighlight %}

<br/>

<h3>Statement</h3>

EXECUTE IMMEDIATE : "prepares (parses) and immediately executes a dynamic SQL statement or an anonymous PL/SQL block" <a href="https://docs.oracle.com/cd/B12037_01/appdev.101/b10807/11_dynam.htm">[2]</a>. It use a string argument that is the SQL and can be use with other clauses:
<ul>
  <li>INTO: used to an individual result</li>
  <li>BULK COLLECT: used to more than one result</li>
  <li>USING: used to pass arguments to the query</li>
</ul>

FORALL: It do process to all elements. It's similar to the loop.

TYPE ... IS TABLE OF .... TYPE: It can be used to create an attribute that will be stored in a temporary table. It can be used instead of varrays.

CURSOR: it is a pointer to a memory area where is possible control the rows returned by a SQL statement. <a href="https://www.tutorialspoint.com/plsql/plsql_cursors.htm">[3]</a>

<h3>Conclusion</h3>


<p style="text-align: justify;">These are simple examples of how to use PL/SQL. Maybe some of these can be simpler. The idea is to see the possibilities.</p>

<p style="text-align: justify;">A point to say here is that you cannot use an array inside the clause IN of the SQL. And that why In some cases I created a string and put the result inside the SQL that wherein the "EXECUTE IMMEDIATE". </p>

<br/>

<h3>References</h3>

<ul>
	<li><a href="https://www.tutorialspoint.com/plsql/plsql_arrays.htm" >TutorialsPoint</a>
  </li>
  <li><a href="https://docs.oracle.com/cd/B12037_01/appdev.101/b10807/11_dynam.htm" >Docs Oracle</a>
  </li>
  <li><a href="http://www.dba-oracle.com/plsql/t_plsql_dynamic.htm" >PlSQL Dynamic - Oracle</a>
  </li>
  <li><a href="https://stackoverflow.com/questions/36501355/pl-sql-dynamic-sql-using-clause" ><StackOverflow</a>
  </li>
  <li><a href="https://web.stanford.edu/dept/itss/docs/oracle/10gR2/appdev.102/b14261/executeimmediate_statement.htm" >Execute Immediate Statement</a>
  </li>
  <li><a href="https://www.ibm.com/support/knowledgecenter/en/SSEPGG_11.1.0/com.ibm.db2.luw.apdv.plsql.doc/doc/r0055453.html" >IBM PL/SQL doc</a>
  </li>
  <li><a href="http://www.rebellionrider.com/how-to-create-varrays-as-pl-sql-block-member-in-oracle-database/" >How to create varrays - Oracle</a></li>
</ul>
