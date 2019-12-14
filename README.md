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

[0]The above commands are used to:
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

[1]The above commands are used to:
 * create new branch `develop` and switch to it
 * create css file
 * edit css file
 * edit html file to link the css
 * add new file and modified file to track
 * commit those changes
 * check all the branches in local and remote 
 * push to remote (use --set-upstream origin <branch-name> if there's no local branch name in remote)

---

 [2]On github create pull request > merge pull request > delete branch develop

 * base: `master`
 * compare: `develop`

 Back to the local repository

 ```
 $ git checkout master
 $ git pull
 $ git branch -D develop
 $ git fetch --all --prune
 ```

 [3]The above commands are used to:
 * switch to branch `master`
 * pull new codes from remote repository
 * delete local branch `develop`
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

 [4]The above commands are used to:
 * switch to a new branch `develop` (we deleted develop in the past)
 * from `develop` we switch to a new branch `feature/readme`
 * edit file
 * make a commit
 * switch to branch `develop`
 * merge branch `feature/readme` into develop
 * push `develop` to remote

 ---
 
Currently we are in branch `develop`. We also decided to add javascript in association with `index.html`

```
$ git branch -D feature/readme
$ git checkout -b feature/js
$ vim readme.md
$ git commit -am "fix: fixed typos in readme.md"
$ touch script.js
$ vim script.js
$ vim index.html
$ git commit -am "feature: a mini webpage"
$ git push --set-upstream origin feature/js
```

[5]The above commands are used to:
* remove local branch `feature/readme` (we no longer use it)
* create new branch `feature/js` and switch to it
* edit `readme.md` to fix some typos
* commit the changes
* create new file `script.js`
* edit file `script.js`
* edit file `index.html`
* commit the changes
* push them to the remote repository

Then we merge `feature/js` into `develop` on github, similar to step [2] and remove `feature/js`. Back to local repository branch `develop` and keep in sync with remote

We are happy with what we did, so we merge `develop` into `master` and set up a milestone to it

`$ git tag -v 0.1.0 -m "basic structe settled up"`

[6]the above command is used to:
* creat a tag version 0.1.0 with a message

