<!---
{
  "id": "2f4d1f4f-a53b-485e-a290-2da6b69353b2",
  "teaches": "Git: Branch and Merge Conflicts",
  "depends_on": [],
  "author": ["Tabea Röthemeyer","Stephan Bökelmann"],
  "first_used": "2025-04-12",
  "keywords": ["git","merge","branch"]
}
--->

# Git: Branch and Merge Conflicts

## 1) Introduction
When working on code, different tasks occur. There is this bugfix (a bug is a problem in the code) that needs to be done. But also, there is a new feature (new code that adds more functionality) that we want to work on. To separate different histories of developemnt, Git introduces branches. A branch is a special, named pointer to a certain commit. This is the latest commit on the branch. 

Git commits usually have an ancestor (except for the first commit in a repo and in the case of unrelated histories, but fear not, this is mentioned for completeness). When we create a branch, we do the following

```sh
git status
git checkout -b <new-branchname>
git status
```

With the checkout command, we create a new branch starting from the current commit and we switch our context. In other words, when we add a new commit, git will update the new branch instead of the one we were previously on. When you test this, compare the output of `git status`. This command helps you to understand what your current Git context is.

Once our development is complete, we want to add changes to the master branch of the repo. It is called that way because all relevant changes are put there. The operation to achieve this is called *merge*. When merging two branches, Git creates a new commit that combines the content of both branches. While this is trivial when you don't have new history in your master branch, it becomes more complicated when you have independent changes on both branches, or even competing changes in the same file, in the same line. 

Git has merge strategies that help to combine the code. However, when Git does not know which changes to favor, there are merge conflicts.

Git will mark the changes where you need to decide what to keep. This task can be complex and take some time.

### 1.1) Further Readings and Other Sources
- [Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

## 2) Tasks
1. **Create a new Repository**: Navigate to your home directory `cd`. Make a new directory, navigate into it and [initialize it as a git-repository](https://github.com/STEMgraph/474307f2-a30c-4639-9379-298bf1a4c00b). 
2. **Add a Commit**: Create a new file with some content. If you need some text, just run `wget -qO- "https://baconipsum.com/api/?type=meat-and-filler&paras=2&format=text" > lorem.txt`; This will query an online API and redirect the downloaded text into `lorem.txt`. Add the file to the staging area and commit it to the repository. 

<details>
    <summary>Forgot how to stage and commit?</summary>
    This is not a problem and you will get used to it:
    ```sh
    git add lorem.txt
    git commit -m "Add new lorem ipsum text"
    ```
</details>

3. **Create a new branch**: Now we want to create a branch on which we want to try some changes in our file: `git checkout -b my_new_branch`. Open `lorem.txt` with your favorite editor (that's a synonym for [vim](https://github.com/STEMgraph/2c7334b3-b07d-48d6-a562-79072d8e166e) obviously) and change some words. Stage and commit the changes. 
4. **Checkout out Default Branch again**: Run `git branch`. You should see your default branch and `my_new_branch`. Use `git checkout <default_branch_name>` to switch back. Inspect the file `lorem.txt`. 
5. **Merge your Branches**: To merge the changes on your branch into your current working directory, run `git merge my_new_branch`. This will pull the branches changes into your branch.
6. **Another new Branch**: Create another new branch, change a line in `lorem.txt` and commit it to the branch. Checkout the default branch again, change the same line in `lorem.txt`, but with other words and commit that as well. Now we have a different situation. Both branches modified the old point at which they branched. Call `git merge <new branch name>`. You will be confronted with a diagnostics message indicating a conflict:
```sh
Auto-merging lorem.txt
CONFLICT (content): Merge conflict in lorem.txt
Automatic merge failed; fix conflicts and then commit the result.
```
7. **Resolving the conflict**: Since git can't possibly know, which changes are the correct ones when these are conflicting, we now have to resolve this manually. Open `lorem.txt` with `vim`. You will find indicators and the different content of both branches in the same file now:
```sh
<<<<<<<< HEAD
Here is the master text
=======
Here is the feature-branch text
>>>>>>> new
```
Delete the indicators and the text that shouldn't be in the merged version. Save the file, run `git status` and `git commit`. You successfully resolved the merge conflict!


## 3) Questions
1. Find another command that creates a new branch. Compare it with the proposed checkout command.
2. How can you compare the changes of two branches before merging?
3. If the merge does not work, how can you reset your work?

## 4) Advice
Merge conflicts will be hard no matter how experienced you are. It might even be the case that you need to add code in order to make the merge work. If you are comfortable with the syntax Git uses to mark conflicting changes, this taks becomes a little easier. Also, your work is never lost! Whatever has been committet is kept by Git for at least 2 weeks even if the commit is not part of a branch anymore.

