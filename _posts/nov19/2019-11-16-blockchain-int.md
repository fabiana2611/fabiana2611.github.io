---
layout: post
title:  "Blockchain - Init"
date:   2019-11-16
categories: blockchain
permalink: /:categories/blockchain-int
---

<p style="text-align: justify;">I'm not sure if you already listened about Blockchain, but how about <a href="https://bitcoin.org/bitcoin.pdf">Bitcoin</a>? Probably yes, right? The Blockchain is the technology behind the cryptocurrency. However, this technology is used to much more scenarios: smart contracts (facilitate, verify, or negotiate a contract agreement), financial services, video games, security, Healthcare (store their patients’ medical records), Automobiles, Insurance, etc. It is a really safe technology. Most parts of the problems happen because of the users and not because of the technology.</p>
Here, let's understand the basic concepts about how the Blockchain works.

<em>The <a href="https://www.geeksforgeeks.org/blockchain-technology-introduction/">characteristics</a>: distributed, secure, transparent, consensus-based and flexible.</em>
<h2>What is this?</h2>
<p style="text-align: justify;">The Blockchain is a<a href="https://www.tutorialspoint.com/blockchain/blockchain_chaining_blocks.htm"><span style="color: #993366;"> list of blocks</span></a> (<span style="color: #ffcc00;">really? 🤔</span>) connected to each other by a <a href="https://fabiana2611.github.io/java/jca">cryptographic hash</a>. It is used to identify the previous block.</p>
<p style="text-align: justify;">Each <span style="color: #993366;">block</span> contains many <span style="color: #993366;">messages</span> (or transactions), timestamps (when the block was created) and <span style="color: #993366;">hash codes</span>. In fact, you will identify different types of hash codes. One is to identify the <em>previous block</em>, the other is the <em>root hash</em> that represents a list of hash inside a binary tree that regarding all the transactions, and the other is the <em>Nonce</em>.</p>

<center>
  <img src="/img/blockchain/blockstructure.png" width="732" height="488" />
  References: [<a href="https://www.geeksforgeeks.org/introduction-to-blockchain/">1</a>], [<a href="https://www.tutorialspoint.com/blockchain/blockchain_merkle_tree.htm">2</a>]
</center>
<br/>

<p style="text-align: justify;">When a new block is created, the hash used to identify this block is the combining of the <span style="color: #993366;"><em>previous hash,</em></span><span style="color: #993366;"><em> the root hash</em></span> and the <span style="color: #993366;"><em>Nonce</em></span> value. <span style="color: var(--color-text);">The </span>Nonce<span style="color: var(--color-text);"> is a calculated value used to identify the block. Below is a simplistic example of how to create the hash that will represent the block.</span></p>

<pre class="p1">//calculateBlockHash
String <span class="s1">dataToHash</span> = <span class="s2">previousHash</span> + Long.toString(<span class="s2">timeStamp</span>)
<span class="Apple-converted-space">    </span>+ Integer.toString(<span class="s2">nonce</span>)<span class="Apple-converted-space">  </span>+ <span class="s2">data</span>;
MessageDigest <span class="s1">digest</span> = MessageDigest.getInstance(<span class="s5">"SHA-256"</span>);
<span class="Apple-converted-space"><span class="s3">byte</span>[] <span class="s1">bytes</span></span> = <span class="s1">digest</span>.digest(<span class="s1">dataToHash</span>.getBytes());</pre>
<p style="text-align: justify;"><span style="color: var(--color-text);">The hash code is the key to verify if the block was modified. If a new process runs and generated a different hash code then it is known that this block was modified. A complete example of the <span style="color: #993366;"><em>Block class</em></span> you can see <a href="https://github.com/CryptoKass/NoobChain-Tutorial-Part-2/blob/master/src/noobchain/Block.java">here</a>.</span></p>
<p style="text-align: justify;">The process to create the new block is mining.</p>

<h2>Mining</h2>
<p style="text-align: justify;">The key point of the Blockchain is to be decentralized, based on <a href="https://en.wikipedia.org/wiki/Peer-to-peer">peer-to-peer</a> network. Each node is a machine with duplicate data that will help to maintain the integrity. It is a kind of distributed database with all records of transactions. Always when a computer connects to the network, a synchronization is started and a copy of the data is downloaded.</p>
<p style="text-align: justify;">The <a href="https://www.tutorialspoint.com/blockchain/bitcoin_mining.htm"><span style="color: #993366;">miners</span></a> are nodes on the network marked as available to process the messages. Any node inside the network is electable to be responsible to create the blocks, just need to have a good processing power.  The miners are responsible by process all the messages, create the new block and add the hash code from the last block inside the new block. That is the signature of the block. The miners can dispute the creation of the block. Will win who has a better performance.</p>

<center>
<img src="/img/blockchain/broadcast.png" width="176" height="201" />
</center>

<p style="text-align: justify;">The mining begins when a transaction is broadcasted to all the nodes and a miner selects the transaction to starts the process. This process finishes when the signature <a href="https://www.baeldung.com/java-blockchain#5-blockchain-verification">attends the requirements</a>. This requirement can be the size of the hash, the prefix is started by zero, etc.  Below, another <a href="https://www.baeldung.com/java-blockchain#3-have-we-mined-the-block-yet">example</a> of how to mine the block.</p>

