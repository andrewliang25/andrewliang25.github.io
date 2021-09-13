---
title: TFVC vs Git - Which version control system should I choose?
tags:
---

## Prologue
"Git is the default version control provider for new projects. You should use Git for version control in your projects unless you have a specific need for centralized version control features in TFVC." --from Microsoft TFS documentation.

<!-- more -->

## What is TFVC?
Team Foundation Version Control (TFVC) is a centralized version control system. Typically, team members have only one version of each file on their dev machines. Historical data is maintained only on the server. Branches are path-based and created on the server.

TFVC has two workflow models:

- Server workspaces - Before making changes, team members publicly check out files. Most operations require developers to be connected to the server. This system facilitates locking workflows. Other systems that work this way include Visual Source Safe, Perforce, and CVS. With server workspaces, you can scale up to very large codebases with millions of files per branch and large binary files.

- Local workspaces - Each team member takes a copy of the latest version of the codebase with them and works offline as needed. Developers check in their changes and resolve conflicts as necessary. Another system that works this way is Subversion.

## What is Git?
Git is a distributed version control system. Each developer has a copy of the source repository on their dev machine. Developers can commit each set of changes on their dev machine and perform version control operations such as history and compare without a network connection. Branches are lightweight. When you need to switch contexts, you can create a private local branch. You can quickly switch from one branch to another to pivot among different variations of your codebase. Later, you can merge, publish, or dispose of the branch.

## Benefits of Using Git

## Benefits of TFVC

## Conclusion
Since Git is more popular and powerful than TFVC, I suggest new projects to use Git instead of TFVC. Should old projects using TFVC move to Git? It depends on needs to the benefits of Git, otherwise it will just increase learning cost and pain for the team, and even worse, mess up the workflow and confuse team members.

> Reference
> https://docs.microsoft.com/en-us/azure/devops/repos/tfvc/comparison-git-tfvc?view=azure-devops
> https://simpleprogrammer.com/git-vs-tfvc/
> https://blog.darkthread.net/blog/tfvc-vs-git/