Git As A Master
Published on Jun 3rd, 2020 10:40 PM
VERSION CONTROL SYSTEM

Configure Git easily to get it working on any system and ensure name and email are used for commits.
Find out Basic Git commands that you will use in every project such as git init, git add, git commit, git push, git pull, and git fetch.
Set up Git repositories, clone an existing repository, and work with local and remote branches and tags.
Optimize workflows by leveraging the different workflow styles to suit the needs of the project.
Make your code linear and get better control over it with features such as Rebase and Blame.
Integrate external software into your project without affecting your app, with the help of Sub Modules.
TECHNIQUES

In this post, I’ll talk about the basic Git techniques that you must be familiar with before you join a team. I’ve listed them in an order that you’d logically follow to contribute to a repository, as the importance of each step is paramount. Let’s now jump into the list.

1. Cloning: Getting Started in a Team
If you’ve used Git for personal projects, you may only have initialized a project from scratch and added to it over time. When you’re working on an existing codebase, the first step is to clone the codebase into your local system. This enables you to work on your copy of the repository without any interference from other changes.

To clone a repository, run the git clone command, followed by the path to the repository:

git clone /path/to/repo
If your source doesn’t reside in the same system, you can SSH to a remote system and clone too:

git clone username@remote\_system\_ip:/path/to/repo/on/remote
If you’re cloning from a source on the Internet, you can simply add the URL:

git clone https://github.com/sdaityari/my\_git\_project.git
Whenever you’re cloning a repository, you’ve the choice of multiple protocols to connect to the source. In the GitHub example above, I’ve used the https protocol.

2. Managing Remotes in Git
Once you’ve cloned your repository, it still maintains a pointer to the source. This pointer is an example of a remote in Git. A remote is a pointer to another copy of the same repository. When you clone a repository, a pointer origin is automatically created which points to the source.

You can check a list of remotes in a repository by running the following command:

git remove -v
To add a remote, you can use the git remote add command:

git remote add remote\_name remote\_address
You can remove a remote using the git remote remove command:

git remote remove remote\_name
If you’d like to change the address of a remote, you can use the set-url command:

git remote set-url remote\_name new\_remote\_address
3. Branching in Git
The biggest advantage of Git over other version control systems is the power of its branches. Before I jump into the essentials of branching, you may be wondering what a branch is. A branch is a pointer to a commit in your repository, which in turn points to its predecessor. Therefore, a branch represents a list of commits in chronological order. When you create a branch, you effectively create only a new pointer to a commit. However, in essence, it represents a new, independent path of development.

If you’ve been working on your own project, you may never have consciously used branches. By default, Git uses the master branch for development. Any new commits are added to this branch.

Branching is necessary for Git to bifurcate lines of work in a project. At a single time, there may be many developers who are working on a variety of different problems. Ideally, these problems are worked on in different branches to ensure logical separation of new code until code review and merge.

To check a list of branches and the current active branch, run the following command:

git branch
To create a new branch, run the following command:

git branch new\_branch
Even though Git creates a new branch, notice that your active branch is still the old one. To start development in a new branch, run the following:

git checkout new\_branch
To create a new branch and change the active branch, run the following command:

git checkout -b new\_branch
To rename the current branch, run the following command:

git branch -m new\_renamed\_branch
Use the -D option to remove a branch:

git branch -D new\_renamed\_branch
Here’s a detailed guide on branching in Git.

4. Update your Local Repository: Merging
While we’ve checked the basics of branching in Git, the next logical step is to merge a branch into your base branch when you’ve finished working on a problem. To merge a branch, run the following command:

git checkout base\_branch
git merge new\_branch
While it may sound like an easy process, merging is potentially the most time-consuming process in Git, as it can give rise to conflicts.

5. Handle Conflicts
Imagine that you’re working on a file in a new branch. After you commit the changes, you request Git to merge your new branch with your base branch. However, the same part of the same file in the base branch has been updated since you created the new branch. How does Git decide which changes to keep and which changes to discard?

Git always tries to not lose any data in the process of a merge. If the changes to the same file were done in different parts of the file, you could get away by keeping both sets of changes. However, if Git is unable to decide which changes to keep, it raises a conflict.

When a conflict has been raised, running git status on your repository shows a list of files that were modified in both branches being merged. If you open any file with a conflict, you’d notice the following set of lines:

<<<<<<<< HEAD
...
...
========
...
...
>>>>>>>> new\_branch
The part of the file between <<<<<<<< HEAD and ======== contains that code which is present in the base branch. The lines of code between ======== and >>>>>>>> new_branch are present in the new_branch branch. The developer who’s merging the code has the responsibility to decide what part of the code (or a mix of both parts) should be included in the merge. Once edited, remove the three sets of lines shown, save the file, and commit the changes.

6. Synchronize Changes with the Remote
While we’ve discussed how to commit code in new branches, and merge it with the base branch, let’s now see how you can synchronize code with the remote. Before you can publish your changes to the remote, you need to update your local copy of the repository to account for any changes that may have occurred since your last update. To update changes from the remote, run the following command:

git pull remote remote\_branch:local\_branch
The git pull command first downloads the data from the remote and then merges with the local branch as specified in the command. Conflicts can arise while pulling changes from a remote too. In such a case, the last line in a conflict file would contain >>>>>>>> commit_hash instead of >>>>>>>> new_branch, where commit_hash would be the identifying hash for the commit being added to your branch.

To publish changes to the remote after merging with the latest code from the remote, use the git push command:

git push remote local\_branch:remote\_branch
7. Git on the Cloud: Forking
If your team works on the cloud, you’re introduced to an added concept called a fork. A fork is a copy of the central repository of the cloud under your username. You have write access to your fork, which is a safe place for you to push changes without affecting the original repository.

This affects the very technique step that I covered above. You clone your fork, so the origin of your local repository points to your fork on the cloud. How do you get the updates from the latest repository then? You need to manually add a remote, upstream, which points to the original repository.

While you can easily publish changes to your fork, how do you get new code accepted into the original repository? That brings us to the next step.

8. Code Reviews through Pull Requests
A pull request is a request to merge code from a branch to another. It’s a concept that has developed since cloud services for Git became popular. A pull request summarizes the comparison between the two branches in question and initiates a discussion between the developer and the organization’s admins.

A code review may culminate in more changes before it can be merged. When the admins are satisfied with the changes, it can be merged with the repository.

9. Know About Git Workflows
When you’re working alone on a single project, you’re probably using just a single branch. Unknowingly, you’re adhering to the centralized or trunk workflow, where all changes are made to a single branch.

The next, more complex workflow is the feature-branch workflow, where a single branch is attributed to each feature or bug fix. No development happens directly on the master or development branches.

A Git workflow that encompasses a wide range of situations is the Gitflow workflow. It has separate branches for development, features, releases and hotfixes.

Here’s a detailed guide on Git workflows.

10. Handle Large Files: Git LFS
While Git does a great job of handling text files, it’s unable to track changes in binary and executable files. While you can add such files to Git, it could potentially lead to a large repository size with an increase in the number of commits.

The solution is to use Git Large File Storage, which handles large binary files through Git. This tool stores these files on the cloud, and replaces them with text pointers. Here’s an implementation of using Git LFS to track Photoshop design files.