---
title: 'Practical Git for the Unintiated'
description: 'Pratical Git'
pubDate: 'Nov 20 2023'
heroImage: '/practical-git.png'
---

<p>Part 2 in our series on breaking into software engineering. In this episode, we will talk about Git arguably one of the most important
technologies that developers leverage daily. In my post on how to get into SWE I mentioned Git, and you will probably find it 
on many other people's lists, but Git has a lot of features and it can be daunting to look at something like Git and figure out 
how much you should know when getting started. This article will cover what Git is, why we use it, and which of its uses should 
you be competent with to meet people's expectations. As with all my articles, this is just my opinion of what you should know and 
what I commonly use.</p>
<h2>What is Git?</h2>
<p>
Git is a version control system used for tracking changes, versions, etc. It can be used to allow many developers to work 
on the same code simultaneously while allowing for conflict resolution, rollbacks, and diverting streams of work.</p>
<p>Git, or something similar (looking at you Google), is used by pretty much every company under the sun. I will go out on a limb 
and say that any company not using Git (barring some exceptions like Google) will likely not be a great place to work. We can talk
more about that somewhere else. My point is that Git is ubiquitous, you will need to know it, so why not get a head start?</p>
<h2>How to use Git</h2>
<p>I will not go through the installation of Git here, it is likely something like <br/><code>brew install git</code> depending on your 
machine, but you can find instructions online easily. I will break down the most basic git work-flow and what commands you should be 
familiar with.</p>
<h2>My workflow</h2>
<p>First I clone or create a repo, then I create a branch. I make some changes, commit them, create a pull request, merge changes into main.
 Then I will checkout main, pull the latest version, create a new branch, and work on a new feature. Along the way I will do some 
rebasing, look at the logs, check my status, view the diff, and a few other things I will detail below. </p>
<h4>Cloning</h4>
<p>Git allows you to store changes on some remote location, often Github or Gitlab, and clone that repository onto your local machine 
for development. To do this you will run the command <code>git clone &lt;url-of-your-repo&gt;</code> You will then have the repo on your 
machine and can begin coding.</p>
<h4>Pulling</h4>
<p>Your local version will not automatically sync with the remote, to get other changes which may have been pushed by 
someone else, you will have to pull the changes by running <code>git pull &lt;branch-name&gt;</code>. If you want to pull the 
newest version of main on remote you would say <code>git pull origin main</code> and if you simply want whatever your current branch 
is tracking (by default the remote version of itself) you would say <code>git pull</code>.</p>
<h4>Branches</h4>
<p>Git has a concept of branches. A branch represents a development path of your application. Your application will have a <code>main</code>
branch which should be your current, live, version of your application. When you want to add features, make changes or anything other 
than just view the code, you should create a branch and work on it. The 2 main ways I create branches are:
<ul>
    <li><code>git branch &lt;branch-name&gt;</code><br/><code>git checkout &lt;branch-name&gt;</code><br/>This will create a new branch 
        and then you will check it out (set it as your current branch)</li>
    <li><code>git checkout -b &lt;branch-name&gt;</code><br/>This will create and checkout your branch in one step</li>
</ul>
</p>
<h4>Commits</h4>
<p>In Git, sets of changes are referred to as "commits". Commits consist of a set of changes and a message. They can be referred to 
by a hash, which we will go into a bit later. To create a commit you will first make some changes, edit a file, create a file, etc. 
Once your changes have been made you have to "track" them. To see what changes you have made you can run <code>git status</code> to 
see the files changes and which are staged or unstaged. If you want to look at the actual differences between files you can run
<code>git diff</code> which will show all the changes you have made when compared to the remote. To track your changes you run 
<code>git add &lt;file-names&gt;</code> you can also run <code>git add .</code> to track everything, but be careful there...</p>
<p>Now that you have tracked changes you create a commit <code>git commit</code>. This will put all of the changes into one group 
which can be referred to later these changes are considered "staged". A window will pop up prompting you for a description for your commit, you can make this a bit faster 
by running <code>git commit -m "&lt;your commit message&gt;"</code> to provide your commit message when creating your commit.</p>
<h4>Pushing/Pull Requests</h4>
<p>To send your local changes to the remote, you will have to run <code>git push</code>, but there is some nuance here. Usually, 
you should never push to <code>main</code> (unless you are the only user of some small repo, but still it's not wise). Instead,
you should push to the remote version of you branch and then create what Github calls a "Pull Request" or what Gitlab calls a "Merge Request".
This is a document that says "Hey I want to merge my changes to main" and then someone will look at your changes and reject 
or accept them, at which point you can merge them into main to become the live version. To accomplish this you will run: <br/> 
<code>git push -u origin &lt;branch-name&gt;</code><br/> This will create a remote branch named &lt;branch-name&gt; and set up 
your local branch to follow it. It will then push your commits to that branch. You will then be prompted to create a Pull Request. 
From now on you will not have to specify which branch to push or pull from.</p>
<h4>Getting remote branches</h4>
<p>You might have to pull someone else's branch onto your machine. To do that you run <code>git fetch</code> followed by 
<code>git checkout &lt;branch-name&gt;</code></p>
<h4>Merging/Resolving conflicts</h4>
<p>Sometimes someone will push to your branch, but you have local changes. You can merge, which will try to resolve the conflicts and will 
then prompt you to solve them yourself, or you can <code>git pull --rebase</code> which will accept the remote changes as the current 
version and stick your changes on top of them. Often I choose to rebase, but when there are many complex changes it can be complicated 
and a merge might be easier.</p>
<h4>Walking through history</h4>
<p>Running <code>git log</code> will show you all of the commits in history, and you can jump between them with 
<code>git checkout &lt;commit-hash&gt;</code> This can allow you to revert changes or test different commits.</p>
<h4>Undoing</h4>
<p>If you want the remote version of a file you can run <code>git restore &lt;file-name&gt;</code>. To remove your working changes 
you can run <code>git reset --soft</code> to only remove unstaged changes, or <code>git reset --hard</code> to reset all tracked changes.</p>
<h4>Stash</h4>
<p>Jumping between branches will bring your unstaged changes with you and often complain, to get around this, and other potential issues 
you can stash your changes <code>git stash</code> to hop around or experiment, and when you want them back you can run <code>git stash pop</code></p>
<h4>Others</h4>
<p>There are some other commands I won't go into here which are worth learning on your own, later, they include:
<ul>
    <li><code>cherrypick</code></li>
    <li><code>bisect</code></li>
    <li>More complex versions of the commands we have mentioned.</li>
</ul>
</p>
<i>You now have the basics (and most of the important parts) of Git 😎</i>

