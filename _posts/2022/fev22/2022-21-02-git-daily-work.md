---
layout: post
title:  "Git - Daily work commands"
date:   2022-02-21
categories: infra
permalink: /:categories/git-daily-work
---

<p style="text-align: justify;">This post will give a summary of the git commands and a parallel view of the tree. It is not another tutorial. There are many really good ones.</p>

<p>PS: The trees created here was done by <a href="https://git-school.github.io/visualizing-git/#free">gitHub School</a>.</p>

<h2>First of all...</h2>

- Config the account
{% highlight ruby %}
$ git config —global user.name “Example”
$ git config —global user.email “example@example”
{% endhighlight ruby %}

- Each commit is uniquely identified (SHA1 hash): 79fc79530ecf44809d0aaeb93830ec23a5254d66

- You just need the first seven values in hash code to give as reference in git commands. For example, you just need 79fc795 to do some reference to the previous commit.

<h2>Starting by Local works</h2>

<p>Here is a summary about the first steps. After the Step 4 you will have the folder '.git'. </p>

{% highlight ruby %}
# 1 Create your project folder
$ mkdir MyTestProject
# 2 Go inside
$ cd MyTestProject
# 3 Create a file
$ touch myFirstFile.txt
# 4 Init the git repository
$ git init
# 5 Adding file to the staging area
$ git add myFirstFile.txt
# 6 Commit your file locally
$ git commit -m “First commit”
# 7 See the history
$ git log
# 8 See the status
$ git status

# History in the console
commit 20d9288c202376bc7230f1e08becfa60ac1d0f7c (HEAD -> master)
Author: Name Last  <example@example>
Date:   Mon Feb 21 09:20:40 2022 +0100
    First Commit

{% endhighlight %}

<p><center>
  <img src="/img/infra/git/firstcommit.png" width="60%" height="60%"/>
</center></p>

<p>Now, let's improve the scenario adding a new file.</p>

{% highlight ruby %}
# 9 Create a second file
$touch mySecondFile.txt
# 10 Add to stage area
$git add mySecondFile.txt
# 11 Commit the file
% git commit -m "Second Commit"
# 12 See the history
$ git log

# History in the console
commit 79fc79530ecf44809d0aaeb93830ec23a5254d66 (HEAD -> master)
Author: Name Last  <example@example>
Date:   Mon Feb 21 09:49:30 2022 +0100

    Second Commit

commit 20d9288c202376bc7230f1e08becfa60ac1d0f7c
Author: Name Last  <example@example>
Date:   Mon Feb 21 09:20:40 2022 +0100

    First Commit

{% endhighlight %}

<p>And here is how supposed to be the tree.</p>

<p><center>
  <img src="/img/infra/git/secondcommit.png" width="60%" height="60%" />
</center></p>

<p>Now, let's change both files (adding any text inside the files) and commit them.</p>

{% highlight ruby %}
# 13 Add all files to the staging area
$git add .
# 14 Commit them
% git commit -m "Third Commit"
{% endhighlight %}

<p><center>
  <img src="/img/infra/git/thirdcommit.png" width="60%" height="60%"/>
</center></p>

<p>Next level ... let's <a href="https://git-scm.com/docs/git-revert">revert</a> the commits. </p>

<p><em>git revert is used to record some new commits to reverse the effect of some earlier commits (often only a faulty one). This requires your working tree to be clean (no modifications from the HEAD commit).</em></p>

{% highlight ruby %}
# 15 Remove last modification
$git revert -n HEAD
# 16 Commit the reverted file
$git commit -m "Reverting the third commit"
# 17 Returning modification
$git revert -n HEAD
# 18 Commit the second revert
$ git commit -m "Reverting the revert"
# 19 See the log
$ git log

# History in console
commit 457f13d5b8649f59587979d30af20f0a72590118 (HEAD -> master)
Author: Name Last  <example@example>
Date:   Mon Feb 21 10:18:21 2022 +0100

    Reverting the revert

commit 12c4fda1950c7730c82d5b2dac873bc278d9d3e5
Author: Name Last  <example@example>
Date:   Mon Feb 21 10:15:14 2022 +0100

    Reverting the third commit

commit d75b40a8f1be78ba3abbb6d206ac82283ca9bc65
Author: Name Last  <example@example>
Date:   Mon Feb 21 10:01:18 2022 +0100

    Third Commit

commit 79fc79530ecf44809d0aaeb93830ec23a5254d66
Author: Name Last  <example@example>
Date:   Mon Feb 21 09:49:30 2022 +0100

    Second Commit

commit 20d9288c202376bc7230f1e08becfa60ac1d0f7c
Author: Name Last  <example@example>
Date:   Mon Feb 21 09:20:40 2022 +0100

    First Commit
{% endhighlight %}

<p style="text-align: justify;">The step 15 will go back the files to the state before your changes (original files) and the Step 17 return your changes (changed files).</p>

<p><center>
  <img src="/img/infra/git/revert.png" />
</center></p>

<p><em> If you want to throw away all uncommitted changes in your working directory, you should see <a href="https://git-scm.com/docs/git-reset">git-reset.</a></em></p>

{% highlight ruby %}
# 20 Reset your third commit
$git reset d75b40a --hard
# 21 See the log
$git log

# History in console
commit d75b40a8f1be78ba3abbb6d206ac82283ca9bc65 (HEAD -> master)
Author: Name Last  <example@example>
Date:   Mon Feb 21 10:01:18 2022 +0100

    Third Commit

commit 79fc79530ecf44809d0aaeb93830ec23a5254d66
Author: Name Last  <example@example>
Date:   Mon Feb 21 09:49:30 2022 +0100

    Second Commit

