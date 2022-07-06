---
layout: post
title:  "Working with legacy code"
date:   2021-12-31
categories: foundation books
permalink: /:categories/legacy-code
---

<p style="text-align: justify;">I spend a good part of my developer life working with legacy code. Sometimes it is boring and sometimes exciting. There is a lot of learning on that, mainly with bad code to not repeat it.</p>

I got much of my knowledge on hands-on. I was so happy when I started to read the book [Working Effectively with Legacy Code][book-ref] and realized that I am on the right pathway.

<center>
  <p><img src="/img/legacycode/book.png" width="20%" height="20%"/></p>
</center>

<p style="text-align: justify;">In this post, I'd like to share a little bit about my experience and some notes I did while reading the book.</p>

<h2>Changes... what a pleasure! Or a headache?</h2>

<blockquote>What was delivered has to keep working.</blockquote>

<p style="text-align: justify;">The main point brought up when you are working with legacy code is about the changes. At the end of the day, all the changes are regarding the behaviour. Your strategy to do that work can be different if that requirement is a feature or a bugfix. A feature leads you to a really new code that probably will not impact what is already working (considering it is a well-defined requirement). A bugfix needs more attention on the impacts. The code fixed by a distracted developer can create many others errors hard to find. It impacts negatively the relationship with the customer. And once trust is lost, it will be hard work to rescue it again.</p>

We need to take care of some points. Legacy code is too hard to identify the causes and easy to create new errors. However, you don't need be afraid to change the code but take care of it. Even working in a legacy code we cannot forget we are developers and we have responsibilities. Whenever possible, we have to be focused on quality ([clean code][cleancode-ref], testable code, etc). I know... it can be so hard when the customer is focused on delivering, but we have to try.

<p style="text-align: justify;">You have to add features and fix bugs by demand. You should improve the code when you are confident enough to do it. But how to turn the table and brings confidence to developers?</p>

<p style="text-align: justify;">A good start point is when you have an integrated team. It helps a lot to encourage the team members and give support to it. Unfortunately, it's not the reality of most of the projects. Usually, the colleagues are much more afraid than you and it is a solo journey.</p>

<p>Hey... don't cry... I am with you. I know you can do it!!!!</p>

<h2>How to get the confidence</h2>

<blockquote>Trust in yourself. Or/And make your changes to be trusted.</blockquote>

<p style="text-align: justify;">A good way to have confidence to change the code is to know the business. A good documentation will help on it. If it is your case will be easier for you to understand the work and where to be focused. Also, it will make easier to identify your point of code. Good documentation is also important to protect the team when is necessary to define if a new issue is a bug or a new requirement. If it is a bug the fault is on the developer team debits. If it is a requirement not specified it will be on client debit. Don't be so innocent. It will be brought up on the table at the boss meeting and the numbers can lead to the decisions about the project's directions. </p>

<p style="text-align: justify;">Unfortunately (one more time :D) to have a good documentation is not a reality of many legacy projects. Then, you have to keep your eyes in the code. Unfortunately (again :P), sometimes the legacy code is a spaghetti without sauce, almost indigestible.</p>

<p><b>Take care about the impacts</b></p>
<p style="text-align: justify;"><u>New Features or bugfix:</u> For me, until now, there are no different starting points but DEBUG. You are completely new to the subject you need to search the possibilities of impacts. Search in the code all the terms regarding your subject, add breaking points and try to identify the points that can be impacted. When you find where will be your changes go back in the code to confirm who calls that point and note the different scenarios. Do your work and test all scenarios you found. After commit the code, if you are a Faith-Oriented programming, start to pray you haven't created new bugs ;-)</p>

<p style="text-align: justify;"><u>Refactory:</u> It is a good way to learning about the code. However, take care and verify the changes to be sure about the impacts. In this case, do a really small refactory. Don't forget to test again. Other important point is, just do refactory of the functionality you are working at moment(doesn't matter how many classes will be impacted) to be easier identify bad impact faster.</p>


<p><b>Working with feedbacks</b></p>
<p style="text-align: justify;">Another good way to make you become more confident (besides pray, of course :-*), is TEST. Now... let's go to the next  "Unfortunately"s :( . </p>

<p style="text-align: justify;">Unfortunately, the legacy projects usually are focused on delivery and not in the quality. It push the tests to a second plan. That wrong focus make you not capable to predict the bad consequences.</p>

<p style="text-align: justify;">Also, unfortunately, many legacy codes don't have tests or they cannot be trusted. The lack of trust happens either because it was done only to achieve the covering or because the code was changed and the developers forgot to improve the tests.</p>

