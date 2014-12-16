Git config
----------

```
git config --global user.name "Your Name"
git config --global user.email name@email.com
```

Git tools
---------

Open gitk as a independent process:

```
gitk --all &
or
gitk --all --date-order &
```

Gitk useful options:

```
--all : Show all branches
--date-order : Order commits and changes by date
& : Open gitk as a separate process
```

Gitk creates the `.gitk` file in your $HOME directory to store preferences such as display options, font, and colors like:

```
set mainfont {Helvetica 9}
set textfont {Courier 9}
set uifont {Helvetica 9 bold}
etc.
```

Git workflow
------------

* [Vincent Driessen famous git workflow (EN, 2010)](http://nvie.com/posts/a-successful-git-branching-model/)
* [Marvinlabs git workflow cheatsheet (EN, 2013)](http://www.marvinlabs.com/2013/06/18/our-git-workflow-cheatsheet/)
* [Sogilis severe rebase workflow (FR, 2014)](http://blog.sogilis.com/post/104148375576/notre-workflow-git-pourquoi-comment)
* []()

Git useful commands
-------------------

Supprime le fichier du système de suivi de version mais le préserve localement
```
git rm cached
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

pick
edit
reword
squash
