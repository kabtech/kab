---
layout: kab
group: ccc
title: Git BASH
---
### Git BASH

Notes for version control with Git

```
#create local branch
#check in to local branch
git add src (specified a folder name)
#to check status afer add:
git status 
git commit -m "comment about what you are committing"
#recommend this immediately upon creating branch:
git push --set-upstream origin kab_minor_gui_refinements
#should do every morning:
git pull origin master 
-- here is where you would reconcile conflicts if any --
git push

#when at dev milestone, do local commit and push up to master

```

<br/>
<br/>
