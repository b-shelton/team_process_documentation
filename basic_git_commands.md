If you are new to Git, I would recommend starting with this repository's [git_overview.md](https://github.com/b-shelton/team_processes/git_processes/git_overview.md) post for a high-level understanding of how the environment is built and used on the Data Science and Analytics team.

I would then highly-recommend watching Corey Schafer's [Git Tuturial for Beginners](https://www.youtube.com/watch?v=HVsySz-h9r4), which is a wonderful introduction to the command lines used with Git. Two small notes about Corey's video:
- Our team's Git chosen Git command-line shell is Git Bash, which can requires an I.T. help desk ticket to "Install Git Client, including Git Bash" if you don't already have it installed.
- The user name you should use when logging in is your GitHub account user name (e.g., `bshelt`) instead of your full name like Corey's video shows (e.g., `Brandon Shelton`).
- Our process merges code from a feature branch to the master branch in GitHub, only after a formal code review. In Corey's video, he shows how to merge in the command line, which is not what we do.

After reviewing our team's Git Workflow process and Corey's great introduction to Git video, the code in this post will come in handy as friendly reminders as you are getting ramped up. Happy version controlling!

## Git Command Line Cheat Sheet

Once Git Client has been installed on your machine, you can open Git Bash by searching in your Windows task bar for "Git Bash".

In Git Bash, sign-in with your GitHub Enterprise credentials (you only have to do this the first time).
```
git config --global user.name <yourusername>
git config --global user.email <youruseremail>
```

Change to the correct directory in the terminal where you want the repository to land. Example:
```
cd ~/repo_dir
```


Download the GitHub repository:
```
git clone https://github.com/path_to/repository
```

Move into the new directory:
```
cd repository
```



### UPDATE YOUR LOCAL REPOSITORY FROM GITHUB REMOTE

If you already have a copy of the GitHub remote repo on your local machine,
then use the command line in this section to update the local version
to reflect the most current version on GitHub.


To pull all updates from remote to local (need to be in the correct directory for this to work):
```
git pull
```


### BRANCHING FROM ORIGIN REPOSITORY

This section allows you to branch off of a repository and make changes that are then proposed to the repo's owner
for either approval or further inquiry on GitHub.


To create a new branch use git branch:
```
git branch feature1
```

Switch to the new branch:
```
git checkout feature1
```

_*Note: Unless you are intentionally working in a complex branching system, be sure to always create a new feature branch from the master branch, not another feature branch!*_

After you make your updates in the new branch, switch back to the master branch and do a new pull to ensure that there haven't been any changes from others on the master branch if there have, then you need to merge the updated master with your new branch:
```
git checkout master
git pull
git checkout feature1
```

Only needed if there has been a change on the master:
```
git merge master
```

Commit and push the new file
```
git status
git add -A
git commit -m "<proposed update message here>"
git push --set-upstream origin feature1
```

Once the push has been completed, create a new pull request on GitHub.

After the pull request has been merged, then checkout the master branch locally, pull the updates to the local master, and delete the feature branch.
```
git checkout master
git pull
git branch -d feature1
```
