# Git Note

Before all:
~~~
$ git config --global user.name "Name"
$ git config --global user.email "Email@email.com"
~~~

## Basic commands
---
### One branch local

#### 1. <code>git init</code>
Initialize git repository, generate <code>./.git/.</code>

#### 2. <code>git add [< file >] ['\*.\*'] [.]</code>
Add new files to stage.<br>
Before committed, unstage by typing:
~~~
$ git reset HEAD < file >
~~~
which means reset < file > to HEAD version.<br>
Discard changes of file by typing:
~~~
$ git checkout -- < file >
~~~
It's also available to revoke a whole version by:
~~~
$ git reset HEAD^
or
$ git reset HEAD~5
~~~

#### 3. <code>git commit [-a] -m < commit message ></code>
Commit stage to repository.<br>
There's only one commit when typing:
~~~
$ git commit -m "initial commit"
$ git add forgotten_file
$ git commit --amend
~~~

#### 4. <code>git log [*]</code>
Print log.<br>
~~~
$ git log --pretty=oneline  //show in one line.
~~~

### One branch remote

#### 5. <code>git remote add < remote name > < address ></code>
Add remote repository.

#### 6. <code>git clone < address ></code>
Clone repository from remote.

#### 7. <code>git push < remote name > < branch name ></code>
Push. Fail when conflicts exist.

#### 8. <code>git fetch < remote name > < branch name ></code>
Fetch. Get pointer <code>FETCH_HEAD</code>.

#### 9. <code>git pull < remote name > < branch name ></code>
Pull and merge.

#### 10. <code>git diff [*] [< file >] [HEAD...FETCH_HEAD]</code>
Show diffs between versions and repositories.
```sh
# show diff of file bwteen this and last commit
$ git diff HEAD file
# show diff between this and last commit
$ git diff HEAD HEAD^
```


#### 11. <code>git tag [*] < tag > [-m < message >] [< commit id >]</code>
Tag commit.
~~~
$ git tag -a v0.1 -m message       //generate a tag
$ git tag -d v0.1                  //delete a tag

$ git push < remote name > <tag>   //push a tag
~~~

### Multi branch

#### 12. <code>git branch [*] [< branch name >]</code>
Show all branches or create or delete branch.<br>
With <code>[-d]</code> we can delete a branch:
~~~
$ git branch -d dev
~~~

#### 13. <code>git checkout < branch name ></code>
Switch to < branch name >.
With <code>[-b]</code> we can create and switch to a new branch:
~~~
$ git checkout -b dev
~~~

#### 14. <code>git merge < branch name ></code>
Merge < branch name > to master, failing when conflicts exist.

## Tricks
---

#### 1. <code>git config --global alias.\*\* \*\*\*</code>
replace command \*\*\* with \*\*.
~~~
$ git config --global alias.st status
$ git st

$ git config --global alias.unstage 'reset HEAD'
$ git unstage < file >

$ git config --global alias.last 'log -1'
$ git last

$ git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
$ git lg
~~~

#### 2. <code>./.git/config</code> and <code>~/.gitconfig</code>
Config.

#### 3. <code>./.gitignore</code>
Including files generated by system, during building, or config.

Other gitignore file at [github](https://github.com/github/gitignore)
~~~
# Windows:
Thumb.db
ehthumbs.db
Desktop.ini
#Python:
*.py[cod]
*.so
*.egg
*.egg-info
dist
build
~~~

#### 4. config diff tool and merge tool
