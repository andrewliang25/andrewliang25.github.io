---
title: TFVC vs Git - Which version control system should I choose?
date: 2021-09-17 13:30:44
tags:
---


## Prologue

Initially, TFS supported only TFVC, and support for Git as a source code repository was added later in TFS 2013. Also, Microsoft suggest user to use Git: "Git is the default version control provider for new projects. You should use Git for version control in your projects unless you have a specific need for centralized version control features in TFVC."

<!-- more -->

## What is TFVC?

Team Foundation Version Control (TFVC) is a centralized version control system. Typically, team members have only one version of each file on their dev machines. Historical data is maintained only on the server. Branches are path-based and created on the server.

TFVC has two workflow models:

- Server workspaces - Before making changes, team members publicly check out files. Most operations require developers to be connected to the server. This system facilitates locking workflows. Other systems that work this way include Visual Source Safe, Perforce, and CVS. With server workspaces, you can scale up to very large codebases with millions of files per branch and large binary files.

- Local workspaces - Each team member takes a copy of the latest version of the codebase with them and works offline as needed. Developers check in their changes and resolve conflicts as necessary. Another system that works this way is Subversion.

## What is Git?

Git is a distributed version control system. Each developer has a copy of the source repository on their dev machine. Developers can commit each set of changes on their dev machine and perform version control operations such as history and compare without a network connection. Branches are lightweight. When you need to switch contexts, you can create a private local branch. You can quickly switch from one branch to another to pivot among different variations of your codebase. Later, you can merge, publish, or dispose of the branch.

## Benefits of Using Git

+ Creating new branches in Git is very cheap.
TFVC creates branch by coping whole project while Git almost does nothing cause Git using bit difference to record changes. So what Git does is just take a note that this node has two path below.

+ Better workflow management
Since it is cheap to creat branches in Git. We can use branches to seperate different environment. Such as dev, test, prod, feature, hotfix. And connect these branches by pull requests. For more deeper explanation, search for "Git Flow".

+ Developers have a full version history on local. No need to connect server to compare changes and view history. Despite the advantage of working offline, there is no server response time while manipulating version control system.

+ You can trim the messy branch on local and then sync to server with clean history. And if any issue accurs, just downgrade version. It does not affect anyone since it is all on local. Whithout the concern, it is more freely to make changes on commits history.

+ Git skills is more valueable than TFVC since Git is a standard version control system in most industry. If you have chance to switch team or company, Git skills can get you more points.

## Benefits of TFVC

+ No learning cost for developers who have been using TFVC for years. But there is risks of drifting away from morden techniques since more and more projects using Git as version control system.

+ Centralized system has more clear and simple control logic, GUIs are easy to use. Compare to Git, Git is a distributed system which has more complex commands that makes GUIs are not able to cover all situations. Command line is needed, which is not as friendly as TFVC.

+ Fewer merge conflicts happen in TFVC. Git is a distributed system. Developing independently and branching makes pull requests and merge conflicts. Which increases code quality but also more management.

## Conclusion

Since Git is more popular and powerful than TFVC, I suggest new projects to use Git instead of TFVC.
However, there is a lot of projects created before TFS supporting Git. Should they move from TFVC to Git? It depends on needs to the benefits of Git, otherwise it will just increase learning cost and pain for the team, and even worse, mess up the workflow and confuse team members.

# Reference

> https://docs.microsoft.com/en-us/azure/devops/repos/tfvc/comparison-git-tfvc?view=azure-devops
> https://simpleprogrammer.com/git-vs-tfvc/
> https://blog.darkthread.net/blog/tfvc-vs-git/