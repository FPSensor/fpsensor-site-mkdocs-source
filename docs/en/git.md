# Git/Github/Gitlab guide

this guide will help u to start with git and some commands.    
its basic so dont pretend that u will be expert after this.    
u should have a git account of a git site ofc.    
u should had installed git already    

## initialize my first repo
new repo    

```
mkdir repo
cd repo
git init
```

## who are you?

with the information u provided to create a account u have to fil this    

```
git config --global user.name
git config --global user.email
```

## Doing our first change

```
git branch -M master
touch hi
echo 1 > hi
git add hi
git commit -m "first hi public release"
```

## pushing to our repo

in our github we should make a repository with the name we want to add to it    
i want to clarify that i use github cuz its the more common but its the same for all    

```
git remote add origin https://github.com/FPSensor/hi
git push -f -u origin HEAD:master
```

## first chaper is done, some things to clarify

1: we want u to be explicit with the commits, whats modified, with file, which section of the repo, anything, even in the description u should said why u did what    

2: no need to put -m on the git commit command, if u dont add -m it will open the editor, this is better for long commit messages.    

3: that larger push command is only for new branches, should be another way but if u clone the repo again a "git push" is enough    

## clone a repo

as simple as "git clone link -b branch Descargas/hola"    

## who did this?

i took a commit from another guy, how to recognize his work?    
in android comunity we dont want people that doesnt add authors to commits and u will be like trash for they (i say by previous experiences) so,    
we should add who did that.    
this will be applied for the previous commit, i will tell us how to do for others more later.    

```
git commit --amend --author="FPSensor <gkartyt@gmail.com>"
```

but, how we got that info    
i took a commit from a repo where i was looking, how we can get that?    
in the commit link add .patch    
this will literally make the commit a patch file, something that we will talk later about, but the point is:     
we can use it to get the author, check it.    

## i want a cherry
a cherry pick is literally wen you pick commits from another repo     
to do it is really simple    
we have to initialize the repository where the commit is and its changes with their commit hashes:    

```
git remote add cherrypick https://github.com/FPSensor/FPSensor
git fetch cherrypick
git cherry-pick hfwdhuwhfuiwuihfvuiwfhefhruifhfuihiuwe
```

u can just copy the hash from the commit    
i have to pick 300 commits, how?    
things to have in account?     
its a start commit and a end commit, everything after the first commit and before the final commit will be picked, no metter what it is     

```
git cherry-pick commit-start~..commit-end
```

oh, no    
we got a conflict of context at hi file    

how we look into it?     
a git conflict its where git dont know what to do cuz your source and the source of the repo before that commit are different    
its really simple    

```
<<<<<<< HEAD
======= that source with the commit applied (should appear as a hash of commit)
>>>>>>> end of the confflict
```

we dont want to apply a commit cuz tons of confflicts and u are lazy?

```
git cherry-pick --ship
```

## to be continued