<p style="text-align: justify;">The covering test can be painful and demotivating work because you don't have time/budget to fix the existent tests or create new tests for all the classes. Even on that scenario is better you have that vision (sonar). Your tests (new or improvements) have to be focused on the classes you are working on currently. In this case, the coverage have to be focused on new codes and not all the project's code. To use all the legacy code to validate the quality of code is not fair with a dedicated developer. For sure is a good practice to have that kind of analysis and, one day, with a team on the same page, all the tests will be trusted and the project will have coverage more than 80%.</p>

<p style="text-align: justify;">Even though your customer says "It should be delivered as faster as possible" you cannot leave the tests behind. Be creative and do a strategy to satisfy the client and work on tests in the same way.</p>

<p style="text-align: justify;"><u>New Features or bugfix:</u> If you have a test which cover your functionality you are in the paradise. You just need run the test for each changes to verify you are not breaking anything. In case you have the test but it is not updated then fix the test before start your changes. It will make you more confident about the code. If you don't have tests you have two options: to use TDD and add the new code together with the test; or crate the test after the implementation. If the customer is pushing pressure on you then deliver the code but don't close your card until you finish the test.</p>

<p style="text-align: justify;"><u>Refactory:</u> This case is similar to the previous case, do the refactory only after you have a test that covers what already exists. If you don't have tests you will have to create. After that, you can do your refactory running the test for each change on your refactory.</p>

<p><b>Know the app structure</b></p>
<p style="text-align: justify;">It is not a easy work. It's hard to keep everyone aware of the structure. Usually, no one knows enough and the code tends to degrade. If one developer start to do it in the wrong way probably the others will follow the same wrong direction. It can take a long time for all the team to catch the big picture. It's necessary to have one or more team members to preserve the big picture. Those developers should guarantee all the others are doing good work and give direction to them. How to make everyone goes in the same direction? COMMUNICATION! The book gives the reference <a href="https://www.elsevier.com/books/object-oriented-reengineering-patterns/demeyer/978-1-55860-639-5">Object-Oriented Reengineering Patterns</a> as a way to maintain a good structure. </p>


<h2>Writing fresh code</h2>

One of the pitfalls we can confront in legacy code is dependency. Be focus on your subject. Don't try to understand or solve all the problems in the same time. A way to overcome it is doing a separation between your target and the other dependencies. The book has a list of [Dependency-Breaking Techniques][chapter25].

<p style="text-align: justify;">In terms of insert new code you can follow some alternatives.</p>

<ul>
  <li><b>Sprout Method:</b> add the new code in a separate method and create the specific test to it.</li>
  <li><b>Sprout Class:</b> add the new code in a new class. It is helpful in case of strong dependency situations. It give us confidence because it doesn't have too invasive changes inside old code.</li>
  <li><b>Wrap Method:</b>Separate one method in two methods, one method with the old code and a new one with your new code.</li>
  <li><b>Wrap Class:</b>Break the old and new code in two different classes. It follow the Decorator Pattern.</li>
</ul>

<p style="text-align: justify;">In terms of tests it can be done by the use of mocks and fake objets, for example. However, dependencies can be hard to break. Who already worked with legacy code has some idea how to do it, and the book let this more clear:</p>

- <b>Find Interception Points:</b> "An interception point is simply a point in your program where you can detect the effects of a particular change."
- <b>Find Pinch Points:</b> "A pinch point is a natural encapsulation boundary. It will facilitate move code if necessary. Writing tests at pinch points is an ideal way to start some invasive work in part of a program."
- <b>Pinch Point Traps:</b> "let unit tests slowly grow into mini-integration tests. When you start to notice that your tests are too large, you should break down the class that you are testing, to make smaller independent pieces that can be tested more easily".



<h2>Unit tests and Integration tests</h2>
<blockquote>Test when is possible. Test what is necessary.</blockquote>

<p style="text-align: justify;">The best scenario is to have at least a unit test for each class. However, when you work with legacy code you don't have time/budget enough to do it. Your efforts have to be directed by your functionality. Pay attention on the test because they can become the documentation of the actual behavior, helping you to preserve behavior already exist. </p>

<p><b>Scenario 1 - Changing in a SMALL public method </b></p>
<p style="text-align: justify;">It is the most simple case. You just need to do a simple change in an existing test method or create a new one. Be focused on your functionality. Even if the unit test class doesn't exist you will create a class and the test method to cover only your scenarios. if you have time, it would be good if you create tests to cover the entire public method you are testing. Don't forget that you may be the one to go back to this point for maintenance.</p>

