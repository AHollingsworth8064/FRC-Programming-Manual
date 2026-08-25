When working on code by yourself, keeping track of your code isn't that hard. You make some changes, save the file and move. 

But what would happen if you were working in a group on the same project? What if two people made two different changes, or something broke and you need to revert back to an older version of code? On top of that, how are you supposed to transfer changes from on computer to another?

 Well this is where git comes in. 

[Here is the link to download git](https://git-scm.com/install/)
## What is git

Git is a tool that keeps track of the changes to a project. This let's us save version of our code and  see what has changed. But how does Git keep track of changes? To understand this, we first must start with repositories, or repos for short.   

An **repository** is something that stores the current version of your code, and all past saved changes. They can live locally on your computer, or on a server. I personally recommend keeping a remote copy on a server, and thanks to **GitHub**, it's relatively easily to do so. 

**GitHub** is a cloud based platform that allows users to store their repos. It allows you to access and update your repos across different devices at anytime. But first you have to make a GitHub account ([here is the link](@todo)). Once you made an account, I would advise you to read [this](https://docs.github.com/en/get-started/using-github/hello-world) since it shows you how to make repos. 

Once you have a repo, you need to a way to get it onto your computer. To do this, we do something called **cloning**. Cloning is when we make a copy of the repo on our own computer.

>[!info]- Cloning Using Terminal 
>If you want to use Terminal to make a clone, first learn the basics of navigating terminal.
>[Here is a link for navigating terminal within windows]([https://learn.microsoft.com/en-us/windows/terminal/](https://www.bitecode.dev/p/ultra-beginners-first-steps-for-the)). 
>
>Once you know how to the basics for navigating terminal, I heavily recommend making a folder to hold all of your different code project moving forward. You can either do this in file explorer or with the `mkdir` command.  
>
>After navigating to where you want the repo to live, copy the link to the repo you want to clone. Then type `git clone` into the terminal followed by the link to the repo. It should look something like this
>```
> git clone https://github.com/FRC3636/frc-2026
>```

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