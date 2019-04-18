# Git Workflow

## General Notes

Except in very extreme situations, all developers should work in branches and get peer code review of the changes before deploying code.

## Starting work on a task

```bash
# Make sure you start in the "master" branch
git checkout master

# Get any new updated changes from Github
git pull

# Create a new branch to work from prefixed with the Jira ticket number
git checkout -b WEB-123-some-helpful-name

# Make your changes, committing early and ofter:
git add some-file.js
git commit -m'Add someFunction to do foo bar'

# When you are ready for code review, push your branch to Github
git push origin WEB-123-some-helpful-name
```

Now, create a Pull Request on 

## Updating a branch

If your branch gets out of sync with master, the easiest thing to do is merge master into your branch:

```bash
git merge origin/master
```

### Rebasing

**Proceed with caution!**

For advanced git users, you can also use rebase to update your local version if you know what you are doing and don't want a lot of local merge conflicts.

You won't want to do this if you are collaborating on a branch with someone however

```bash
# Get the most up to date code from the remote repository
git fetch

# Update your local branch by stashing your changes, updating your base branch and then apply your commits on top of them:
git rebase origin/master
```

If there are merge conflicts, you will need to:

- Review the change, deciding which change to keep
- `git add` the files you changed
- `git rebase --continue` to apply the next commit

If you ever feel like you messed something up, do a `git rebase --abort` to exit out of the rebase and ask for help