<p><b>Scenario 2 - Changing in a PRIVATE method</b></p>
<p style="text-align: justify;">This scenario can be a private method that already exist or a new one you are creating in that moment. All the private method has as origin a public method. The best scenario is you test it through the test regarding the public method that call the private method. However, is not rare you have a big and complex methods that call many others. For this case, the best thing is to be focus on the private method and test only that. The book suggests as alternative turn the private method visible: changing it to public in the same class or creating a new class (as a utility) to be tested. I don't like the idea to change the logic and the concepts of the code to allow the tests. For me, the test has to cover the application and not app be adapted to the tests (for sure can have some exceptions). So, the strategy I usually use is the reflection. Using that resource I can see and call the private method and be focused on my changes without adapt the code for the tests. However, the reflection is not answer to all cases. You need verify the best alternative for you.</p>

<p><b>Scenario 3 - Changing in a BIG public method </b></p>
<p style="text-align: justify;">For this case, there is a big chance you have a complex method. It will be hard to cover all scenarios in the test class. So, create the basic scenarios to pass through all lines until achieve the point of code regarding your work. From that, create the different cases of tests to guarantee your changes. For sure if you have time and domain about that code you can create tests to cover all scenarios, but it is not the reality. If you have tests to cover at least your scenario is already a good work. Also, verify if it's not the time to extract code by responsibilities and create small methods to be called from the original one.</p>

<p><b>Scenario 4 - Test DAO classes</b></p>
<p style="text-align: justify;"> Usually those classes just retrieve data from database and don't have business logic. How that kind of tests will help to guarantee the quality? You need to verify if worth to test DAO classes. If you decide not to do that you can configure Sonar, for example, to not consider those classes as parameter to the coverage. If you decide to do the tests it is important you have in your mine that those tests cannot impact the database. For that, you can use, for example, in-memory database.</p>

<p><b>Scenario 5 - Integration tests</b></p>
<p style="text-align: justify;">In a big legacy code, you will find much complex interaction between classes. It will make the unit test not enough to guarantee some different scenarios. A good example is a mapper. Let's suppose you have new attributes passed from frontend to backend which will send to some other module. How to guarantee all the mappings are ok if you don't know all the code and if there is some point that can impact and not send the parameter in the endpoint? The integration test will help you with this. You create an Integration test regarding the first point in the backend and let it navigate through all the classes until the communication point with the other module. Then your test can verify if the attributes are there. As I mentioned before, you don't need to cover other scenarios different from your functionality. You can be focused on your case.</p>

<p><b>Scenario 6 - Using <a href="https://fabiana2611.github.io/foundation/design-pattern">Pattern</a> to test: make your tests useful and reusable</b></p>
<p style="text-align: justify;">It is a way to rest in peace at the end of the world :D. Remember you can be who will use that benefits. Creating a useful test will save time in the future. You can fix bugs only running the test and not all the applications. In the same way, reusable tests will save time to create new scenarios. A really good practice already very applied is using Builder Pattern to create the tests. For me, it is the "silver bullet" to help you create and reuse complex object used on the tests. You will find many references in a simple search on the web about that. Don't wait to convince all the team to work with that. Do it by your self. PS: Don't try to create all scenarios at the same time. It's a legacy code. You need select what worth. Go in baby steps. </p>

<h2>Refactoring a BIG class </h2>
<blockquote>Move the pieces.</blockquote>

<p style="text-align: justify;">It's not rare to find big classes in a legacy project. When and how to refactory? Focus on the current work. When you have a feature or bugfix and feel confident to do it, do it. The <a href="https://fabiana2611.github.io/foundation/solid-principles">Single-Responsibility Principle</a> lead the work. </p>

<p style="text-align: justify;">The idea is to break the class by scope, taking care about who will call the methods to not lose the behaviour. For every code, if you don't know what to do then let it in the same class. Probably the next time you go back to this class it can be clear for you. What is not part of your work just change the position. Don't change names or logic.  </p>

<p style="text-align: justify;">The start point is grouping functionalities/methods in the class. It will help to understand the scopes. Another strategy is to comment the private methods and identify what will not compile anymore. It helps to understand the dependencies and if the method is used in different scopes. If yes, it can be an alert that this method should be in a separate class (as a util class) to be used for all new classes. Extract common methods to a separate class to be used by different classes, avoiding duplication. Take care about instance variables to have it only in the class that really use it. Also, you can apply <a href="https://fabiana2611.github.io/foundation/solid-principles">the Interface Segregation Principle</a> to only expose part of the class to the client code, giving a clue about what can be moved away from the big class.  </p>

