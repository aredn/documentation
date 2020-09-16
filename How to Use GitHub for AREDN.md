# How to Use GitHub
## Contributing Documentation to the AREDN Project


### Create Your GitHub Account

To contribute to the AREDN project you first must create your own GitHub account. This is free and easy to do by following these steps:

1. Open your web browser and navigate to the GitHub URL `https://github.com`.
2. Click the `Sign Up` button and enter a username, email, and password. We suggest using your callsign as the username.
3. On the GitHub website, click the `Sign In` button and enter your username or email, followed by your github password.
4. You can enter "aredn" into the search bar to find all repositories related to AREDN, or if you want to navigate directly to the AREDN documentation repository you can type this URL into your web browser: `https://github.com/aredn/documentation`.

### Understanding GitHub Workflow

The process of contributing and tracking changes to AREDN is circular. Code is maintained in the AREDN Master repository on GitHub. To contribute a potential documentation update, you must first FORK the AREDN master repository to your own GitHub account. You then CLONE your copy of the documentation from your GitHub repository to your own local computer. Make and test any changes you want to contribute using your local computer's copy of the documentation repository.

When you are satisfied with your changes, COMMIT them to your local computer's repository, then PUSH those local changes to your copy of the documentation on your own GitHub account. Finally, create a PULL REQUEST, which tells the AREDN development team that you would like your changes to be reviewed for inclusion in the AREDN Master repository.

![GitHub Workflow](_images/GitHub-docWorkflow.png)

#### One-time Repository Setup:

1. Login to your own GitHub account and navigate in your browser to `https://github.com/aredn/documentation`
2. Click the `Fork` button on the upper right side of the page.  You now have a copy of the AREDN documentation on your own GitHub account.
3. Go to your local computer and copy your fork of the AREDN documentation: `git clone https://github.com/myCall/documentation`
4. `cd documentation`  This directory contains your local copy of the AREDN documentation. The following commands will be executed while you are in this directory or its subdirectories.
5. `git remote add aredn https://github.com/aredn/documentation`  

Now your local environment knows about both the master documentation repository and your forked copy on your GitHub account.

#### Ongoing Development Cycle:

1. Update your local environment with the latest documentation changes from the rest of the community, which will include any changes you had previously submitted.  *Caution:*  never make changes directly on the `master` branch.  This will result in inconsistencies between the main repository and your repository, requiring a force-remove of any changes you have made.
	1. `git checkout master`
	2. `git pull aredn master`
2. Create a git branch to fix a bug or implement a new feature:
	1. `git checkout -b my-new-doc-item`
3. Make your changes and test them.
4. When ready to submit changes, check to see whether they can be merged with documentation others have recently submitted. In GitHub terminology, “pull” down the latest changes and “rebase” or move your changes on top of the latest. In this process you might find conflicts with changes someone else has submitted, making further merge edits necessary.
	1. `git stash` to stash the changes still in process.
	2. `git checkout master`
	3. `git pull aredn master`
	4. `git checkout my-new-doc-item`
	5. `git rebase master` to move your branch and changes on top of the latest changes others have submitted.
	6. `git stash pop` to reapply your stashed changes
	7. Resolve any conflicts that need to be merged if warned in the step above.
	8. Final build and validation that your changes work on top of the latest changes from other contributors.
5. `Commit` your changes to your local repository, then `Push` the changes to your own GitHub repository.
	1. `git add any-changed-files` (stage changes for commit)
	2. `git commit` (commit changes with a meaningful commit message)
	3. `git push origin my-new-doc-item`
6. Create a `Pull Request` (PR) to the AREDN master repository by browsing to `github.com/myCall/documentation`, then select the my-new-doc-item branch. Click the `New Pull Request` button to generate your Pull Request. Others can now review your changes, test them, and give feedback. If feedback is given and you need to make changes, go back to step 3.
7. Once your changes have been accepted into the AREDN master repository, you can delete your branch:
	1. On your local repository: `git branch -D my-new-doc-item`
	2. On your forked copy of your GitHub repository: `git push origin --delete my-new-doc-item`

You can continue contributing new documentation by beginning the cycle again starting with step 1.
