---
title: Tracking Changes
teaching: 20
exercises: 0
questions:
- "How do I record changes in Git?"
- "How do I check the status of my version control repository?"
- "How do I record notes about what changes I made and why?"
objectives:
- "Go through the modify-add-commit cycle for one or more files."
- "Explain where information is stored at each stage of Git commit workflow."
keypoints:
- "`git status` shows the status of a repository."
- "Files can be stored in a project's working directory (which users see), the staging area (where the next commit is being built up) and the local repository (where commits are permanently recorded)."
- "`git add` puts files in the staging area."
- "`git commit` saves the staged content as a new commit in the local repository."
- "Always write a log message when committing changes."
---

Let's edit our file `index.md`. We'll use `nano` to edit the file;
you can use whatever editor you like.

~~~
$ nano index.md
~~~
{: .bash}

Type the text below into the `index.md` file:

~~~
Two types of data will be generated
~~~
{: .output}

`index.md` now contains a line under the first header. We can see the contents of the whole document by running:

~~~
$ cat mars.txt
~~~
{: .bash}

~~~
# Data description
Two types of data will be generated

# Roles and responsibilities

# Data standards and metadata

# Storage and security

# Access and data sharing

# Archiving and preservation

Repository with source code [here](https://github.com/clarallebot/GRAD521_DMPtemplate)
~~~
{: .output}

If we check the status of our project again,
Git tells us that it's noticed the change:

~~~
$ git status
~~~
{: .bash}

~~~
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   index.md

no changes added to commit (use "git add" and/or "git commit -a")
~~~
{: .output}


The last line is the key phrase:
"no changes added to commit".
We have changed this file,
but we haven't told Git we will want to save those changes
(which we do with `git add`)
nor have we saved them (which we do with `git commit`).
So let's do that now. 

~~~
$ git add index.md
~~~
{: .bash}

And check the status
~~~
$ git status
~~~
{: .bash}

~~~
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   index.md
~~~
{: .output}

Git now knows what to save, the changes we just submitted in `index.md` are recorded in a staging area. 
But it hasn't recorded these changes as a commit yet.
To get it to do that,
we need to run one more command:

~~~
$ git commit -m "Start descriptions of the dataset"
~~~
{: .bash}

~~~
[master f3f9619] Start descriptions of the dataset
 1 file changed, 1 insertion(+)
~~~
{: .output}

When we run `git commit`,
Git takes everything we have told it to save by using `git add`
and stores a copy permanently inside the special `.git` directory.
This permanent copy is called a [commit]({{ page.root }}/reference/#commit)
(or [revision]({{ page.root }}/reference/#revision)) and its short identifier is `f3f9619`
(Your commit may have another identifier.)

We use the `-m` flag (for "message")
to record a short, descriptive, and specific comment that will help us remember later on what we did and why.
If we just run `git commit` without the `-m` option,
Git will launch a text editor so that we can write a longer message.

[Good commit messages][commit-messages] start with a brief (<50 characters) summary of
changes made in the commit.  If you want to go into more detail, add
a blank line between the summary line and your additional notes.

Let's make another change to our file. At the bottom of the file we have a link to the repository. But right now the link goes to Clara's repository. Change it so that it goes to your repository. 

~~~
$ nano index.md
~~~
{: .bash}

~~~
# Data description
Two types of data will be generated

# Roles and responsibilities

# Data standards and metadata

# Storage and security

# Access and data sharing

# Archiving and preservation

Repository with source code [here](https://github.com/username/GRAD521_DMPSurname)
~~~
{: .bash}

It is good practice to always review
our changes before saving them. We do this using `git diff`.
This shows us the differences between the current state
of the file and the most recently saved version:

~~~
$ git diff
~~~
{: .bash}

~~~
diff --git a/index.md b/index.md
index 322d170..c99e98b 100644
--- a/index.md
+++ b/index.md
@@ -11,4 +11,4 @@ Two types of data will be generated
 
 # Archiving and preservation
 
-Repository with source code [here](https://github.com/clarallebot/GRAD521_DMPtemplate)
+Repository with source code [here](https://github.com/username/GRAD521_DMPSurname)
~~~
{: .output}

The output is cryptic because
it is actually a series of commands for tools like editors and `patch`
telling them how to reconstruct one file given the other.
If we break it down into pieces:

1.  The first line tells us that Git is producing output similar to the Unix `diff` command
    comparing the old and new versions of the file.
2.  The second line tells exactly which versions of the file
    Git is comparing;
    `322d170` and `c99e98b` are unique computer-generated labels for those versions.
3.  The third and fourth lines once again show the name of the file being changed.
4.  The remaining lines are the most interesting, they show us the actual differences
    and the lines on which they occur.
    In particular,
    the `+` marker in the first column shows where we added a line. The `-` marker shows where we deleted a line. 

After reviewing our change, it's time to commit it:

~~~
$ git commit -m "Change link to Repository"
$ git status
~~~
{: .bash}

~~~
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
Changes not staged for commit:
	modified:   index.md

no changes added to commit
~~~
{: .output}

Whoops:
Git won't commit because we didn't use `git add` first.
Let's fix that:

~~~
$ git add index.md
$ git commit -m "Change link to Repository"
~~~
{: .bash}

~~~
[master d407efb] Change link to Repository
 1 file changed, 1 insertion(+), 1 deletion(-)
~~~
{: .output}

Git insists that we add files to the set we want to commit
before actually committing anything. This allows us to commit our
changes in stages and capture changes in logical portions rather than
only large batches.
For example,
suppose we're adding a few citations to our supervisor's work
to our thesis.
We might want to commit those additions,
and the corresponding addition to the bibliography,
but *not* commit the work we're doing on the conclusion
(which we haven't finished yet).

To allow for this,
Git has a special *staging area*
where it keeps track of things that have been added to
the current [change set]({{ page.root }}/reference/#change-set)
but not yet committed.

> ## Staging Area
>
> If you think of Git as taking snapshots of changes over the life of a project,
> `git add` specifies *what* will go in a snapshot
> (putting things in the staging area),
> and `git commit` then *actually takes* the snapshot, and
> makes a permanent record of it (as a commit).
> If you don't have anything staged when you type `git commit`,
> Git will prompt you to use `git commit -a` or `git commit --all`,
> which is kind of like gathering *everyone* for the picture!
> However, it's almost always better to
> explicitly add things to the staging area, because you might
> commit changes you forgot you made. (Going back to snapshots,
> you might get the extra with incomplete makeup walking on
> the stage for the snapshot because you used `-a`!)
> Try to stage things manually,
> or you might find yourself searching for "git undo commit" more
> than you would like!
{: .callout}

![The Git Staging Area](../fig/git-staging-area.svg)


Let's look at the history of what we've done so far:

~~~
$ git log
~~~
{: .bash}

~~~
commit d407efb81ac0100ad919f92021f6134ca161baf9
Author: Clara Llebot <clara.llebot@oregonstate.edu>
Date:   Wed Jan 30 17:18:43 2019 -0800

    Change link to Repository

commit f3f9619847e3421700dc073c1769591f7f9b7cec
Author: Clara Llebot <clara.llebot@oregonstate.edu>
Date:   Wed Jan 30 17:09:58 2019 -0800

    Start descriptions of the dataset
~~~
{: .output}

`git log` lists all commits made to a repository in reverse chronological order. The listing for each commit includes the commit's full identifier (which starts with the same characters as the short identifier printed by the `git commit` command earlier), the commit's author, when it was created, and the log message Git was given when the commit was created.

The list shows actually more commits than just the two we just made. It shows all the changes that I made when I was creating the repository. When we imported the repository we imported not just the files, but also the history of the files.  

Now check our status:

~~~
$ git status
~~~
{: .bash}

~~~
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
nothing to commit, working tree clean
~~~
{: .output}

The working tree is clean and we have nothing to commit, but we see a message saying that the branch is ahead of origin/master. `origin` is a local nickname for your remote repository that is set by default by Git. Git knows what the remote repository is because we set that up when we cloned the repository. If you had started the repository locally in your computer first, you would have to set up the origin repository. What the sentence means is that git knows that what we have made changes on our local repository that are not in GitHub. Our local branch is ahead of the remote branch. Let's see how to fix that. 

> ## Paging the Log
>
> When the output of `git log` is too long to fit in your screen,
> `git` uses a program to split it into pages of the size of your screen.
> When this "pager" is called, you will notice that the last line in your
> screen is a `:`, instead of your usual prompt.
>
> *   To get out of the pager, press `q`.
> *   To move to the next page, press the space bar.
> *   To search for `some_word` in all pages, type `/some_word`
>     and navigate throught matches pressing `n`.
{: .callout}

> ## Limit Log Size
>
> To avoid that `git log` cover all your terminal screen you can
> limit the numbers of commit that Git will list by using `-N`
> where `N` is the number of commits that you want to receive
> the information. For example, if you only want the information
> from the last commit you can use
>
> ~~~
> $ git log -1
> ~~~
> {: .bash}
> 
> ~~~
> commit 005937fbe2a98fb83f0ade869025dc2636b4dad5
> Author: Vlad Dracula <vlad@tran.sylvan.ia>
> Date:   Thu Aug 22 10:14:07 2013 -0400
>
>    Discuss concerns about Mars' climate for Mummy
> ~~~
> {: .output}
>
> You can also reduce the quantity of information using the
> `--oneline` option:
>
> ~~~
> $ git log --oneline
> ~~~
> {: .bash}
> ~~~
> * 005937f Thoughts about the climate
> * 34961b1 Concerns about Mars's moons on my furry friend
> * f22b25e Starting to think about Mars
> ~~~
> {: .output}
>
> You can also combine the `--oneline` options with others. One useful
> combination is
>
> ~~~
> $ git log --oneline --graph --all --decorate
> ~~~
> {: .bash}
> ~~~
> * 005937f Thoughts about the climate (HEAD, master)
> * 34961b1 Concerns about Mars's moons on my furry friend
> * f22b25e Starting to think about Mars
> ~~~
> {: .output}
{: .callout}

To recap, when we want to add changes to our repository,
we first need to add the changed files to the staging area
(`git add`) and then commit the staged changes to the
repository (`git commit`):

![The Git Commit Workflow](../fig/git-committing.svg)

> ## Choosing a Commit Message
>
> Which of the following commit messages would be most appropriate for the
> last commit made to `mars.txt`?
>
> 1. "Changes"
> 2. "Added line 'But the Mummy will appreciate the lack of humidity' to mars.txt"
> 3. "Discuss effects of Mars' climate on the Mummy"
>
> > ## Solution
> > Answer 1 is not descriptive enough,
> > and answer 2 is too descriptive and redundant,
> > but answer 3 is good: short but descriptive.
> {: .solution}
{: .challenge}

> ## Committing Changes to Git
>
> Which command(s) below would save the changes of `myfile.txt`
> to my local Git repository?
>
> 1. `$ git commit -m "my recent changes"`
>
> 2. `$ git init myfile.txt`  
>    `$ git commit -m "my recent changes"`
>
> 3. `$ git add myfile.txt`  
>    `$ git commit -m "my recent changes"`
>
> 4. `$ git commit -m myfile.txt "my recent changes"`
>
> > ## Solution
> >
> > 1. Would only create a commit if files have already been staged.
> > 2. Would try to create a new repository.
> > 3. Is correct: first add the file to the staging area, then commit.
> > 4. Would try to commit a file "my recent changes" with the message myfile.txt.
> {: .solution}
{: .challenge}

> ## Committing Multiple Files
>
> The staging area can hold changes from any number of files
> that you want to commit as a single snapshot.
>
> 1. Add some text to `mars.txt` noting your decision
> to consider Venus as a base
> 2. Create a new file `venus.txt` with your initial thoughts
> about Venus as a base for you and your friends
> 3. Add changes from both files to the staging area,
> and commit those changes.
>
> > ## Solution
> >
> > First we make our changes to the `mars.txt` and `venus.txt` files:
> > ~~~
> > $ nano mars.txt
> > $ cat mars.txt
> > ~~~
> > {: .bash}
> > ~~~
> > Maybe I should start with a base on Venus.
> > ~~~
> > {: .output}
> > ~~~
> > $ nano venus.txt
> > $ cat venus.txt
> > ~~~
> > {: .bash}
> > ~~~
> > Venus is a nice planet and I definitely should consider it as a base.
> > ~~~
> > {: .output}
> > Now you can add both files to the staging area. We can do that in one line:
> >
> > ~~~
> > $ git add mars.txt venus.txt
> > ~~~
> > {: .bash}
> > Or with multiple commands:
> > ~~~
> > $ git add mars.txt
> > $ git add venus.txt
> > ~~~
> > {: .bash}
> > Now the files are ready to commit. You can check that using `git status`. If you are ready to commit use:
> > ~~~
> > $ git commit -m "Wrote down my plans to start a base on Venus"
> > ~~~
> > {: .bash}
> > ~~~
> > [master cc127c2]
> > Wrote down my plans to start a base on venus
> > 2 files changed, 2 insertions(+)
> > ~~~
> > {: .output}
> > ~~~
> {: .solution}
{: .challenge}

> ## Author and Committer
>
> For each of the commits you have done, Git stored your name twice.
> You are named as the author and as the committer. You can observe
> that by telling Git to show you more information about your last
> commits:
>
> ~~~
> $ git log --format=full
> ~~~
> {: .bash}
>
> When commiting you can name someone else as the author:
>
> ~~~
> $ git commit --author="Vlad Dracula <vlad@tran.sylvan.ia>"
> ~~~
> {: .bash}
>
> Create a new repository and create two commits: one without the
> `--author` option and one by naming a colleague of yours as the
> author. Run `git log` and `git log --format=full`. Think about ways
> how that can allow you to collaborate with your colleagues.
>
> > ## Solution
> >
> > ~~~
> > $ git add me.txt
> > $ git commit -m "Updated Vlad's bio." --author="Frank N. Stein <franky@monster.com>"
> > ~~~
> > {: .bash}
> > ~~~
> > [master 4162a51] Updated Vlad's bio.
> > Author: Frank N. Stein <franky@monster.com>
> > 1 file changed, 2 insertions(+), 2 deletions(-)
> >
> > $ git log --format=full
> > commit 4162a51b273ba799a9d395dd70c45d96dba4e2ff
> > Author: Frank N. Stein <franky@monster.com>
> > Commit: Vlad Dracula <vlad@tran.sylvan.ia>
> >
> > Updated Vlad's bio.
> >
> > commit aaa3271e5e26f75f11892718e83a3e2743fab8ea
> > Author: Vlad Dracula <vlad@tran.sylvan.ia>
> > Commit: Vlad Dracula <vlad@tran.sylvan.ia>
> >
> > Vlad's initial bio.
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

[commit-messages]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
