---
layout: post
title:  "Git Rebase - Where is the trick point?"
date:   2022-03-03
categories: infra
permalink: /:categories/git-rebase
---

<p style="text-align: justify;">It is a subject I'd like to put on the table because of some attentions points we have to have in our minds.</p>

<p style="text-align: justify;">The <a href="https://docs.github.com/es/get-started/using-git/about-git-rebase" >Git page</a> gives the definition: <em>The git rebase command allows you to easily change a series of commits, modifying the history of your repository.[1]</em></p>

<p style="text-align: justify;">That part is ok. I believe all of us is aware about that. My concerns is the WARNING after the definition:</p>

<p><em>Warning: Because changing your commit history can make things difficult for everyone else using the repository... It's considered bad practice to rebase commits when you've already pushed to a repository. </em></p>

<p style="text-align: justify;">The alert brings up the risk to lose code. It is a painful part in the developers work.</p>

<p style="text-align: justify;">The fundamental Git workflow use the merge command which brings your work from some feature branch to your target branch. The image below illustrates a merge command. Note that there is a last commit regarding the merge.</p>

<p><center>
  <img src="/img/infra/git/merge3.png"/>
</center></p>

<p style="text-align: justify;">The merges preserves the entire history of your repository (even the chronological order). It makes the merges a traceable command. However, they can make a mess on the tree and can be painful to review because of a lot of irrelevant commits. It is one reason to use the rebase. It makes the tree cleaner and reviewer-friendly.</p>

<p style="text-align: justify;"><em>Rebasing changes where you started your branch. The whole branch is lifted up, and transported to the end of the current master branch, where it connects to the end. The master branch is left untouched, and is free to continue receiving commits. The commits aren’t actually moved, however, since commits are immutable. Rather, they’re copied, which results in new commit IDs. The previous commits are left stranded, hiding in your Git files but never to be seen again, since the playhead has moved somewhere else.</em>[3]</p>

<p style="text-align: justify;">In other words, the rebase identify the base of the feature branch and commit again all the commits after the last commit in your main branch (eg. master).</p>

<p><center>
  <img src="/img/infra/git/rebase1.png"/>
</center></p>

<p style="text-align: justify;"><em>When you run <b>git rebase</b>, Git takes each commit in the branch and moves them, one-by-one, onto the new base. If any of these commits alter the same line(s) of code as the upstream commits, it will result in a conflict. The <b>git merge</b> command lets you resolve all of the branch's conflicts at the end of the merge. In rebase, the process will stop the rebase procedure and display a warning.</em>[2] </p>

<p style="text-align: justify;">After solve the conflicts you just need continue the process (<b>git rebase --continue</b>). The rebase can be done in an iterative way, selecting which commit you want. It's a way to have a clean commit.</p>


<h2>The Trick</h2>

<p style="text-align: justify;">As we saw in the definition, the rebase command changes the original base commit of a branch. It makes the new commits in the target branch without no context of where those commits come from. </p>

<p style="text-align: justify;">The rebase will not delete the commits or reposition them. The rebase will rewritten the history. Here is the trick: the risk to lose code when you are working with other developers because they are using a part of the tree not used anymore. It seems the code was deleted, but it's just the main part of the tree that was changed. For sure you can rescue the commit, but it's a hard work to do.</p>

<p style="text-align: justify;">The image shows an example where we can fall into a trap. It has a feature branch created from master. The branches and commits are a mirror of remote repository. Then is done a rebase locally and a push. You can see the feature branch is there yet.</p>

<p><center>
  <img src="/img/infra/git/rebase2.png"/>
</center></p>

<p style="text-align: justify;">Now the next image show an example where the tree can be a messy even using the rebase. The example use a shared feature branch, do a rebase locally and push it. In this case, the rebase was possible doing a pull first (implicit merge). The example do commit in master, rebase again and push.</p>

<p><center>
  <img src="/img/infra/git/rebase3.png" />
</center></p>


<h2>Use or not to use? That's the question</h2>

<p style="text-align: justify;">The rebase create new commits and let the old parts lost in the limbo. It is the issue if you are sharing the work with other developers. The others can use that tree in the limbo. So, how to decide?</p>

<ul>
  <li>Avoid use rebase in public branches unless you are sure that anyone is working on that branch.</li>
  <li>You can use rebase to a local cleanup and commit only what is necessary</li>
  <li>You can rebase onto a remote branch instead of master to help your collaboration with another developer and incorporate their changes into your repository.</li>
  <li>Avoid rebase shared branches</li>
  <li>Prioritize rebase locally</li>
  <li>Verify the priority of the work: simplicity (rebase) or traceability (merge). Pay attention rebase requires more work when dealing with conflicts</li>
  <li>Verify if you are in a big project and if everyone knows how to use it in the right way.</li>
</ul>

<h2>Conclusion</h2>

<p style="text-align: justify;">The rebase is an excellent resource to work with. However, it requires attention at some points to avoid unnecessary headaches. The decision should be made based on the type of collaboration with other developers and the level of expertise.</p>

<h2>Reference</h2>

<ul>
  <li>[1] <a href="https://docs.github.com/es/get-started/using-git/about-git-rebase">About Git Rebase</a></li>
  <li>[2] <a href="https://code.tutsplus.com/tutorials/rewriting-history-with-git-rebase--cms-23191">Rewriting History with Git Rebase</a></li>
  <li>[3] <a href="https://en.buradabiliyorum.com/what-is-git-rebase-and-how-is-it-different-than-merging-cloudsavvy-it/">#What is Git Rebase and How Is it Different than Merging? – CloudSavvy IT</a></li>
  <li>[4] <a href="https://towardsdatascience.com/the-differences-between-rebase-and-merge-30c91cd18f30">The Differences between Rebase and Merge</a></li>
  <li>[5] <a href="https://medium.com/pranayaggarwal25/git-merge-rebase-d8b91825bbb1">Git merge vs Git Rebase</a></li>
  <li>[6] <a href="https://dzone.com/articles/git-merge-vs-rebase">Git Merge vs. Rebase</a></li>
  <li>[7] <a href="https://www.atlassian.com/git/articles/git-team-workflows-merge-or-rebase">Git team workflows: merge or rebase?</a></li>
  <li>[8] <a href="https://git-scm.com/book/en/v2/Git-Branching-Rebasing">3.6 Git Branching - Rebasing</a></li>
  <li>[9] <a href="https://git.logikum.hu/tutorials/merge-rebase/golden-rule">The golden rule of rebasing</a></li>
</ul>
