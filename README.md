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
![im1](https://user-images.githubusercontent.com/77024625/132250798-475d3fb4-4c64-4a87-91a7-078cc968f24e.png) ![im2](https://user-images.githubusercontent.com/77024625/132251127-dd8cecca-6933-4315-891f-a21c3de45b70.png)


- `git rebase main`

![im3](https://user-images.githubusercontent.com/77024625/132252982-ab4423ed-aab1-4b4c-81e7-f86490b942b9.png) ![im4](https://user-images.githubusercontent.com/77024625/132253065-54691a14-1c96-4d17-b808-ef7144e6f249.png)

Now the work from our bugFix branch is right on top of main and we have a nice linear sequence of commits.Note that the commit C3 still exists somewhere. 
Now to merge the main branch onto bugFix:

![im5](https://user-images.githubusercontent.com/77024625/132253373-59d37aea-069d-423b-8fba-dd257d398105.png)

- Relative commits are powerful, but we will introduce two simple ones here:

Moving upwards one commit at a time with `^`.
Moving upwards a number of times with `~<num>`.

- ![im6](https://user-images.githubusercontent.com/77024625/132255553-8ccb2e7b-33e2-4528-a2b3-76859102a8dc.png)

`git branch -f main HEAD~1`. force move the main branch 1 level up the current HEAD.

![im7](https://user-images.githubusercontent.com/77024625/132255694-63d666de-69c4-4c44-8799-9eca9ff032c1.png)

`git checkout main`

`git merge C6`. merging main branch to a specific commit.

![im8](https://user-images.githubusercontent.com/77024625/132255932-f6d6270e-79b4-40bf-b675-2a034b1f6440.png)

moving the bugFix branch to specific commit. `git branch -f bugFix HEAD~4`
![image9](https://user-images.githubusercontent.com/77024625/132255997-e0546926-5e3b-42d0-b477-3bf1458abb87.png)


- `git reset` 

![image10](https://user-images.githubusercontent.com/77024625/132257372-91b7b409-1294-4d80-b197-77675249fa42.png)

- While resetting works great for local branches on your own machine, its method of "rewriting history" doesn't work for remote branches that others are using. `git revert`.

![image11](https://user-images.githubusercontent.com/77024625/132257538-288337bb-d655-4a5d-adc5-21b7c0c17ab4.png)

- `git cherrypick`

![image12](https://user-images.githubusercontent.com/77024625/132258329-6d893790-7591-4f4c-b11c-2bb7ca5f86a0.png)

That's it! We wanted commits C2 and C4 and git plopped them down right below us. Simple as that!

![image13](https://user-images.githubusercontent.com/77024625/132258394-f8f961cd-c400-4d14-8094-decf2b7e4c44.png)


