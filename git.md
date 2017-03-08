# GIT USAGE NOTE

## basic 

git init
: init a repository, no needed options

git three concept
: repository, index file, working tree

edit working
: edit working tree


git add
: update index file

git commit
: update repository

git commit -a -m
: frequently used, add&commit, update index file & commit to reopsitory. But 

if there new file or new folder, you should run 'git add' manually. the option -a only trace old files.

git diff
: show diff between working tree and index file
git diff --cached

: show diff between index file and reopsitory

git diff HEAD
: between working tree and repository. HEAD is the newest COMMIT in repository

git status
:update means index file is updated. commit means repository is commited/updated

git log

git add .; git commit -a -m "new"

git reset --soft
: only undo commit, working tree and index file will be kept.

git reset
: default option is mixed, which means to undo the 'add' and 'commit' action, only working tree will be kept

git reset --hard
: all things include wogit rking tree will be reset

git reset HEAD^
:reset to last node, the father of HEAD. By default the reset-to node is HEAD. So if you want to undo a commit, usually you should use HEAD^.

You can use 6 digit hash code to represent a commit node at any time.

## Review an older version
You can use 'git checkout hashcode' to checkout any version of the code, and there will be an new branch called 'no branch' to show the code. nothing will be changed. Use 'git checkout master' to back to master branch. If you want to keep the code, you can use 'git branch newbranch' to keep the code into a new branch.
 
## Branch

branch
:git branch  newbranch #新建一个branch
 git branch -d newbranch  #delete the branch
 git checkout newbranch  #switch to branch


git clone git@210.45.66.101:testing   gitolite-admin
git push origin master
git push

git pull
: fetch + merge

git fetch <options><reopsitory><src>:<dst>
: get remote repository to local

git merge
: merge branch

set -u
: set this remote be default remote 

TO BE CONTUNUE...

git tag  V3   4fb8jl    
: to mark a commit with another name.

git show
:

git rm
:

git mv
:

git
:to show the help page.
gitolite configuration to see the tutial of gitolite.

remote adress format
:used for rcp, git, rsync and so on
username@hostname:path   no port

url format
:used for source access.
ftp://username:passwd@hostname/path

# remote action:

git clone only clone one branch frome remote server, defaultly the branch is master. to specify which branch to clone you should use  git clone --branch branchname

creat a branch:   git push origin labdist:labdist     format:  git push remote local-branch:remote-branch, by default git will creat a new branch.

fetch a branch:   git fetch origin labdist:labdist   if not specify the destiny branch, fetch will creat a  FETCH_HEAD, a temp head to store the fetched branch.

pull: git pull origin labdist:labdist     if local branch is not specified, by default git will pull remote branch to FETCH_HEAD and merge to local current branch.

merge   :  always to current branch

pull fetch 如果目标不填, 默认是FETCH_HEAD, 如果源不填, 默认是一开始克隆来的分支

push如果目标不填, 默认是和源同名分支, 如果源不填, 默认是克隆来的分支.

一个合作者或者一台机器要操作某个分支, 最好一开始就直接克隆这个分支. 这样默认的push和pull都配置好了

config配置
remote origin
pull push的分支用

本地直接用merge就可以了

所有操作都是分支对分支的操作. 本地和远端base不一样只能合并.

rebase 
