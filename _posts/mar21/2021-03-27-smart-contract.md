---
layout: post
title:  "Smart Contract"
date:   2021-03-27
categories: blockchain
permalink: /:categories/smart-contract
---

<p style="text-align: justify;">The <a href="https://fabiana2611.github.io/blockchain/ethereum">last</a> post I listed some important bullet points I considered important to start the path to learn Ethereum and concepts around that theme.</p>

<p style="text-align: justify;">Ethereum is an application of the blockchain such as bitcoin. The cryptocurrency to allow transactions in the ethereum network is the ETHER (ETH). The incentive to verify or execute the transactions is the payment of a fee, the gas, a fraction of ETH. The transactions are verified by the nodes.</p>

<p style="text-align: justify;">The interaction with ethereum can happen through the DAPPs, (decentralized application) which combine smart contracts and frontend user interfaces. The executions are done inside the EVM (Ethereum Virtual Machine). The dapps can interact with a library in JavaScript <a href="https://ethereum.org/en/developers/docs/web2-vs-web3/">web3</a>.</p>

<h2>What is</h2>

<blockquote>A "smart contract" is simply a program that runs on the Ethereum blockchain. It's a collection of code (its functions) and data (its state) that resides at a specific address on the Ethereum blockchain. </blockquote>

<p style="text-align: justify;"> The idea is to have a contract between two or more parts that allow the parts to transact directly with each other. That contract has rules which parts agree to execute.  The contract is the law. No one has the control and is not necessary a third part. The contracts are distributed and the outcome is validated by networks. </p>

<p style="text-align: justify;">That program has life in blockchain. After created and commited to the blockchain the contract cannot be changed anymore. It makes the contracts immutable. If exist same error with the contract is necessary to create another one with the fix and redirect your application to the new contract. The code is executed in the EVM. </p>

<blockquote>The only possibility that code is removed from the blockchain is when a contract at that address performs the selfdestruct operation. The remaining Ether stored at that address is sent to a designated target and then the storage and code is removed from the state. <a href="https://docs.soliditylang.org/en/v0.4.24/introduction-to-smart-contracts.html#self-destruct">[Self-destruct]</a></blockquote>

<p style="text-align: justify;">The most popular languages to create a contract are <a href="https://ethereum.org/en/developers/docs/smart-contracts/languages/">Solidity and Vyper</a>. The first one is the most popular. The languages to create dapps can be <a href="https://geth.ethereum.org/docs/dapp/native-bindings">Java, Go, JavaScript, .NET, Python, Rust</a>.</p>

<p style="text-align: justify;">Stack: Smart Contract (your program to execute on blockchain), EVM (runtime environment for smart contracts), Node (do the communication between the dapp and the network), APIs (allow user applications to connect/communicate with the Ethereum blockchain/Node.), End User App (Web/Mobile).</p>

<p>Advantages: Autonomy, Trust, Backup, Safety, Speed </p>

<p><center>
  <iframe width="560" height="315" src="https://www.youtube.com/embed/ZE2HxTmxfrI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center></p>

<h2>Beginning...</h2>

<p style="text-align: justify;">If you want to start to understand how to create one contract in a funny way without any dependencies you can start by <a href="https://cryptozombies.io/">Cryptozombies</a>, where you will start open your mind to the coding. <p>

<p style="text-align: justify;">To create your first smart contract you can use the online IDE <a href="https://remix.ethereum.org/">Remix</a>. As well, you need the Metamask plugin to create accounts to simulate the transactions, <a href="https://www.trufflesuite.com/">ganache</a> to simulate blockchain and test your development. Finally, web3.js allows your web app to use your contract. </p>

<p>Here is a simple example.</p>

{% highlight ruby %}
pragma solidity >=0.5.0 <0.6.0;

contract MyFirstContract {

    event NewEntity(uint id, string name, uint value);

    struct Type {
        string name;
        uint value;
    }

    Entity[] public entities;

    function _createEntity(string memory _name, uint _value) private {
        uint id = entities.push(Entities(_name, _value)) - 1;
        emit NewEntity(id, _name, _value);
    }

    function createRandomEntity(string memory _name) public {
        uint randValue = uint(keccak256(abi.encodePacked(_name))) % 16;
        _createEntity(_name, randValue);
    }
}
{% endhighlight %}

<p>Here one abstraction of the line where the JS could call the contract:</p>


{% highlight ruby %}
var MyFirstContract = web3.eth.contract(YYYYYYYYYY)
var contractAddress = XXXXXXXXXXX
var myFirstContract = MyFirstContract.at(contractAddress)
myFirstContract.createRandomEntity("TEST");
{% endhighlight %}  

<p>Next post I'll describe a complete use case.</p>

<h2>References</h2>

<ul>
  <li><a href="https://docs.soliditylang.org/en/v0.4.24/index.html">Solidity</a></li>
  <li><a href="https://cryptozombies.io/">Cryptozombies</a></li>
  <li><a href="https://remix.ethereum.org/">Remix</a></li>
  <li><a href="https://rubygarage.org/blog/guide-to-smart-contracts">A Guide to Smart Contracts and Their Implementation</a></li>
  <li><a href="https://blockgeeks.com/guides/smart-contracts/">Blockgeeks - Smart Contracts: The Blockchain Technology That Will Replace Lawyers</a></li>
  <li><a href="https://swissborg.com/blog/smart-contracts">What are smart contracts and how do they work?</a></li>
  <li><a href="https://www.freecodecamp.org/news/how-to-write-and-deploy-your-first-smart-contract-341d5e2ffb35/">How to write and deploy your first smart contract</a></li>
  <li><a href="https://thebitcamp.com/blog/smart-contracts">Smart Contract for Beginners: What is It and How It Works</a></li>
</ul>
