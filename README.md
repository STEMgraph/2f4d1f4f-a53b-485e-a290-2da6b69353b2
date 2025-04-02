<!---
{
  "depends_on": [],
  "author": "Tabea Röthemeyer",
  "first_used": "2025-04-12",
  "keywords": ["learning", "exercises", "education", "practice"]
}
--->

# Git: Branch and Merge Conflicts

## 1) Introduction
When working on code, different tasks occur. There is this bugfix (a bug is a problem in the code) that needs to be done. But also, there is a new feature (new code that adds more functionality) that we want to work on. To separate different histories of developemnt, Git introduces branches. A branch is a special, named pointer to a certain commit. This is the latest commit on the branch. 

Git commits usually have an ancestor (except for the first commit in a repo and in the case of unrelated histories, but fear not, this is mentioned for completeness). When we create a branch, we do the following
```
git status
git checkout -b <new-branchname>
git status
```
With the checkout command, we create a new branch starting from the current commit and we switch our context. In other words, when we add a new commit, git will update the new branch instead of the one we were previously on. When you test this, compare the output of `git status`. This command helps you to understand what your current Git context is.

Once our development is complete, we want to add changes to the main branch of the repo. It is called that way because all relevant changes are put there. The operation to achieve this is called *merge*. When merging two branches, Git creates a new commit that combines the content of both branches. While this is trivial when you don't have new history in your main branch, it becomes more complicated when you have independent changes on both branches.

Git has merge strategies that help to combine the code. However, when GIt does not know which changes to favor, there are merge conflicts.

Git will mark the changes where you need to decide what to keep. This task can be complex and take some time.

### 1.1) Further Readings and Other Sources
- [Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

## 2) Tasks
1. **Create a new branch**
2. **Checkout an existing branch**
3. **Create merge conflict**: Create a file and add a word. Then replace the word with a different one. Then checkout main and replace the word with a third one. Try to merge your branches by resolving the merge conflict.


## 3) Questions
1. Find another command that creates a new command. Compare it with the proposed checkout command.
2. How can you compare the changes of two branches before merging?
3. If the merge does not work, how can you reset your work?

## 4) Advice
Merge conflicts will be hard no matter how experienced you are. It might even be the case that you need to add code in order to make the merge work. If you are comfortable with the syntax Git uses to mark conflicting changes, this taks becomes a little easier. Also, your work is never lost! Whatever has been committet is kept by Git for at least 2 weeks even if the commit is not part of a branch anymore.