<p style="text-align: justify;">If nothing works and you are not safe to commit the code then don't commit. Do it in another moment. At least you started to know the class :D. If the original class has unit test class you have to do the same separation and run the tests for each changes. </p>

<h2>Removing code </h2>
<blockquote>Delete is harder than insert</blockquote>

<p style="text-align: justify;">Removing code is much harder than inserting a new one. Therefore, insert code if it has a purpose. Don't let a code that you believe one day, maybe or not, perhaps.... can be used. The next developer will not be sure about the consequence of removing it and the project will be full of trash code. Trust on git. You can recover old code. </p>

<p style="text-align: justify;">Another point is about duplicate code. It creates confusing maintenance. Duplicate code makes you do duplicate work, doing the same changes in all duplicated code. You can extract the code to a common point of code to be reused. Removing duplication makes code starts follow the <a href="https://fabiana2611.github.io/foundation/solid-principles">Open/Closed Principle</a> (code should be open for extension but closed to modification).</p>


<h2>Conclusion</h2>
<p style="text-align: justify;">I wanted here to share my experience with you and not only summarize the book (a good reference even nowadays). I added references that already make this summary at the end of this post. </p>

<p style="text-align: justify;">Working with legacy code does not mean it should be a mess. You cannot forget who you are and your responsibility. Pay attention to all the concepts you already have. Pay attention to clean code. Do not create new code that looks like legacy code. Don't be afraid to refactory. After some time you will be comfortable enough with it.</p>

<p style="text-align: justify;">Left the code better than you found.</p>


<h2>References</h2>

- [Working Effectively with Legacy Code - Summary][book-summary]
- [Working Effectively with Legacy Code - Amazon book][book-ref] <br />
1. [Changing Software (Part 1: Chapter 1)][chapter1] <br />
2. [Changing Software (Part 1: Chapter 2)][chapter2]
3. [Changing Software (Part 1: Chapter 3)][chapter3]
4. [Changing Software (Part 1: Chapter 4)][chapter4]
5. [Changing Software (Part 1: Chapter 5)][chapter5]
6. [Changing Software (Part 2: Chapter 1)][chapter6]
7. [Reflection about the chapter 6 to 10][chap6-10]
8. [Dependency-Breaking Techniques (Part 3: Chapter 25) ][chapter25]
- [How to deal with legacy code][blogcyril]
- [Clean Code][cleancode-ref] <br />
- [Using Builder Pattern in JUnit tests][builder-ut] <br />


[book-summary]: https://www.frederikbanke.com/book-review-working-effectively-with-legacy-code/#chapter-7-it-takes-forever-to-make-a-change
[book-ref]: https://www.amazon.es/Working-Effectively-Legacy-Robert-Martin/dp/0131177052/ref=asc_df_0131177052/?tag=googshopes-21&linkCode=df0&hvadid=54582498915&hvpos=&hvnetw=g&hvrand=9345068620875249139&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1005419&hvtargid=pla-138214717035&psc=1
[cleancode-ref]: https://fabiana2611.github.io/foundation/cleancode
[builder-ut]: https://www.javacodegeeks.com/2012/12/using-builder-pattern-in-junit-tests.html
[chapter1]: https://biratkirat.medium.com/working-effectively-with-legacy-code-changing-software-part-1-episode-1-2bf282f5260
[chapter2]: https://biratkirat.medium.com/working-effectively-with-legacy-code-changing-software-part-1-episode-2-1c4429721c53
[chapter3]: https://biratkirat.medium.com/working-effectively-with-legacy-code-changing-software-part-1-chapter-3-a87128445249
[chapter4]: https://biratkirat.medium.com/working-effectively-with-legacy-code-changing-software-part-1-chapter-4-b997b78fc0a2
[chapter5]: https://biratkirat.medium.com/working-effectively-with-legacy-code-mechanics-of-change-part-1-chapter-5-3dc6ad98dabf
[chapter6]: https://biratkirat.medium.com/working-effectively-with-legacy-code-mechanics-of-change-part-ii-chapter-1-91f2129c3b72
[chap6-10]: https://dev.to/dannypsnl/reflection-on-working-effectively-with-legacy-code-chapter-6-to-10-55g6
[chapter25]: https://gist.github.com/jonnyjava/42883d4e464167f81e2ee60a488a5ded#chapter-25-dependency-breaking-techniques
[blogcyril]: https://cyril.deguet.com/en/2017/01/09/how-to-deal-with-legacy-code/
