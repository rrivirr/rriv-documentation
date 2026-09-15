Branch and Merging Strategy

# Summary

We use the a branch and commit strategy that relies on many small commits that are then squashed into larger, explicitly described units of work before they are merged through the pull request mechanism.

# Process

1. Developer clones the repository and wants to write code
2. Create a working feature branch for the work that is being done
	1. `git checkout main`
	2. `git checkout working-<feature name>`
3. As code is updated, make small commits for either clear units of change, or work in progress commits to capture unfinished work.
	1. `git commit ...`
4. *Always* push work from this working branch often, to ensure work is stored in the cloud and not lost
	1. `git push -u origin <branch name>` - the first time
	2. `git push` - every other time
5. Finish the feature or work that is being done
6. Now, create a new branch to be used to clean up the commit history
	1. `git checkout -b finished-<feature name>`
7. Clean up the the commit history using interactive rebase with squashing
	1. `git rebase -i <base commit>`
	2. Use `pick` or `squash` to combine commits
	3. Update the commit message so they follow the correct conventional commits format
8. Create a PR using the github cli
	1. `gh pr create`
9. Review the PR with other devs
10. Merge to main
