# Git Commands

## Git cmd

`git init`: initialize git in the current directory.
`git add`: add files to staging area.
`git reset`: unstage changes
`git commit`: add a commit.
`git push`: push the updates in the repo to GitHub.

### log

- Pretty logs: `git log --oneline --decorate --graph --all --abbrev-commit`
- Shorter version: `$ git log --pretty=oneline --decorate --graph --all --abbrev-commit`

Add to `.bashrc`
```bash
alias glt='git log --oneline --decorate --graph --all --abbrev-commit'
alias gltt='git log --pretty --decorate --graph --all --abbrev-commit'
alias glta='git log --graph --decorate --pretty='\''%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'\'' --all --abbrev-commit'
```
1. commit message of each commit and branches
2. More informative version
3. More colorful and informative version
### branch

[tutorial](https://www.atlassian.com/git/tutorials/using-branches)
- List all branches: `git branch`
- Create branch: `git branch <branch>`
- Checkout branch: `git checkout <branch>`
- Rename current branch: `git branch -m <branch>`
- List all remote branches: `git branch -a`
- Delete branch (after merge!): `git branch -d <branch>`
- Force delete: `git branch -D <branch>`
- Each branch needs to be pushed separately: `git push origin <branch>`
## Github

[Choose license](https://choosealicense.com/)
[How to set it up](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories)
`git remote add origin https://github.com/chuyaowang/bluearchiveApp` set up remote repo
`git push --set-upstream origin main`: set up upstream branch to use `git push` to directly push to this repo
`git push -u origin main`: push to this repo and the local main branch，-u is shorthand for --set-upstream
`git pull --rebase`: [rebase vs. merge explain](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
`git clone --depth=1`: shallow clone a repository

## gitee

`git remote add gitee https://gitee.com/jumping-beaver/bluearchiveApp`