commit 20d9288c202376bc7230f1e08becfa60ac1d0f7c
Author: Name Last  <example@example>
Date:   Mon Feb 21 09:20:40 2022 +0100

    First Commit
{% endhighlight %}

<p style="text-align: justify;">The step 20 move the pointer the a specific position on the tree. You just need the first seven first number of the commit's hash. Bellow is how is supposed to be the tee.</p>

<p><center>
  <img src="/img/infra/git/revert.png" />
</center></p>

<br />
<h2>Change the branch</h2>

<p style="text-align: justify;">Until now, all the works is happening using the master branch. Now, let's create a new one.</p>

{% highlight ruby %}
# 22 Create a new branch
$ git branch mynewbranch
# 23 Change the head to the new branch
$ git checkout mynewbranch
{% endhighlight ruby %}

<p><center>
  <img src="/img/infra/git/newbranch.png" />
</center></p>

<p>Let's create a new file to this branch.</p>

{% highlight ruby %}
# 24 Create a new file
$ touch newfile.txt
# 25 Adding to the stage area
$ git add newfile.txt
# 26 commit new file
$ git commit -m "Adding new file"
{% endhighlight ruby %}

<p><center>
  <img src="/img/infra/git/fourthcommit.png" />
</center></p>

<br />
<h2>Merge branches</h2>

<p>You need to be on your branch target. Here, we will merge from the newbranch to the master. So, checkout to the master and let's go.</p>

{% highlight ruby %}
# 27 checkout to target
$ git checkout master
# 28 merge from new branch
$ git merge mynewbranch
# 29 Console log
$ git log

#History in Console
commit 803023ed0a9f3d2fb9f6ce398e73e7e8cf95e1b2 (HEAD -> master, motivation)
Author: Name Last  <example@example>
Date:   Mon Feb 21 13:13:17 2022 +0100

    adding new file

commit d75b40a8f1be78ba3abbb6d206ac82283ca9bc65
Author: Name Last  <example@example>
Date:   Mon Feb 21 10:01:18 2022 +0100

    Third Commit

commit 79fc79530ecf44809d0aaeb93830ec23a5254d66
Author: Name Last  <example@example>
Date:   Mon Feb 21 09:49:30 2022 +0100

    Second Commit

commit 20d9288c202376bc7230f1e08becfa60ac1d0f7c
Author: Name Last  <example@example>
Date:   Mon Feb 21 09:20:40 2022 +0100

    First Commit

{% endhighlight ruby %}

<p>Here is the tree after the merge to master.</p>

<p><center>
  <img src="/img/infra/git/merge.png" />
</center></p>

<p>If you want to remove the branch you just need use the attribute 'd'. And here is the tree after that.</p>

<p><center>
  <img src="/img/infra/git/deletebranch.png" />
</center></p>

<p style="text-align: justify;">The first example show the case where the new branch has everything the master. The image below show another example where the master has a new commit and the other branch also has different commits. </p>

<p><center>
  <img src="/img/infra/git/merge2.png" />
</center></p>

<p style="text-align: justify;">In case happen changes in the same file in both branches the console will the the conflict's message. You just need to open your file, fix that and commit again. The <b>git diff</b> show in the console all the changes in the files.</p>

<h2>Working with Remote Repositories</h2>

<p style="text-align: justify;">When you create the repository remotely the GitHub show you all the directions to synchronize it with a local repository. You just need follow it. For example used in this post you should follow the second option. </p>

<p><center>
  <img src="/img/infra/git/remoteguide.png" width="70%" height="70%"/>
</center></p>

<p style="text-align: justify;">However, if you have more then one branches and want push all of them you can use <b>git push --all origin</b>. In case you want let the master branch default you can write <b>git push -u origin master</b> and the last time you just need to write <b>git push</b>. </p>

Other case is when exist the project in the remote repository and you want just use it. For that you have to clone the repository.

{% highlight ruby %}
# 30 Clone the repository - copy the url from git repository
$ git clone https://github.com/fabiana2611/api-java.git
# 31 Downloads the changes from remote before push your changes
$ git pull
# 32 Upload your changes to remote
$ git push
{% endhighlight ruby %}

<p style="text-align: justify;">Before the <b>pull</b>, you can use <b>stash</b> to store locally the changes you are not prepared to commit yet. And put back the code using <b>git stash pop</b>. If you want do a clean commit you can use <a href="https://www.git-tower.com/learn/git/faq/git-squash">git squash</a>.</p>

<p style="text-align: justify;">Probably will be necessary configure the key ssh to use the remote repository. One possibility is you have to <a href="https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent">generate new SSH key</a> locally and copy in the github repository. Other case you can create in your repository (Settings/Developer Settings/Personal access tokens) and copy locally when try to be logged. </p>


<h2>Example of the Tree</h2>

<p>Here are the steps regarding an example of using remote repository. Below you will see commits, merges and push to remote repository. Pay attention: The HEAD in remote repository is changed only after the merger.</p>

<p>
  <center>
    <img src="/img/infra/git/stepsremote1.png" width="100%" height="100%"/>
    <img src="/img/infra/git/stepsremote2.png" width="100%" height="100%"/>
  </center>
</p>

<h2>Reference</h2>

<ul>
  <li>Git-school.github.io/visualizing-git/#free</li>
  <li>Udemy: Learn Git by Doing: A step-by-step guide to version control (Codingdojo, Inc)</li>
  <li>Video Fabia Akita: https://youtu.be/6Czd1Yetaac</li>
</ul>
