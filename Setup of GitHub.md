# **\[Intro for GitHub 2026-06-10]**

This document will explain the good way to make GitHub repository that contain synchronized some local files and how to use them, some other useful commands, troubleshoots.



##### Premise

* installed git to your local pc(Windows)
* installed MATLAB



### **Section 1: Make Your Repository**

This section will introduce the robust way to create a local repository that synchronized to a remote repository.



##### Step 1: Make a Remote Repository

At first you need to make a repository with using browser. If you want to take a way of this document, you should make a repository that contain completely nothing(README.md or LICENCE, .gitignore, etc.).So, you have to only specify the name for repository when you make repository with browser firstly.

If the repository has at least one file, this would be recognized as first push by GitHub and they would make first branch. Then, if you want to push some local files, you better make empty repository to dodge the branch name conflict or other unexpected errors.



##### Step 2: Do Some Configurations at Local Environment

If there is any conflict or mismatch about default branch name between latest GitHub and your local GitHub environment, you will get an error when you push local files to a repository that already has a first branch.

For now, latest GitHub's default branch name is "main".



Check your current local default branch name:

> git config --global init.default Branch



If you got "master" as a result, you need to change it. If you got "main", you can skip this step.



To change:

> git config --global init.default Branch main:



Check again:

> git config --global init.default Branch



##### Step 3: Make a Local Repository and Synchronize it to the Remote One

At this step, We will make the local directory that works as a local repository and make first commit, push to a initial branch.



Make a new local directory that has the same name as the remote repository you made few minutes ago.



Move to arbitrary directory:

> cd {the directory that will work as a local repository}



If you have used that directory with GitHub, there is possibility to existing some cache files. To keep that directory completely clean, you can execute below command.

Any way, this concern is not appropriate for majority case, that using new local directory you made.



Discard previous .git:

> rmdir /s /q .git



Now you have to make some cache files related to Git things.



Initialize Directory:

> git init



You have to make at least one file to make your first commit. So lets make any kind of files like .txt to explain about the repository. It can be completely anything. But you have to create at least one.

If you do not this, you will got the message from git that saying "nothing to commit!!!". Since this message is written by white, not red, so beginner would not recognize this will be a problem and try push the empty folder, and get red error message in this time like "error: failed to push some...", finally you get upset. Haha.



So, Make a file like "{your repository name}.txt" that explains what your repository is supposed to do, in your repository directory.



Add files to tracking:

> git add .



When you type upon command, you have to insert space between "add" and ".". "." means all files belong to that directory.



Make Initial commit:

> git commit -m "Initial commit" -m "Initial commit with README.md and .gitignore, ..."



When you execute upon command, you have to be careful that you haven't contained any kind of parentheses(, \[, { to your commit message. Windows CLI is week for those, so you will probably get an errors if you do that.



Add remote repository:

> git remote add origin {URL of your repository}



The URL of your repository must be end with ".git". You can copy the URL from your repository page. And in upon command you defined your repository nickname "origin" because it's too long to call proper name of the repository(Actually this is URL you typed).



Push files:

> git push origin main



If your local repository is completely empty, you cannot push files due to GitHub request at least one file. In that time, you should make .gitignore or README.md for instance.

Finally, you got a local repository that synchronized with your remote repository. But be very careful not to execute "git init" again. This will break all works we made in this step.



##### Step 4: Push Your Works

If you do some work at your local PC, you have to push those works at the end of the day. This step will explain how to do it.



Firstly, you have to move to the directory that you set as a local repository before.



Add files:

> git add .



Commit:

> git commit -m "commit message" -m "extended commit message"



Push:

> git push origin main



##### Step 5: Clone and Update Your Local Repository

This step is intended to execute on a different pc than the one used in the previous step.



Clone:

> git clone {URL of your repository}



Update local repository:

> git pull origin main



In this section we introduced how to develop an synchronized remote-local repository environment. In daily works, you have to push and pull your all works at the end of the days, but besides that in this section.



