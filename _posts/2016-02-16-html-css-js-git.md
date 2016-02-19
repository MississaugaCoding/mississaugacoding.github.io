---
layout: post
title: "HTML/CSS/JS - Git & GitHub"
comments: true
publish: true
---

Git is a source code management tool used to keep track of changes to files in a project. Git is freely available as a download for Windows, Mac and Linux machines. Once installed, the `git` commands used are identical across all three platforms.

If for some reason you are unabe to download and install Git on your PC or laptop (for example, it's a work laptop), you can use an online IDE which has Git support built-in, such as Cloud9. Again, the `git` commands we will discuss here will be indentical.


### Starting with a local repository

`git init` 
- starting with a local repository; done only once, at the beginning

`git add --all`
- adds tracking for all files changes, i.e. adding new files as well removing exisiting ones
 
`git commit -m "some descriptive comment"`
- commits (to the repo) any changes made to the files being tracked

`git status`
- shows current status; especially useful to see if any changes have been made but have not yet been committed

`git log`
- shows a history of all commits; note each commit has a unique id. (SHA)

`git checkout` 
- recover a previous version of a file from the repo; e.g. deleted a file by mistake / deleted contents of file / made incorrect modifications
- use `git log` to figure out which commit (date, time) you wish to go back to; note SHA
- `git checkout [SHA] [filename]` gets an earlier committed version of that file


### Working with a remote repo on GitHub

We can just have a local repository and be able to keep track of all changes there. Sometimes, however, we need to go a step further and store our files in a remote repository. For example, for extra backup in case something happens to my laptop, or as a way to publicly showcase a project and make the code available to others. This is where something like GitHub comes in. 

Once you register on GitHub, you get an unlimited number of public repositories. 'Public' means anyone can see your files and copy them, but no one can change them directly.

1. create repo on GitHub
2. copy the repo URL, normally HTTPS, to clipboard
3. `git remote add [name e.g. origin] [paste repo URL from GitHub]` done only once to let local Git installation know about remote repository
4. `git push -u origin master` to push changes upstream to rempte repo (origin) from local (master); will prompt for GitHub username and password


To summarise, once local and remote repositories are set up, the only three `git` commands you will really use most of the time are:
`git add --all`
`git commit -m "some descriptive comment"`
`git push -u origin master`

## References &amp; Resources

- [Git Download & Docs](https://git-scm.com/)
- [Github](http://github.com)
- [Cloud9](http://c9.io)
- [Bitbucket](https://bitbucket.org)

