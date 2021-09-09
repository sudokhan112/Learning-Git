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

- git log --stat --summary

- git rebase -i master

- git mergetool -t meld

- git rebase --abort

### Git Locals

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

- `git cherry-pick`

![image12](https://user-images.githubusercontent.com/77024625/132258329-6d893790-7591-4f4c-b11c-2bb7ca5f86a0.png)

That's it! We wanted commits C2 and C4 and git plopped them down right below us. Simple as that!

![image13](https://user-images.githubusercontent.com/77024625/132258394-f8f961cd-c400-4d14-8094-decf2b7e4c44.png)

- When the `interactive rebase` dialog opens, you have the ability to do two things in our educational application:

You can reorder commits simply by changing their order in the UI (via dragging and dropping with the mouse).

You can choose to keep all commits or drop specific ones. When the dialog opens, each commit is set to be included by the pick button next to it being active. To drop a commit, toggle off its pick button.

It is worth mentioning that in the real git interactive rebase you can do many more things like squashing (combining) commits, amending commit messages, and even editing the commits themselves. For our purposes though we will focus on these two operations above.

- Here's another situation that happens quite commonly. You have some changes (newImage) and another set of changes (caption) that are related, so they are stacked on top of each other in your repository (aka one after another). The tricky thing is that sometimes you need to make a small modification to an earlier commit. In this case, design wants us to change the dimensions of newImage slightly, even though that commit is way back in our history!!

![image14](https://user-images.githubusercontent.com/77024625/132261561-660d8a7f-309b-4c3b-8398-0454215625e6.png)

`git rebase -i main` and change sequence of C2 and C3

![image15](https://user-images.githubusercontent.com/77024625/132261641-83bc2ec3-fbbf-4ba0-abe2-d5dd00d5880b.png)

![image16](https://user-images.githubusercontent.com/77024625/132261670-1efb565b-69d3-4cb5-9b3a-3373792eb0cc.png)

`git commit --amend`

![image17](https://user-images.githubusercontent.com/77024625/132261739-e8919c71-45d0-4f49-9bf5-156827efd1f9.png)

`git rebase -i main` (to rechange location of C2 and C3)

![image18](https://user-images.githubusercontent.com/77024625/132261780-88551c2f-12fa-4525-8adc-b9fe0d52f973.png)

`git checkout master`

`git merge caption`

![image19](https://user-images.githubusercontent.com/77024625/132261843-711de17c-929a-4327-9d84-65cc61640b5e.png)

- Git tags support this exact use case -- they (somewhat) permanently mark certain commits as "milestones" that you can then reference like a branch. More importantly though, they never move as more commits are created. You can't "check out" a tag and then complete work on that tag -- tags exist as anchors in the commit tree that designate certain spots.

![Screenshot from 2021-09-08 14-36-06](https://user-images.githubusercontent.com/77024625/132573889-b3f20a2d-2148-4f34-a7bd-f405975d24e8.png)


- Because tags serve as such great "anchors" in the codebase, git has a command to describe where you are relative to the closest "anchor" (aka tag). And that command is called git describe!cGit describe takes the form of:

`git describe <ref>`

Where <ref> is anything git can resolve into a commit. If you don't specify a ref, git just uses where you're checked out right now (HEAD).

The output of the command looks like:

`<tag>_<numCommits>_g<hash>`

Where tag is the closest ancestor tag in history, numCommits is how many commits away that tag is, and <hash> is the hash of the commit being described.
  
  
![Screenshot from 2021-09-08 14-42-35](https://user-images.githubusercontent.com/77024625/132574779-9183c0bb-4215-46e5-9e07-27dcd0a24b9b.png)
  
 - Upper management is making this a bit trickier though -- they want the commits to all be in sequential order. So this means that our final tree should have C7' at the bottom, C6' above that, and so on, all in order.
  
  ![Screenshot from 2021-09-08 15-23-32](https://user-images.githubusercontent.com/77024625/132580092-9d2fea5b-0890-4d48-9b73-6e6af64ea8d5.png)

  `git checkout bugFix`
  `git rebase main`
  
  ![Screenshot from 2021-09-08 15-24-43](https://user-images.githubusercontent.com/77024625/132580256-36a239d4-0a7d-4ac2-87b2-205deddf40a5.png)

  `git checkout C4`
  `git rebase bugFix`
  
  ![Screenshot from 2021-09-08 15-26-37](https://user-images.githubusercontent.com/77024625/132580525-12c25526-cbf3-4db9-a164-3815ec5ed21a.png)

   `git checkout C5`
   `git rebase C4'`
   `git checkout side`
   `git rebase C5'`
   `git checkout another`
   `git rebase side`
  
  ![Screenshot from 2021-09-08 15-29-41](https://user-images.githubusercontent.com/77024625/132580876-7ae19cc2-60c1-4f6c-8ffd-934488efe4de.png)

  `git checkout main`
  `git merge another`

  ![Screenshot from 2021-09-08 15-30-38](https://user-images.githubusercontent.com/77024625/132581004-b0bd1196-5610-4d67-8801-b70ef6d45529.png)


- Branch one needs a re-ordering of those commits and an exclusion/drop of C5. Branch two just needs a pure reordering of the commits, and three only needs one commit transferred!
  
  ![Screenshot from 2021-09-08 16-03-26](https://user-images.githubusercontent.com/77024625/132585266-ac087638-c998-403a-8807-8808c4b119cc.png)
`git checkout one` 
  `git cherry-pick C4 C3 C2`
  
  ![Screenshot from 2021-09-08 16-04-41](https://user-images.githubusercontent.com/77024625/132585409-eda70615-2d16-4979-a901-91c54b39e9c0.png)
  
`git checkout two` .
  `git cherry-pick C5 C4 C3 C2`
  
  ![Screenshot from 2021-09-08 16-06-14](https://user-images.githubusercontent.com/77024625/132585591-9167c4ec-cc5e-4e98-ba77-185d00771773.png)

`git branch -f three C2`
  ![Screenshot from 2021-09-08 16-07-16](https://user-images.githubusercontent.com/77024625/132585726-bca9b6af-feaf-4aa3-bf28-3838f408257d.png)
  

  ### Git Remotes
  
  - Technically, `git clone` in the real world is the command you'll use to create local copies of remote repositories (from github for example). We use this command a bit differently in Learn Git Branching though -- git clone actually makes a remote repository out of your local one. Sure it's technically the opposite meaning of the real command, but it helps build the connection between cloning and remote repository work.
  
  -  Well, remote branches also have a (required) naming convention -- they are displayed in the format of:

`<remote name>/<branch name>`
  
Hence, if you look at a branch named o/main, the branch name is main and the name of the remote is o.

Most developers actually name their main remote `origin`, not o. This is so common that git actually sets up your remote to be named origin when you git clone a repository.
  
  
![Screenshot from 2021-09-09 08-17-09](https://user-images.githubusercontent.com/77024625/132692955-89c2258f-8e1b-416a-aa6d-5320371ffa38.png)

  - In this lesson we will learn how to fetch data from a remote repository -- the command for this is conveniently named git fetch.
You'll notice that as we update our representation of the remote repository, our remote branches will update to reflect that new representation. This ties into the previous lesson on remote branches.

![Screenshot from 2021-09-09 08-22-02](https://user-images.githubusercontent.com/77024625/132693673-aaddb8be-7d32-44f4-aedc-febdb86ae862.png)

  ![Screenshot from 2021-09-09 08-22-54](https://user-images.githubusercontent.com/77024625/132693787-eb36f177-9770-4483-93a7-1158ee2b5f7c.png)

  ![Screenshot from 2021-09-09 08-27-21](https://user-images.githubusercontent.com/77024625/132694546-d8153bb3-2f97-4ede-9340-aafaa1cab2e9.png)
  
![Screenshot from 2021-09-09 08-28-37](https://user-images.githubusercontent.com/77024625/132694705-820cba6f-b52d-4fb7-984f-ec624aca45aa.png)

`git fetch` downloads commits/data for all the branches.
  
  - 
  ![Screenshot from 2021-09-09 16-38-31](https://user-images.githubusercontent.com/77024625/132766083-debe58b1-476d-49dd-943f-1ab55be9588e.png)
  ![Screenshot from 2021-09-09 16-41-31](https://user-images.githubusercontent.com/77024625/132766401-d747c018-ee4e-4914-9a34-79a8f7f37470.png)
  ![Screenshot from 2021-09-09 16-46-44](https://user-images.githubusercontent.com/77024625/132766948-806dd428-58d0-4674-a75b-3a7c056c0748.png)



