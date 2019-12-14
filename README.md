### Git commands practice

This is repository is another demonstration of how to use git.

>Level: Entry

```sh
$ git init
$ git remote add origin 'git@github.com:<UserName>/<project-name>.git'
$ touch index.html
$ echo '<html><head><title>Simple html file</title></head><body>Hello World</body></html>' > index.html
$ git status
$ git add index.html
$ git commit -m 'init html entry'
$ git push orign master
```

The above commands are used to:
 * initialize a project in local environment
 * set up origin to git repository
 * create file index.html
 * check git status (stages we are in)
 * add file to git track
 * commit file width flag -m to add commit message
 * push local file to remote master branch

---

Other commands that would be generally in use:

```sh
$ git checkout -b develop
$ touch style.css
$ vim style.css
$ vim index.html
$ git add .
$ git commit -m 'start to work with css'
$ git branch -a
$ git push --set-upstream origin develop
```

The above commands are used to:
 * create new branch 'develop' and switch to it
 * create css file
 * edit css file
 * edit html file to link the css
 * add new file and modified file to track
 * commit those changes
 * check all the branches in local and remote 
 * push to remote (use --set-upstream origin <branch-name> if there's no local branch name in remote)

---

 On github create pull request

 * base: master
 * compare: develop

 create pull request > merge pull request > delete branch develop

 Back to the local repository

 ```
 $ git checkout master
 $ git pull
 $ git branch -D develop
 $ git fetch --all --prune
 ```

 The above commands are used to:
 * switch to branch master
 * pull new codes from remote repository
 * delete local branch develop
 * keep sync with remote

---

 In the above, we mainly work on branch `master`, now we mainly work on branch `develop`, we only merge useful commits to `develop`

 ```
 $ git checkout -b develop
 $ git checkout -b feature/readme
 $ vim readme.md
 $ git commit -am "feature: update readme.md"
 $ git checkout develop
 $ git merge feature/readme
 $ git push
 ```

 The above commands are used to:
 * switch to a new branch `develop` (we deleted develop in the past)
 * from develop we swithc to a new branch `feature/readme`
 * edit file
 * make a commit
 * switch to branch `develop`
 * merge branch `feature/readme` into develop
 * push develop to remote

 ---
 
