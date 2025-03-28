Every project starts with a `master` branch considered as the main
It can be copied (creating a reference to the specific commit) and work on it independently of the original branch by using `git branch <branch_name>` or `git checkout -b <branch_name>`

`git checkout <branch_name>` is used to navigate between the branches

Once it is ready, the branch can be put back to the original branch. Git `rebase` and `merge` allows to integrate changes from one branch into another
# Merging and rebasing
Before performing merge or rebase, it is important to ensure that the current branch is sync with the remote branch and that there are no conflicts between the changes made in both branches
#### Merge
To be able to call `merge` we need to `checkout` to the target branch

When performing `git merge <feature_branch>` (from our master branch, git creates a new commit that merges the changes from the feature branch into the target branch

The commit was made has two parent commits, one from each branch, and the resulting Git history shows the entire branch structure and all the merge points

The merge can happen all in one or by cherry-picking specific commits
#### Rebase
To be able to call `rebase` we need to `checkout` to the feature branch

Moves a branch to a new base commit
Instead of creating a new merge commit `git rebase <target_branch>`  replays the changes from the feature branch on top of the target branch one-by-one

The result is a linear git history as if the feature branch was created on top of the target branch, with no merge points

It is important to know that it can be dangerous if it is used improperly, as it can rewrite the Git history in a way that makes it difficult to track down bugs or recover lost code
## Orphaned branch
We call a branch orphaned if the commit where it was created had been deleted before merging/rebasing back to the original branch

In this case the branch does not exist in the branch history of the repository, but it will still contain the changes made in the original commit

It can still be merged back into the main branch, but it may result in a merge conflict, as the changes in the new branch may not be compatible with the changes made in the main branch after the original commit was deleted
## Conflicts
If we modify the same parts of the same files on two different branches, then merging the branches may result in a merge conflict. This situation can occur when the changes cannot be combined automatically, and manual intervention is required to resolve the conflict and complete the merge

Affected files need to be resolved manually. The parts that cannot be automatically merged are encapsulated in a special syntax in Git source files
```git
<<<<<<< HEAD
The content of the conflicting file on the current branch
=======
The content of the conflicting file on the branch that we want to merge
>>>>>>> <feature_brach>
```
Resolved files must be added to the staging area using `git add` and then the changes need to be committed
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE1NzIzNDU4MF19
-->