### **Section 2: In Your Daily Works**

This section will explain what we put beside at the last of the previous section, that is how to update your environment(push and pull) in daily progress. This procedure is intended to do after you achieved developing of your environment.



##### Step 1: Push Your Works

When you have done some works, you have to update those progress and update your remote repository.



Push:

> git add .

> git commit -m "A commit message" -m "You can add extended explanation if you want"

> git push origin {Branch name}



###### Step 2: Pull Your Works

When you want to update your local repository at latest version, you have to pull it at the start of the daily works.



Pull:

> git pull origin {branch name}

###### 

##### Option 1: Make A New Branch

You can make new branch of your repository arbitrary, but if you work at that project alone, you better do your work simply as you can. You can make new branch by executing below command.



Make new branch:

> git checkout -b {New Branch Name}



Change current branch:

> git checkout {Your Current Branch Name}



Push your works to new branch:

> git push origin {New Branch Name}



Finally, you have to keep in your mind that you must update the progress at the start and the end of your works on your every local PC environment. If you forget to do that, you will get an conflict error and it is so troublesome to solve.



##### Useful Commands:

Confirm the status: This will inform you what the branch are you working on, your branch is up to date with GitHub or not and this is the most important though, saving or tracking status of the files. Red color means "changes not staged for commit", Green color means "changes to be committed", Yellow color means "untracked files". Of course, you have to execute this at your local repository directory. "git fetch" will inform your PC the latest information of remote repository to compare your local environment and remote one.

> git fetch

> git status



### **Section 2: MATLAB Synchronization**

This section will explain how to let MATLAB recognize your local repository you already have synchronized previous steps as a project.



##### Step 1: Open MATLAB

Open the MATLAB you have installed.



##### Step 2: Create Project

At the "home" tab, make new project. At the configuration window, specify the directory that you set as a local repository in below procedure. After you made it, you will get "{Project Name}.prj" and "resources/", ".gitattributes" at your local repository. ".gitattributes" will prevent your data corruption but won't work as ".gitignore". So you still have to make your own".gitignore" properly.

So you have to push your progress. You can push second time for the way I introduced in Section1, Step 4.

And you will get a warning that saying newline character of ".pri" "Lf" to "CRLF" due to Windows' default newline character is "CRLF". However this is totally no problem. So you can let it be.



##### Step 3: Clone MATLAB Project on your another PC

In this step, we will clone your GitHub synchronized MATLAB project on your another PC. This step is almost same as Section1, Step 5.

At the first place, you have to move to your arbitrary directory that you want to clone the project.



Move to the arbitrary directory:

> cd {your arbitrary directory that you want to clone the project you made}



Then, Copy the repository URL from GitHub page and clone it.



Clone the project at the directory:

> git clone {URL of your repository}



Note that, cloned your repository already has "{Project Name}.prj" and this file contains all information for MATLAB project. So, next, open the MATLAB and move to the directory you cloned, and click that file. And then you will get fully redeveloped environment on your another PC.



### **Section 4: GitHub Troubleshootings**

In this section, we will introduce some usual situations of troubles for beginners, and how to solve those.



##### Case 1: trouble with single-quotation\[ ' ]

When you type some commands to operate some git things, do not use single-quotation. Especially when you try to commit.



e.g.

> git commit -m 'refine note for study'



And then you will get an error: Hey you! "refine" is not the name for any files, "note" is not the name for any files, or something like that. But, note that this error message is displayed with normal color. So beginner might not realize something is going wrong. But this is completely an error to be solved.



So, git cannot recognize single-quotation having a role as double-quotation. If you do commit with single-quotation and then you tried to push, you will get this:



> Everything up-to-date



This is a trap. Beginner might feel, Oh, So It is ok with this and think push was succeed, even nothing have pushed. Actually, When you get this message, you will get some green message that tells there is a changes to be committed by executing git status.



Because you used single-quotation to commit and commit was not succeed and git says like everything u-to-date. This is quite obvious.

