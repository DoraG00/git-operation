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

>Level: Immediate

Git is a great communication tool until you have to collaborate with others

First let's view the data struction about what git is used
```
$ tree .git/
.git/
|--- COMMIT_EDITMSG
|--- FETCH_HEAD
|--- HEAD
|--- ORIG_HEAD
|--- branches
|--- config
|--- description
|--- hooks
|    |--- applypatch-msg.sample
|    |--- commit-msg.sample
|    |--- post-update.sample
|    |--- pre-applypatch.sample
|    |--- pre-commit.sample
|    |--- pre-push.sample
|    |--- pre-rebase.sample
|    |--- pre-receive.sample
|    |--- prepare-commit-msg.sample
|    |--- update.sample
|--- index
|--- info
|    |--- exclude
|--- logs
|    |--- HEAD
|    |--- refs
|         |--- heads
|         |    |--- develop
|         |    |--- master
|         |--- remotes
|         |    |--- origin
|         |         |--- HEAD
|         |         |--- master
|         |--- stash
|--- objects
|    |--- 0a
|    |    |--- 848e69db467af77e396d43873f014a3de2ce46
|    |--- 12
|    |    |--- 2601d7bb3cb47d9a5cdf320692123073fa48d0
|    |--- fd
|    |    |--- bd3b6f42b759c2ae095be60be8426292e0ed59
 * many of lines was omitted here *
|    |--- info
|    |--- pack
|--- packed-refs
|--- refs
|    |--- heads
|    |    |--- develop
|    |    |--- master
|    |--- remotes
|    |    |--- origin
|    |         |--- HEAD
|    |         |--- master
|    |--- stash
|    |--- tags
|         |--- v1.0

```

The above is the file structure in folder `.git/`, to use the `tree` command you have to `brew install tree` on macOS, right now we only focus on `HEAD`, `objects`, `refs`

```
$ git cat-file -t fdbd
blob
$ git cat-file -t 0a84
tree
$ git cat-file -t 1226
commit
```

The above commands are to check the file type of an object, as you can see `blob`, `tree`, `commit`

A `blob` object stores the contents of the file with a SHA1 name

| Type | Length | null | Content |
| :---: | :----: | :---: | :-----: |
| blob |  1064  |  \0  | MIT License... |

```
$ git cat-file -s fdbd
1064
$ git cat-file -p fdbd
MIT License... 
$ git hash-object 'blob 1064 \0MIT License...'
fdbd3b6f42b759c2ae095be60be8426292e0ed59
$ echo 'blob1064\0MIT License...' | openssl sha1
fdbd3b6f42b759c2ae095be60be8426292e0ed59
```

The above commands shows the object size and object contends identified by <object>, and how the hash came from. 

A `tree` stores information about filenames and permissions for associated blobs

| Permissions | Type |            SHA1        | Filename |
| :---------: | :----: | :----------------------: | :--------: |
| 100644 | blob | fdbd3b6f42b759c2ae095be60be8426292e0ed59 | LICENSE |
| 100644 | blob | 8449812f5a4c48192c5ab5ccfbdde488d13a6ee4 | README.md |
| 100644 | blob | 3c2f359f4bcfb89166f6b28c76ad52510adc01f8 | index.html |

```
$ git cat-file -p 0a84
100644 blob fdbd3b6f42b759c2ae095be60be8426292e0ed59	LICENSE
100644 blob 8449812f5a4c48192c5ab5ccfbdde488d13a6ee4	README.md
100644 blob 3c2f359f4bcfb89166f6b28c76ad52510adc01f8	index.html
```

A `commit` points to a top-level tree of changes for this commit and contains metadata about the commit.

|       Tree       |        Parent       |     Author    |     Committer     |     Commit Message    |
| :--------------: | :-----------------: | :-----------: | :---------------: | :-------------------: |
| 632eec11....c263 | dd62333f0b6....2d26 | DoraG00 <user@mail.com> |  DoraG00 <user@mail.com> | "feature: a mini webpage" |

```
$ git cat-file -p 1226
tree 632eec11aad2639f162aff15a454c60e22b8c263
parent dd62333f0b61437bc120e569bf5351f59cbb2d26
author DoraG00 <user@mail.com> 1576340131 +1100
committer DoraG00 <user@mail.com> 1576340131 +1100

feature: a mini webpage
```

A reference, or ref, simply points to a commit, a reference could be 
- Branches
- Tags
- Remote branches
`HEAD` always points to the current branch (or top-level commit), as you can see from the following:

```
$ cat .git/refs/heads/develop
daa78e3aaef24bec0a86f27e7715dc465b780848
$ cat .git/HEAD
ref: refs/heads/develop
```

Question: how these commits are connected? 

`HEAD` -> `refs/heads/<branchName>`  ->  `commit`  ->  `tree`  ->  `blob`

Commits always points to a parent and this forms a linked list where each commit knows who its parent is. It makes branching cheap and easy as each branch just needs to point to a single commit. To see how the commits are connected use the following command in your terminal

`$ git log --oneline --decorate --graph --all`

Question: Rebase VS Merge

|          Rebase         |          Merge        |
| :---------------------- | :-------------------- |
| Pros:                   | Pros:                 |
| - History remains flat and readable  - Superfluous (Commits are likely non-esistent) | - Traceability (The merge commits will show historyical information including full history of the feature branch) |
| Cons:                   | Cons:                 |
| - Can be dangers. Rebase changes commit SHAs, effectively making new commits and diverging a branch from itself. | - The history becomes very polluted (--first-parent flag can be helpful with this) |
| - If a branch has already been synced with a remote then it needs to be push with `-force` flag | - If a feature branch has irrelevant commits, they're now part of history |

We've already used merge a lot, from now on we'll use rebase a lot and collaborate with others.

```
$ git checkout -b feature/rebase
$ touch .gitignore
$ vim .gitignore
$ npm init -y
$ npm install node-sass express --save
$ npm install nodemon --save-dev
** lots of file operation here ** 
$ git add .
$ git commit -m "start to interact with nodejs & scss"
$ git push --set-upstream origin feature/wordle
```