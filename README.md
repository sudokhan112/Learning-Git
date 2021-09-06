# git_notes

## Resources:
**1. Happy Git and GitHub for the useR**(https://happygitwithr.com/)

**2. Learn Git Branching** (https://learngitbranching.js.org/)

**3. Git - the simple guide** (https://rogerdudler.github.io/git-guide/)

**4. Oh,shit! Git?!** (https://ohshitgit.com/)




#### Commands

- git reset src/*

- git pull --rebase

- git log --oneline --graph --all

- git submodule update --init --recursive

- git submodule sync

- git remote get-url origin

- cat .gitmodules 

- git submodule update --init --recursive --remote

- git remote -v

- git fetch --all

- git checkout master

- git log --stat --summary

- git rebase -i master

- git mergetool -t meld

- git rebase --abort

- One of the most common ways I use relative refs is to move branches around. You can directly reassign a branch to a commit with the -f option. So something like:

`git branch -f main HEAD~3`

moves (by force) the main branch to three parents behind HEAD.
![image](https://user-images.githubusercontent.com/77024625/132250798-475d3fb4-4c64-4a87-91a7-078cc968f24e.png)
![image](https://user-images.githubusercontent.com/77024625/132250876-0295d210-bab5-4117-9f9d-dc3c4a2f4c7b.png)


