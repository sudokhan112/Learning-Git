# git_notes

## Resources:
**1. Happy Git and GitHub for the useR**(https://happygitwithr.com/)

**2. Learn Git Branching** (https://learngitbranching.js.org/)

**3. Git - the simple guide** (https://rogerdudler.github.io/git-guide/)

**4. Oh,shit! Git?!** (https://ohshitgit.com/)



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

- updating remote branches
  
 ![Screenshot from 2021-09-17 13-58-59](https://user-images.githubusercontent.com/77024625/133840268-1509ae23-42af-44de-a5ff-2313529e2703.png)
  
  `git commit`
  
![Screenshot from 2021-09-17 13-59-56](https://user-images.githubusercontent.com/77024625/133840365-10d17ebc-20bb-4366-8053-a7089a007e7b.png)

  `git pull`
  
  ![Screenshot from 2021-09-17 14-00-54](https://user-images.githubusercontent.com/77024625/133840420-165c535f-eaae-4cfc-9668-69930910e92f.png)

  
- `git push` is responsible for uploading your changes to a specified remote and updating that remote to incorporate your new commits. Once git push completes, all your friends can then download your work from the remote.
  
  - 
Imagine you clone a repository on Monday and start dabbling on a side feature. By Friday you are ready to publish your feature -- but oh no! Your coworkers have written a bunch of code during the week that's made your feature out of date (and obsolete). They've also published these commits to the shared remote repository, so now your work is based on an old version of the project that's no longer relevant.

In this case, the command git push is ambiguous. If you run git push, should git change the remote repository back to what it was on Monday? Should it try to add your code in while not removing the new code? Or should it totally ignore your changes since they are totally out of date?
  
  ![Screenshot from 2021-09-17 14-13-28](https://user-images.githubusercontent.com/77024625/133841721-dcffea15-ae3a-4ae5-a902-e34d0c03863f.png)
  
  `git pull --rebase`
  `git push`
  
  ![Screenshot from 2021-09-17 14-18-27](https://user-images.githubusercontent.com/77024625/133842317-02425646-c00d-480c-98a3-d5516d03fa6b.png)
  
  But with `git pull` then `git push`
  
  ![Screenshot from 2021-09-17 14-20-34](https://user-images.githubusercontent.com/77024625/133842553-8ce71b90-d3df-4695-a790-8b05f25b3a01.png)

- Next Topic:
  
  ![140814368-22a70033-78a2-4349-9bd6-e7e6cd1338a2](https://user-images.githubusercontent.com/77024625/140814368-22a70033-78a2-4349-9bd6-e7e6cd1338a2.png)

**Input** 
  
  ![7fe192f6-fe2f-4ca0-865e](https://user-images.githubusercontent.com/77024625/140820533-7fe192f6-fe2f-4ca0-865e-7cc038aec46e.png)
  
 **Output**
  
  ![d80950e7-33ee-43da-a7bd](https://user-images.githubusercontent.com/77024625/140820627-d80950e7-33ee-43da-a7bd-3e4dc3ff00bc.png)

  step 1: `git checkout main; git pull --rebase`
  
  ![abbf1438-c346-4151](https://user-images.githubusercontent.com/77024625/140821043-abbf1438-c346-4151-88e5-afcb57dfb35c.png)

  step 2: `git checkout side1; git rebase main`
  
  ![6b28a044-6053](https://user-images.githubusercontent.com/77024625/140821316-6b28a044-6053-497c-9663-787521497425.png)
  
  step 3: `git checkout main; git rebase side1; git push`
  
  ![89aa44b73-f3ef](https://user-images.githubusercontent.com/77024625/140821774-9aa44b73-f3ef-48e3-96f9-8be7fac5f472.png)
  
  step 5: (we can also use cherry-pick) `git cherry-pick C3 C4; git push`

  ![220a-4db6-8df3-](https://user-images.githubusercontent.com/77024625/140822038-fc315561-220a-4db6-8df3-248a50fcd0c2.png)
  
  step 6: `git cherry-pick C5 C6 C7; git push`
  
  ![b7cd2455-9dac-44f2](https://user-images.githubusercontent.com/77024625/140822360-b7cd2455-9dac-44f2-97f3-535ec6e00443.png)


 Easier way to complete this:
  - `git fetch` (fetch C8 from remote and point o/main to C8)
  - `git rebase o/main side1` (rebase side1 on top of o/main)
  - `git rebase side1 side2`
  - `git rebase side2 side3`
  - `git rebase side3 main`
  - `git push`

**Rebase vs. Merge**
  
 There's a lot of debate about the tradeoffs between merging and rebasing in the development community. Here are the general pros / cons of rebasing:

Pros:

Rebasing makes your commit tree look very clean since everything is in a straight line
  
Cons:

Rebasing modifies the (apparent) history of the commit tree.
For example, commit C1 can be rebased past C3. It then appears that the work for C1' came after C3 when in reality it was completed beforehand.

Some developers love to preserve history and thus prefer merging. Others (like myself) prefer having a clean commit tree and prefer rebasing. It all comes down to preferences.
  
- We can do the above mentioned problem but with `git merge`
```
$ git fetch
$ git checkout main
$ git pull
$ git merge side1
$ git push
$ git merge side2
$ git push
$ git merge side3
$ git push
  ```
![54394822-ffae](https://user-images.githubusercontent.com/77024625/140826431-54394822-ffae-4b91-b4b0-24972301b446.png)
  
- You can make any arbitrary branch track o/main, and if you do so, that branch will have the same implied push destination and merge target as main. This means you can run git push on a branch named totallyNotMain and have your work pushed to the main branch on the remote!

There are two ways to set this property. The first is to checkout a new branch by using a remote branch as the specified ref. Running

`git checkout -b totallyNotMain o/main`

Creates a new branch named totallyNotMain and sets it to track o/main.
  
![41d8-4fe8-9844](https://user-images.githubusercontent.com/77024625/140827110-ad3de2a0-41d8-4fe8-9844-a95e9429ce26.png)


Another way to set remote tracking on a branch is to simply use the git branch -u option. Running

`git branch -u o/main foo`

will set the foo branch to track o/main. If foo is currently checked out you can even leave it off:

`git branch -u o/main`
  
**Input**
  
![2e5094fb-5d1d](https://user-images.githubusercontent.com/77024625/140828320-2e5094fb-5d1d-42fb-b82d-b4f75c1b9fe3.png)

**Output**

![ab65-468c-be69](https://user-images.githubusercontent.com/77024625/140828442-41d2c46b-ab65-468c-be69-58a19f01444b.png)
  
```
$ git checkout -b side
$ git commit
$ git branch -u o/main
$ git fetch
$ git rebase o/main
$ git push
```

  
#### Git push
  
git push can optionally take arguments in the form of:

`git push <remote> <place>`
 Ex: `git push origin main`
 
translates to this in English:

*Go to the branch named "main" in my repository, grab all the commits, and then go to the branch "main" on the remote named "origin". Place whatever commits are missing on that branch and then tell me when you're done.*
  
By specifying main as the "place" argument, we told git where the commits will come from and where the commits will go. It's essentially the "place" or "location" to synchronize between the two repositories.
Keep in mind that since we told git everything it needs to know (by specifying both arguments), it totally ignores where we are checked out!

**Input**
  
  ![fe25a8e8](https://user-images.githubusercontent.com/77024625/144614214-fe25a8e8-a8ba-4fd6-907c-fc1b559a575e.png)

**Output**
  
  ![59a69ad2](https://user-images.githubusercontent.com/77024625/144614333-59a69ad2-2d02-4d11-97bc-595ee16b7c2a.png)

```
  git push origin main
  git push origin foo
```
  
You might then be wondering -- what if we wanted the source and destination to be different? What if you wanted to push commits from the foo branch locally onto the bar branch on remote? n order to specify both the source and the destination of <place>, simply join the two together with a colon:

`git push origin <source>:<destination>`

This is commonly referred to as a colon refspec. Refspec is just a fancy name for a location that git can figure out (like the branch foo or even just HEAD~1).
  
![b0c18c2c](https://user-images.githubusercontent.com/77024625/144616026-b0c18c2c-92bf-4bcf-9961-f817bafc67f9.png)
  
![4ce55968](https://user-images.githubusercontent.com/77024625/144616135-4ce55968-9209-440b-8cc8-efb828b973b9.png)
  
**Input**
  
 ![585e11af](https://user-images.githubusercontent.com/77024625/144616268-585e11af-1ffa-46ab-9f2d-8d7f2c8678b3.png)
  
 **Output**
  
![70d18b4d](https://user-images.githubusercontent.com/77024625/144616347-70d18b4d-5b99-4aee-959a-bd8d8b1258b0.png)


step 1: `git push origin foo:main`
  
![bdb5bae0](https://user-images.githubusercontent.com/77024625/144870422-bdb5bae0-d223-4ad3-94d8-8e8a1fa51bcd.png)

step 2: `git push origin main^:foo`
  
Solved!


  
#### Git Fetch
The arguments for git fetch are actually very, very similar to those for git push. It's the same type of concepts but just applied in the opposite direction (since now you are downloading commits rather than uploading).
  
If you specify a place with git fetch like in the following command:

`git fetch origin foo`

Git will go to the `foo` branch on the remote, grab all the commits that aren't present locally, and then plop them down onto the `o/foo` branch locally.
  
You might be wondering -- why did git plop those commits onto the `o/foo` remote branch rather than just plopping them onto my local foo branch? I thought the <place> parameter is a place that exists both locally and on the remote?

Well git makes a special exception in this case because you might have work on the `foo` branch that you don't want to mess up!! This ties into the earlier lesson on `git fetch` -- it doesn't update your local non-remote branches, it only downloads the commits (so you can inspect / merge them later).
  
"Well in that case, what happens if I explicitly define both the source and destination with `<source>:<destination>`?"

If you feel passionate enough to fetch commits directly onto a local branch, then yes you can specify that with a colon refspec. You can't fetch commits onto a branch that is checked out, but otherwise git will allow this.

Here is the only catch though -- <source> is now a place on the remote and <destination> is a local place to put those commits. It's the exact opposite of git push, and that makes sense since we are transferring data in the opposite direction!

That being said, developers rarely do this in practice. I'm introducing it mainly as a way to conceptualize how fetch and push are quite similar, just in opposite directions.
  
![d349e918](https://user-images.githubusercontent.com/77024625/144874768-d349e918-0003-45eb-8f19-9359e9bb6f2f.png)
  
![6a5f7ca2](https://user-images.githubusercontent.com/77024625/144875026-6a5f7ca2-41f0-4e8b-ab08-b7082219c9a2.png)

 **Git Alias**
  
Edit ~/.gitconfig to add these useful developer shortcuts.

```
[core]
	editor = code --wait
[alias]
	co = checkout
	cob = checkout -b
	cp = cherry-pick
	go = clone --recurse-submodules -j8
	kill = branch -D
	last = log -1 HEAD
	lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
	ll = log --pretty=oneline --graph --name-status
	pr = !git fetch --all --prune && git prune && git remote prune origin
	spull = !git fetch --all && git pull --rebase && git submodule sync --recursive && git submodule update --init --recursive
	spush = push --recurse-submodules=on-demand
	sup = submodule update --recursive --init
	sync = !git fetch --all && git pull --rebase origin master
	undo = reset HEAD~1 --mixed
	unstage = reset HEAD --
	wipe = clean -Xfd
	amend = commit --amend
[diff]
	submodule = log
[fetch]
	recurseSubmodules = on-demand
[init]
	templatedir = ~/.git-templates
[pull]
	rebase = true
[status]
	submoduleSummary = true
[rerere]
	enabled = true
```

  **Want to squash commits before merge request**

 This will create a interactive rebase against `master` branch.
  
`naz@pop-os ~/git-cloned-repos/psf-vsn/sources/row-guidance (naz/save-data-csv) `
 
`$ git rebase -i origin/master`
  
 Then you pick all the commits that you want to squash as `s` and leave the commit
 as `pick` where you want to squash all the commits.
  
 Then you have to force push the new commits on your branch at `origin`
 
 ` $ git push -f origin naz/save-data-csv `
