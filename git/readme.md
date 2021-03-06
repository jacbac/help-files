Git config
----------

```
git config --global user.name "Your Name"
git config --global user.email name@email.com

# show all untracked files in parent directories and not only the untrackend directories
git config --global status.showUntrackedFiles all
```

Git tools
---------

### Gitk

Gitk useful options:

```
--all : Show all branches
--date-order : Order commits and changes by date
& : Open gitk as a separate process
```

So we can open gitk as a independent process:

```
gitk --all &
or
gitk --all --date-order &
```

And personalize gitk. Gitk creates the `.gitk` file in your $HOME directory to store preferences such as display options, font, and colors like. We can edit it:

```
set mainfont {Helvetica 9}
set textfont {Courier 9}
set uifont {Helvetica 9 bold}
etc.
```

Git workflow
------------

* [Vincent Driessen famous git workflow (EN, 2010)](http://nvie.com/posts/a-successful-git-branching-model/)
* [Vincent Driessen git workflow in french by occitech (FR, 2014)](http://www.occitech.fr/blog/2014/12/un-modele-de-branches-git-efficace/)
* [Marvinlabs git workflow cheatsheet (EN, 2013)](http://www.marvinlabs.com/2013/06/18/our-git-workflow-cheatsheet/)
* [Sogilis rebase workflow (FR, 2014)](http://blog.sogilis.com/post/104148375576/notre-workflow-git-pourquoi-comment)
* [Various example workflow (EN, 2014)](http://blog.endpoint.com/2014/05/git-workflows-that-work.html)
* [J-P Fleury simple workflow (FR, ?)](http://www.jpfleury.net/tutoriels/gestion-projet-git.php)
* [AOE single branch git workflow (EN, 2014)](http://fbrnc.net/blog/2014/12/keeping-it-simple-git-workflow)
* [Gitready pull rebase technique (EN, 2009)](http://gitready.com/advanced/2009/02/11/pull-with-rebase.html)
* [Herve Guetin Agile Flow (FR, 2014)](http://www.herveguetin.com/magento/agile-flow.html)
* [William Durand branching model (EN, 2012)](http://williamdurand.fr/2012/01/17/my-git-branching-model/)

Git useful commands
-------------------

* [30 git helper options (FR, 2014)](http://www.git-attitude.fr/2014/09/15/30-options-git-qui-gagnent-a-etre-connues)
* [Merge and rebase (FR, 2014)](http://www.git-attitude.fr/2014/05/04/bien-utiliser-git-merge-et-rebase/)
* [Rebasing by Ry (EN](http://rypress.com/tutorials/git/rebasing)

Supprime le fichier du système de suivi de version mais le préserve localement
```
git rm --cached
```

Informe une branche locale de suivre par défaut une branche spécifique sur le dépôt
```
git push -u <remote-name> <branch-name>
OU
git branch --set-upstream <local_branch> origin/<repo_branch>
```

```
git rebase -i
```

* pick
* edit
* reword
* squash

Delete a remote branch
```
git push origin --delete <branchName>
```

Associer un message à un stash
```
git stash save "your message here"
```

Supprimer tous les stash précédemment enregistrés
```
git stash clear
```

Git tutorials
-------------

* [Ry's Git tutorial (EN)](http://rypress.com/tutorials/git/index)
