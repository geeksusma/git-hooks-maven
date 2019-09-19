# git-hooks-maven
[Git hooks](https://git-scm.com/book/uz/v2/Customizing-Git-Git-Hooks) are an interesting way to automatize some tasks or checks, like executing actions after merging a branch, or before committing or pushing changes and so on.

Git brings by default their own hooks, and they are placed in a hidden folder .git/hooks if you want to use them, just remove the ".sample" extension and rewrite them to make those scripts fulfill your requirements.

But the problem is the next, maybe those hooks are not enough for you (for example, there is no post-merge script) and even worse, because they are not in a visible folder, they can't be shared (imagine you're coding in a team) with others.

Now the thing is, the hooks are not executed in server side, they are scripts which run at client side, locally.

This project contains, under the git-hooks folder, a set of hooks that they might be interesting for you.

## Pre-requisites

The hooks are just bash files, so they will only works for Unix/Linux/Mac (they were written using a MacBook Pro)
The post-merge were designed for [Maven](https://www.apache.org/) projects, so they will look for a pom.xml in order to create tags or to upgrade versions. The pom added to this project is just for if you want to play with the hook before moving it to your project.

## hooks:

* post-merge:
***
This hook will be fired when a merge is executed locally. But detecting if you are only in a master branch, then it will allow to you to fire the next actions:
* It will replace the SNAPSHOT suffix by RELEASE in a pom.file, assuming you're declaring your project-version at the top of the file before declaring dependencies, and you're not badly using SNAPSHOT's as dependencies
* It will commit and push a generic message 'upgrading to next release' in master
* It will take the version from the pom.xml, and it will create and push a tag like 'vX.X.X-RELEASE' with a default message

Those steps were steps I had to do it manually when:
 * I deploy a new artifact on my nexus repository
 * Or when I deploy a new release of a web-app in live
 * Or when I push a new release of a docker image
 * ... in fact, when something is marked "to be used"
 
If you have a CI/CD (for example with Jenkins) you can automatize those steps just ensuring you add a merge from your development branch to master.

***
* More hooks soon :)
***

## usage:

Just add the git-hooks folder to your project at root level. And then execute the "init-hooks.sh" script to ensure the hooks have execution permissions
````
-rwxr-xr-x  1 geeksusma  staff  724 19 sep 10:24 post-merge
````