<pre class="p1"><span class="s1">public</span> String mineBlock(<span class="s1">int</span> <span class="s2">prefix</span>) {
<span class="Apple-converted-space">    </span>String <span class="s2">prefixString</span> = <span class="s1">new</span> String(<span class="s1">new</span> <span class="s1">char</span>[<span class="s2">prefix</span>]).replace(<span class="s3">'\0'</span>, <span class="s3">'0'</span>);
<span class="Apple-converted-space">    </span><span class="s1">while</span> (!<span class="s4">hash</span>.substring(0, <span class="s2">prefix</span>).equals(<span class="s2">prefixString</span>)) {
<span class="Apple-converted-space">        </span><span class="s4">nonce</span>++;
<span class="Apple-converted-space">        </span><span class="s4">hash</span> = calculateBlockHash();
<span class="Apple-converted-space">    </span>}
<span class="Apple-converted-space">    </span><span class="s1">return</span> <span class="s4">hash</span>;
}</pre>
<h2>Proof of work</h2>
<p style="text-align: justify;">It is the process to guarantee that this block is correct. To do this, the <em>Nonce</em> part of the block is used by miners. This process starts when a miner creates a new block and broadcast this block to the other miners to confirm this new block before to be added inside the blockchain.</p>
<p style="text-align: justify;">If more then one miner in the network solves the Proof-of-Work and all of then connect the new block to the last block of the list, the list can have more then one branch. The next block has to choose which branch to use. It can be done by the newer criterion.</p>

<h2>How it works</h2>
<p style="text-align: justify;">The blockchain uses public-key cryptography to represent the address.  In a general view, some sender sends a <a href="https://github.com/CryptoKass/NoobChain-Tutorial-Part-2/blob/master/src/noobchain/Transaction.java">transaction</a> by broadcast and the owner uses the private key to access the messages. The miners validate the transactions, create the block and send it to all the nodes.</p>
The <a href="https://bitcoin.org/bitcoin.pdf">steps</a> cited in the bitcoin article are:
<ol>
	<li>New transactions are broadcast to all nodes.</li>
	<li>Each node collects new transactions into a block.</li>
	<li>Each node works on finding a difficult proof-of-work for its block.</li>
	<li>When a node finds a proof-of-work, it broadcasts the block to all nodes.</li>
	<li>Nodes accept the block only if all transactions in it are valid and not already spent.</li>
	<li>Nodes express their acceptance of the block by working on creating the next block in the chain, using the hash of the accepted block as the previous hash.</li>
</ol>
In blockchain only insert new block is permitted. No deletions or updates are permitted.
<h2>Videos</h2>
<table>
<tbody>
<tr>
<td style="text-align: center;"><strong>What is Blockchain</strong></td>
<td style="text-align: center;"><strong>What are miners</strong></td>
</tr>
<tr>
<td><iframe width="390" height="235" src="https://www.youtube.com/embed/SSo_EIwHSd4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
<td><iframe width="390" height="235" src="https://www.youtube.com/embed/RmhrGHKWZA8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Application</strong></td>
<td style="text-align: center;"><strong>19 Industry</strong></td>
</tr>
<tr>
<td><iframe width="390" height="235" src="https://www.youtube.com/embed/aQWflNQuP_o" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
<td><iframe width="390" height="235" src="https://www.youtube.com/embed/G3psxs3gyf8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
</tr>
</tbody>
</table>

<h2>References</h2>
<ul>
	<li><a href="https://www.tutorialspoint.com/blockchain/index.htm">Tutorial Point</a></li>
	<li><a href="https://en.wikipedia.org/wiki/Blockchain">Wikipedia</a></li>
	<li><a href="https://www.investopedia.com/terms/b/blockchain.asp">InvestOpedia</a></li>
	<li><a href="https://www.geeksforgeeks.org/blockchain-technology-introduction/">Java Code Geeks - Set 1</a></li>
	<li><a href="https://www.geeksforgeeks.org/introduction-to-blockchain/">Java Code Geeks -  Set 2</a></li>
	<li><a href="https://www.javacodegeeks.com/2019/02/6-blockchain-career-options-need-know.html">Java Code Geeks - Career</a></li>
	<li><a href="https://www.javacodegeeks.com/2018/03/a-beginners-guide-to-testing-blockchain-applications.html">A Beginner’s Guide to Testing Blockchain Applications</a>
</li>
	<li class="eg b eh eo ef"><a href="https://blog.goodaudience.com/how-a-miner-adds-transactions-to-the-blockchain-in-seven-steps-856053271476">Blockchain: how mining works and transactions are processed in seven steps</a></li>
	<li><a href="https://dev.to/damcosset/blockchain-what-is-mining-2eod">Blockchain: What is Mining?</a>
</li>
	<li><a href="https://www.baeldung.com/java-blockchain">Implementing a Simple Blockchain in Java</a>
</li>
	<li><a href="https://medium.com/programmers-blockchain/create-simple-blockchain-java-tutorial-from-scratch-6eeed3cb03fa">Creating Your First Blockchain with Java. Part 1</a></li>
</ul>
