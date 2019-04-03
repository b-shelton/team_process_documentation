# Git and GitHub Overview

## What is Git?

Git is a version-control system that allows developers to collaborate together on files and projects. For our Data Science and Analytics teams, it is what we use to house, update, and peer review the scripts that we develop to produce analytic insights and products for our customers. Benefits using a system like this include:

- **Quality Assurance:** Requiring peer review of each others’ work ensures quality in our work products.
- **Collaboration:** A centralized location to house our teams’ scripts and work on them together allows developers to share ideas and logic that speed up time-to-delivery and improve consistency amongst deliverables.
- **Transparency:** Making our scripts (internally) publicly available allows us to easily reference the logic that we’ve developed when needing to discuss the processes with customers or other analytic developers.

## Remote and Local Git Environments

1. **Remote Environment:** Our remote Git environment is an Enterprise edition of [GitHub](https://github.com). It is a web interface where our team collaborates by creating projects, proposing new ideas or fixes, reviewing each others code enhancements, and accessing the latest production-grade scripts.

2. **Local Environment:** When analytics are being developed, they are written and saved in the user’s local environment (i.e., their personal machine or virtual computer), which is only accessible to the specific user. In the local environment, the project looks just like any other directory system with folders and files. Once a change has been developed and tested in the local environment, it is pushed to the remote environment for code review and included as part of the production-grade code accessible by all collaborators.

#### Communicating between Remote and Local Environments

There are many options to send information between the remote and local git environments. The organization-supported option is [Git Bash](https://git-scm.com/download/win). This application requires an I.T. install. Git Bash is a command-line shell where the developer uses linux-like syntax to execute commmands. If this idea is new to you, then it may sound more intimidating than it really is (more below)...

Another option that has been used in our organization is [Atom text editor](https://atom.io/), which can be installed directly by the user.

## Git Workflow

Let's take a moment to walk through the general components of the Git workflow at our organization. Note that all of the code used in the .gifs throughout this post can be found in this repo's [basic_git_commands.md](https://github.com/b-shelton/team_processes/git_processes/basic_git_commands.md) file.

![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/gitflow_single_branch.png)

### Create New Repo

Anytime you begin to develop a completely new product or work on a new analytics project, you'll want to contain all of the development information in a central location, including the code, documentation, and project plan. This project location in Git is called a _*repository*_ (repo). A new repo is generated on remotely on GitHub, under the "Repositories" tab of your user profile, as shown below.

![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/new_repo.gif)

Unless the subject matter you've been asked to work on is extremely confidential (e.g., provider fraud investigation), every repo should be initialized as a "public" repo and include a README.md file, as shown below. Making all of our repositories "public" allows for greater collaboration, while the README.md file is the place to contain general information about the content and context of the repository.

![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/readme_edit.gif)

Public repos are able to be accessed and read by anyone with an Enterprise GitHub account. In order for people to be able to engage with the repo (e.g., add issues, perform code reviews), they need to be added as a repository "Collaborator" under Settings > Collaborator, as shown below. Note that our GitHub server requires you to search for individuals by their GitHub username.

![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/collaborator.gif)

### Master Branch: Remote Environment

The master branch in a public repo on GitHub (i.e., the remote environment) is accessible by all Enterprise GitHub users and is considered production-grade quality. This means that any code or documentation that is included in the master branch should be peer-reviewed prior to "merging" to the master branch. To enforce this, you need to protect the master branch from people making updates directly to it. This is achieved through the "Protected branches" setting for the master branch under Settings > Branches, as shown below.

![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/branch_protect.gif)

### Master Branch: Local Environment

As previously mentioned, when adding new files or updating existing scripts to a repo for the first time, the work is completed outside of the remote master branch. The first step is to _*clone*_ (copy) the remote master branch to your local environment (e.g., your personal network drive) through the use of a Git communication tool like Git Bash. Again, the line of code to execute this command, as well as other pertinent commands to the Git workflow, are located in this repo's [basic_git_commands.md](https://github.com/b-shelton/team_processes/git_processes/basic_git_commands.md) file.

![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/git_clone.gif)

### FeatureX Branch: Local Environment

New work is never completed directly on the master branch. Instead, the user creates a new “branch” of the master repository to complete enhancements or bug fixes.

Think of the relationship between the master and feature branches like updating the recipe of a popular dish at a restaurant. Let’s imagine that the chef decides that she wants to make the current dish spicier. She is not going to just change the original recipe that is being served to customers (master version) without testing which new spices should be used and how much to add. Instead, the chef will continue to serve the original recipe to customers while she takes the recipe and experiments with it in the back kitchen (feature branch). Only after the chef is comfortable with the changes through rounds of experimentation and testing with her co-workers and/or a select group of tasters, will she make the decision to update the original recipe with the new, spicier version to be shared with all customers who order the dish.

Now back to the world of git version control. Much like the chef in our example, our team makes changes to the existing code by creating a feature branch of the repository, then edits that version instead of the master version of the repository. Once the developer is comfortable with the changes on the feature branch in the local environment, the feature branch is then _*pushed*_ to the the remote repository.

![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/git_push.gif)

### FeatureX Branch: Remote Environment

Once the new branch has been pushed to the remote repository (GitHub), a "Pull Request" is submitted in GitHub. This signifies that the feature's author is requesting to have the update merged to the master branch (thus, becoming part of the production-grade code).

![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/pull_request.gif)

### Code Review

Before any new code can be merged with the master branch in GitHub, it must go through a peer code review as part of the GitHub Pull Request. A full overview of the team's code review process can be found [here](https://github.com/b-shelton/team_processes/git_processes/code_review).

Upon successful completion of the code review process, FeatureX is allowed to be "merged" with the master branch, qualifying it as production-grade code.

## Expanding to Multiple Collaborators

The beauty of this process is that it allows for simultaneous development of different features, all being created on their own separate branches, and rolled into the remote repository's master branch, only after code review has been completed.

![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/gitflow_multiple_branches.png)
