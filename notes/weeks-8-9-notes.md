# Weeks 8-9, 15-28.07.2019

## Goals: 

- [x] build a Rails app

## Practice

Date | Project | progress
--- | --- | ---
15-28.07 | [Acebook - team engineering project](https://github.com/bengscott2/acebook-livewire) | [project notes](https://github.com/aniasobo/portfolio/blob/master/challenges/acebook.md)  
20-21.07 | Instagram clone - [GitHub](https://github.com/aniasobo/instagram-challenge) - [Heroku app](https://fauxtagram.herokuapp.com) | [project notes](https://github.com/aniasobo/portfolio/blob/master/challenges/instagram.md)  


### git tips:

[from here](https://dev.to/antjanus/my-personal-git-tricks-cheatsheet-23j1)  

when branch falls behind master:

```
git fetch origin
git rebase origin/master
// git reset --hard origin/master will discard all changes
```

for small fixes in separate commits:

```
git commit --amend --reuse-message HEAD
```
(this throws error on branch, not sure why)

to only retrieve certain commits without the entire codebase:

```
git cherry-pick hash-goes-here
git cherry-pick first-hash second-hash third-hash
```

- [x] added `git-up` and `git up`

```
alias git-up="git branch | sed -n -e 's/^\* \(.*\)/\1/p' | xargs git push -u origin "

git config --global alias.up = push -u origin
```


**Rails tip**

Create a Rails app that runs on PostGreSQL from the get go with `rails new my_app_name --database=postgresql`

`bin/rails routes` to see all your routes (routing debugging)

---

### Q&A workshop

**git tip**

merging feature branch to master mid-work:

- PR/merge or rebase

PR adds a commit, rebase doesn't; rebase rewrites, PR just adds.

- commit or stash your branch
- go back to master
- pull recent changes from master
- go back to your branch and rebase master (NOT origin master) OR merge your branch with master (`git merge master`)

`git fetch` just adds current info to your git, like any new branches.

rebase requires some resolving of conflicts - or automatic overwrite.

not a good idea to pull master into branch.

**undoing changes on feature branch**

- revert locally  
- revert remotely  
- reset HEAD
- rebase (interact?)

**trunk-based development**

short-lived feature branches - constant PRs to master. 

pruning redundant branches regularly.  

**how to test in Rails**

- feature test - the whole app; the most important testing to be done in a rails app
- controller tests - send request to the controller, receive a response; good for the Rails API.

Controller, model & view - should have as little logic as possible and be v skinny; keep the logic for the /lib.

**acceptable logic to put in views:**  

- If statements 
- loops
- (ok not to unit test views as feature testing should cover the logic)

**debugging with pry**

`save_and_open_page` and `puts page.body` let you peek inside the DOM from the POV of the Selenium Driver

`exit!` to exit pry 

**how to get Travis to run the correct version of FF for JS tests:**  

```
addons:
  firefox: "33.0"
before_script:
  - export DISPLAY=:99.0
  - sh -e /etc/init.d/xvfb start
```


**git rebase tip:**

run `git rebase master` from your branch to move it forward in time. commit first.

`git checkout master^` - checks out the parent of master.

`git checkout master^^` - checks out the grandparent of master.

`git checkout HEAD^` - move back/up a level in the commit tree (ie go back in time with commits).

`git checkout HEAD~4` - move back four times.  

reassign a branch to a commit in the past: `git branch -f master HEAD~4` - forces master to the commit that is 4 parents behind HEAD.

`git reset HEAD~1` - moves branch back a commit as if the changes never happened; good solution for __local branches__  

`git revert HEAD` - introduces a change to your remote but that change is undoing - so that others can update their copies of your branch to this new state; good fore __remotes__  

`git cherry-pick <commit> <commit><c...` - puts specified commits below current HEAD  

interactive rebase: `git rebase -i HEAD~4` - vim window with the last 4 commits behind HEAD opens up and allows you to drag/drop commits to rearrange commit history  

moving only one commit to master (ex. result of bug fix without the whole debugging history): 
`git rebase -i` followed by `git cherry-pick`, example:  
`git checkout master` - moves from branch to master
`git cherry-pick <commit>` - adds the chosen commit only to master  

mark commits that are milestones with git tags: `git tag <tag> <commit hash>`  

`git describe <ref>` - ref can only be something that can be resolved into a commit; default is HEAD; outputs:  
`<tag>_` - closest ancestor tag in history  
`<num commits>_` - how many commits away that tag is  
`_g<hash>` - the hash of the commit being described  

**rebasing multiple branches**

`git checkout HEAD^2` - checks out the second parent  
`git checkout HEAD~^2~2` - moves up one level, then to the second parent, then up 2 levels over that parent;  

**remotes**  

`git fetch` - gets data from a remote, and updates the local representation of that remote; it downloads the commits that the remote has but the local repo does not (say, added by other people); it then updates where the remote branches point 

  