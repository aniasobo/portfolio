# Weeks 8-9, 15-28.07.2019

## Goals: 

- [x] build a Rails app

## Practice

Date | Project | progress
--- | --- | ---
15-28.07 | [Acebook - team engineering project](https://github.com/bengscott2/acebook-livewire) | [project notes](https://github.com/aniasobo/portfolio/blob/master/challenges/acebook.md)
20-21.07 | Instagram clone - [GitHub](https://github.com/aniasobo/instagram-challenge) - [Heroku app](https://fauxtagram.herokuapp.com) | project notes

### git tips:

[from here](https://dev.to/antjanus/my-personal-git-tricks-cheatsheet-23j1)  

when branch falls behind master:

```
git fetch origin
git rebase origin/master
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
