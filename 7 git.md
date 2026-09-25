When working on code by yourself, keeping track of your code isn't that hard. You make some changes, save the file and move. 

But what would happen if you were working in a group on the same project? What if two people made two different changes, or something broke and you need to revert back to an older version of code? On top of that, how are you supposed to transfer changes from on computer to another?

 Well this is where git comes in. 

[Here is the link to download git](https://git-scm.com/install/)
## What is git

Git is a tool that keeps track of the changes to a project. This let's us save version of our code and  see what has changed. But how does Git keep track of changes? To understand this, we first must start with repositories, or repos for short.   

An **repository** is something that stores the current version of your code, and all past saved changes. They can live locally on your computer, or on a server. I personally recommend keeping a remote copy on a server, and thanks to **GitHub**, it's relatively easily to do so. 

**GitHub** is a cloud based platform that allows users to store their repos. It allows you to access and update your repos across different devices at anytime. But first you have to make a GitHub account ([here is the link](@todo)). Once you made an account, I would advise you to read [this](https://docs.github.com/en/get-started/using-github/hello-world) since it shows you how to make repos. Importantly, GitHub is an entirely separate organization as Git. Git is a free, open source software project, whereas GitHub is a closed-source, for-profit subsidiary of Microsoft.

You can choose to use Git from either the terminal or from IntelliJ. IntelliJ is more intuitive, but learning to use the terminal is a valuable skill that will be useful in virtually any software development environment. This page will be split up into two sections: Using Git from IntelliJ, and using Git from the terminal.
## Using Git from the terminal

### Cloning

Once you have a repository on GitHub, you need to a way to get it onto your computer. To do this, we do something called **cloning**. Cloning is when we make a copy of the repo on our own computer.

If you want to use Terminal to clone a repository, first learn the basics of navigating terminal.
[Here is a link for navigating terminal within windows]([https://learn.microsoft.com/en-us/windows/terminal/](https://www.bitecode.dev/p/ultra-beginners-first-steps-for-the)). 

Once you know how to the basics for navigating terminal, I heavily recommend making a folder to hold all of your different code project moving forward. You can either do this in file explorer or with the `mkdir` command.  

After navigating to where you want the repo to live, copy the link to the repo you want to clone. Then type `git clone` into the terminal followed by the link to the repo. It should look something like this:

```
git clone https://github.com/FRC3636/frc-2026
```

This will *clone* the repository into the working directory. In this case a new folder will be created called `frc-2026`. You can list everything inside the working directory by using the `ls` command and hitting enter (`ls` is short for list). Some of the things listed will be files and some will be folders. Hopefully, the repository's name will be listed. 

You can then move into that folder using the `cd` command, which changes the working directory of the terminal. It stands for "change directory".

```
cd frc-2026
```

All Git commands are going to look similar to this. You first write `git` to tell the terminal to use Git, then the subcommand (what you want Git to do) and then the arguments (in this case a link to the repository you want to clone). 

After this step, you can go ahead and make any changes you want to the repository. Note that these changes will only be made on your local computer, and not automatically synced to GitHub. The rest of this chapter will focus on both *pushing* your changes back to GitHub, and *pulling* changes other people have pushed to GitHub.

### `add`-ing (staging)

When you make changes, at first even Git doesn't know about them. To let Git know about any changes you've made, you can use `git add ...`, replacing the `...` with the path to the file that you've changed. For example, if I have this setup:

```
frc-2026
  | code
  |   | package
  |   |   | file.java (changed)
  |  README (created)
```

In this example, one file has been changed and one file has been created. Assuming the working directory of the terminal is `frc-2026`, we can add the files like so:

```
git add code/package/file.java
git add README
```

Adding a bunch of files in this way can be tedious, and most of the time we want to let Git know about every change we've made in the repository. In that case, you can use this command:

```
git add -A
```

### `commit`-ing 

Once your changes are staged, you can use the `commit` subcommand. A repository is made up a chain of commits going back all the way to the first commit. When you commit, you add to that chain. The reason staging and committing are separated is because you can stage multiple times before you commit, giving you control over what exactly goes into the commit history. 

A Git commit looks like this:

```
git commit -m "Add climber subsystem."
```

The `-m` argument stands for "message". After it, in quotes, you write a short summary of the changes you made. In general, commit messages follow a specific grammar pattern. Here are some examples of messages that don't follow this pattern:

- "I add the climber subsystem".
- "Added the climber subsystem."

But most people don't really care about this, so give it no more thought.

Committing is the first place you might see a problem, if you've done something wrong. It's hard to document all these such cases, so if you do encounter one you should ask someone about how to fix it. Make sure to always check that the commit operation (and every command you run for that matter), executed successfully, because if you try to run more commands in a broken state you will probably just end up making everything even more broken.

### `pull`-ing

Before you push all your changes to GitHub, you have to grab the changes other people have pushed to GitHub. Pulling is perhaps the most powerful, but also the most devastating feature of Git. To pull, simply type `git pull`, hit enter, and say a prayer to whatever deity you have faith in. 

Everything is probably going to be okay, but if you see the word `CONFLICT` on any of the lines, you're in trouble. 

After you do pull successfully and fix all the conflicts, test the code again to make sure it works properly. In most cases it does, but sometimes other people's changes can mess up your changes. 
### `push`-ing

At long last, you can push your changes to GitHub. Simply type `git push` and hit enter. You have now learned 90% of the Git process. Now, you can begin learning the final 90% of the Git process.

### `branch`-ing

So far, we have thought of the Git history as a single chain of commits. In reality, the history can be much more complicated. Any commit can be branched off into two separate "branches", and any commit can be formed as the merger of two branches.  Here is an image that will help you visualize branches:

![[Pasted image 20260925114044.png]]

IntelliJ makes it very convenient to switch between branches, so we'll focus more on how branches work than on making and switching between them. 

Every repository has a base branch, from which all other branches sprout. What your base branch is called can say a lot about you:

- Main: You are an NPC and just like everyone else.
- Master: You are afraid of being woke, but also still an NPC.
- Trunk: You are cool, understand git, and probably have facial hair the size of Karl Marx.
## Using Git from IntelliJ

Once you have a repository on GitHub, you need to a way to get it onto your computer. To do this, we do something called **cloning**. Cloning is when we make a copy of the repo on our own computer.

>[!info]- Cloning In IntelliJ
>@todo make a gif 

Once you have it cloned, you can start editing the code in what ever IDE you want. Once you want to save you changes to remote repo (the one stored in GitHub), you need to **stage** the changes. This is just telling git that you want the changes made to these files to be included when you commit.

>[!info]- Staging Changes Using Terminal
>I personally recommend using your IDE's built in git tools since they tend to be simpler to use. However, if you really want to use terminal, I'll link resources for each step of this process.
> 
 [Staging Changes](https://www.geeksforgeeks.org/git/staging-in-git/)

>[!info]- Staging Changes Using IntelliJ 
>Stage changes with IntelliJ is really easly
>@todo add gif

Once the changes have been staged, the next step is to **commit**. Although it's name might seem intimidating, it just mean you're saving the changes in the local repo. 
 

>[!info]- Commit Using Terminal
>[Commiting](https://www.w3schools.com/git/git_commit.asp)

>[!info]- Commit Using IntelliJ
>@todo

One important part of a committing is writing the commit message. Since it is meant to tell other, and possibly your future self, what changed. Since, without it, people would have to manual look through the changes. 

Anyways, once you committed something, the changes are only saved locally.  To save the changes to the remote repo, you must **push** the changes. 

>[!info]- Pushing Using Terminal
>[Pushing](https://docs.github.com/en/get-started/using-git/pushing-commits-to-a-remote-repository)

>[!info]- Pushing Using IntelliJ
>@todo

Once you push changes, the remote repo will update.. To get these new changes, we do something called **pulling**. This process download the committed changes from the remote repo onto your current local repo. 

>[!info]- Pulling Using Terminal
>[Pulling](https://www.w3schools.com/git/git_pull_from_remote.asp?remote=github)

>[!info]- Pulling Using IntelliJ
>@todo

But what do you think would happen if two people who changed the same file pushed their changes? Usually git will automatically handle it, but if both commits have contradicting elements - such as one commit deleted something, while the other kept that thing -, then a merge conflict will happen.  This means you have to manually go through the changes and decide what to keep. To help avoid this headache, we use something called **branches**. 

**Branches** are independent workspaces. If you think of  `main`  as the main save file. Then a branches are like separate save files where you try out new things without impacting your main save. This means, we can  edit, change, commit, etc. branches  without impacting the `main` branch. 

>[!info]- Branches Using Terminal
>[Branches](https://www.w3schools.com/git/git_branch.asp?remote=github)

>[!info]- Branches with IntelliJ
>@todo

%%
1) what and why we use git 
	1) Wokring with group similtalicy = hard
2) repos 
	1) Where projects are held
3) clones
	1) Geting a repo 
4) commit and push
	1) IDK 
	2) State in dropdown 
	3)
5) pull 
6) branches
7) pull requests