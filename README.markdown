How to GIT awesome ?
=============
A fun and interactive git and github tutorial
Modified from Kuahyeow's tutorial for DataTas

#### Presented by Nic Pittman & Jake Weis


Aims for Today:

- What is Git (version control) and why should I use it (and some repository examples)?
- Command line Git vs GUI Git, which one to choose?
- Installing Git
- Using Github Part 1
- How does repository workflow work (add, commit, push, branching, merging)
- How to create a new repository
- How to back up / or find old data.
- Using Github Part 2 (Pull requests, collaboration, publishing scientific code)


What is GIT?
============
Git is a *distributed* **version control** system [1]

[1] <a href="http://git-scm.com/about">http://git-scm.com/about</a>

Getting Git
-----------

We assume of course you have Git installed,
(hopefully \>= 1.7.0).

If you don't you can install it from downloads on the git homepage or you can
install [Github's git GUI](https://help.github.com/articles/set-up-git/).

Setup
-----

First thing to do is to setup your identity. This identifies you to
other people who download the project.

    $ git config --global user.name "Your Name"
    $ git config --global user.email your.email@example.com

As a helpful step, you may want to set Git to use your favourite editor

    $ git config --global core.editor vim

***Git GUI***

*If you prefer to Git using a GUI/software, you can go through this tutorial using any Git software you fancy. I (Jake) would suggest [Fork](https://git-fork.com/), since this is what I use most of the time and will be best able to troubleshoot. Fork is free to use and occasionally asks you to buy the paid version. This seems to be optional as far as I can tell. It's only 50USD (one-time payment), so do consider buying it and supporting the developers once you feel like you'll continue using it on a regular basis. Fork users: Watch out for cursive text starting with* ***&rarr; Fork instructions: ...*** *These will be yours to follow.*

Using Github Part 1
==================
To be able to share, we’ll need a server to host our git repositiories.
GitHub (<a href="https://github.com/">github.com</a>) is probably the
easiest place to begin with.

Login or sign up with GitHub
----------------------------

If you've already got an account you can skip on to creating the repo on
github, or forking this repository and cloning it down to your local machine.

Otherwise...

Go <a href="https://github.com/signup">sign up for an account</a> at
GitHub; Or login into your GitHub account if you had previously signed
up.

Hint: You may need to setup git cache your GitHub password - see
<a href="https://help.github.com/articles/set-up-git">https://help.github.com/articles/set-up-git</a>

Then come back here, we’ll wait.

***&rarr; Fork instructions:*** *Sign up to your GitHub account in Fork: **Menu bar > Fork > Accounts.** *This will let you easily clone repositories from your GitHub account.*

Create your first GitHub repository (Fork this one!)
-----------------------------------------------------

A repository (repo) is a place where you would store your code.
Try forking this repository.

Go to [this tutorial](https://help.github.com/articles/fork-a-repo)
Then come back here, we’ll wait.


While we are here ... Optional and advanced but very useful (SSH keys)
--------------------------------------------------------
Lets set up SSH keys between github and our laptop so we can pull or push without having to put in our password.

Github > Settings > SSH and GPG keys > New SSH Key and follow the links provided for help.
https://docs.github.com/articles/generating-an-ssh-key/
https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent



Starting your git journey
========================

First, clone this repository:

    $ git clone https://github.com/datatas/git-workshop.git

You may want to fork (create your own copy of) the project on github and
clone from your own repo. You can find the fork button at the top right of
the screen on a github repository, or more help about doing that [here](https://help.github.com/articles/fork-a-repo/).

***&rarr; Fork instructions:*** *Cloning in Fork: Menu bar > File > Clone (Shift+CMD+N). If you select your GitHub account, you will see all of your repositories on GitHub. Select the workshop repository you forked during the previous step. Choose the location you want your repository to be stored in and hit* ***Clone***.

Once you have cloned your repository, you should now see a directory
called `git-workshop`. This is your `working directory`

    $ cd git-workshop
    $ ls

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff.

For the curious, you should also see the `.git` subdirectory. This is
where all your repository’s data and history is kept.

    $ ls -a .git

You will see :

    branches  config  description  HEAD  hooks  info  objects  refs

The staging area
----------------

Now, let’s try adding some files into the project. Create a couple of
files.

Let’s create two files named `bob.txt` and `alice.txt`.

    $ touch alice.txt bob.txt

***&rarr; Fork instructions:*** *Either create the files as described above or do it using a text editor.*

Let’s use a mail analogy.

In Git, you first add content to the `staging area` by using `git add`.
This is like putting the stuff you want to send into a cardboard box.
You finalize the process and record it into the git index by using
`git commit`. This is like sealing the box - it’s now ready to send.

Let’s add the files to the staging area

    $ git add alice.txt bob.txt

***&rarr; Fork instructions:*** *Navigate to Local Changes (top of the side bar). Here you will see any changed, added or deleted files in the 'Unstaged section'. Click on a file to take a look at the changes. Add Alice and Bob to the staging area by selecting both files and clicking 'Stage' (CMD+S). You should see the files moving from unstaged to staged. Yey!*

Committing
----------

You are now ready to commit. The `-m` flag allows you to enter a message
to go with the commit at the same time.

    $ git commit -m "I am adding two new files"

***&rarr; Fork instructions:*** *Add a commit subject and description to let future-you know what this commit was about and hit 'Commit' (Bottom right corner or SHIFT+CMD+C). The files will now leave the staging area.*

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Let’s see what just happened
----------------------------

We should now have a new commit. To see all the commits so far, use
`git log`

    $ git log

The log should show all commits listed from most recent first to least
recent. You would see various information like the name of the author,
the date it was commited, a commit SHA number, and the message for the
commit.

You should also see your most recent commit, where you added the two new
files in the previous section. However git log does not show the files
involved in each commit. To view more information about a commit, use
`git show`.

    $ git show

You should see something similar to:

    commit 5a1fad96c8584b2c194c229de7e112e4c84e5089
    Author: kuahyeow
    Date:   Sun Jul 17 19:13:42 2011 +1200

        I am adding two new files

    diff --git a/alice.txt b/alice.txt
    new file mode 100644
    index 0000000..e69de29
    diff --git a/bob.txt b/bob.txt
    new file mode 100644
    index 0000000..e69de29

***&rarr; Fork instructions:*** *Navigate to 'All Commits' (below 'Local Changes' in the side bar) to view the Fork equivalent of the git log. The new commit, labelled as the commit subject, can now be found at the top of the branch tree. Listed below are all previous commits.*

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

A necessary digression
----------------------

In this section, we are going to add more changes, and try to recover
from mistakes.

Be forewarned, this next step is going to be hard. We will need to add
some content to alice.txt.

Open `alice.txt` and type in some fun or interesting text. Hint: Add a few lines of text to take full advantage of the following step (mainly for those of you who use Fork).

Then **save** the file

What did we change? A very useful command is `git diff`. This is very
useful to see exactly what changes you have done.

    $ git diff

You should see something like the following:

    diff --git a/alice.txt b/alice.txt
    index e69de29..2aedcab 100644
    --- a/alice.txt
    +++ b/alice.txt
    @@ -0,0 +1 @@
    +Lorem ipsum Sed ut perspiciatis, unde omnis iste natus error sit voluptatem accusantium doloremque laudantium

***&rarr; Fork instructions:*** *View changes as instructed above (Local Changes and select changed files). Red and green sections indicate deletions and additions. If you edit a longer file at multiple locations you will find that Fork allows you to stage sections separately. Try it out: Edit multiple lines of your file and save it. Hover your cursor over the file changes in Fork. This will highlight any separate changes that were made and a 'Stage' button appears. Click it to stage only the selected section. Pretty nifty, hey?*

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Staging area again
------------------

Now let’s add our modified file, `alice.txt` to the staging area. Do you
remember how ?

Next, check the `status` of `alice.txt`. Is it in the staging area now?

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Undoing
-------

Let’s say we did not like putting Lorem ipsum into `alice.txt`. One
advantage of a staging area is to enable us to back out before we
commit - which is a bit harder to back out of. Remembering the mail
analogy - it’s easier to take mail out of the cardboard box before you
seal it than after.

Here’s how to back out of the staging area :

    $ git reset HEAD alice.txt

    Unstaged changes after reset:
    M   alice.txt

***&rarr; Fork instructions:*** *Select one or multiple staged files and hit the 'Unstage' button. The files will move back to the 'Unstaged' area.*

Compare the `git status` now to the git status from the previous
section. How does it differ?

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Your staging area should now be empty. What’s happened to the Lorem
Ipsum changes? It’s still there. We are now back to the state just
before we added this file to staging area. Going back to the mail
analogy, we just took our letter out of the box.

Undoing II
----------

Sometimes we did not like what we have done and we wish to go back to
the last *recorded* state. In this case, we wish to go back to the state
just before we added the Lorrem ipsum text to `alice.txt`.

To accomplish this, we use `git checkout`, like so:

    $ git checkout alice.txt

You have now un-done your changes. Your file is now empty.

***&rarr; Fork instructions:*** *Right click a file in the Unstaged area and select 'Discard changes'. Note: This will discard* **every** *change made to the file. You can selectively discard changes the same way you can stage them. Do you remember how? The file will be reverted back to the state before you made the discarded changes. Check!*

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Branching
---------

Most large code bases have at least two branches - a ‘live’ branch and a
‘development’ branch. The live branch is code which is OK to be deployed
on to a website, or downloaded by customers. The development branch
allows developers to work on features which might not be bug free. Only
once everyone is happy with the development branch would it be merged
with the live branch.

Creating a branch in Git is easy. The `git branch` command, when used by
itself, will list the branches you currently have

    $ git branch

The `*` should indicate the current branch you are on, which is
`master`.

***&rarr; Fork instructions:*** *In Fork, the branches are listed in the side bar under 'Branches'. Click the arrow to collapse or expand the branch list. You should see a single branch called 'master'.*

If you wish to start another branch, use
`git checkout -b (new-branch-name)` :

    $ git checkout -b exp1

Try git branch again to check which branch you are currently on:

    $ git branch
      exp1
    * master

***&rarr; Fork instructions:*** *Start a new branch: Menu bar > Repository > New Branch (SHIFT+CMD+B). The new branch will now be listed next to the master branch in the branch list. You will also find the new branch added as a little tag next to the latest commit.*

The new branch is now created. Now let’s work in that branch. To switch
to the new branch:

    $ git checkout exp1

`git checkout (branch-name)` is used to switch branches.

***&rarr; Fork instructions:*** *Checking out branches is as easy as double clicking them in the branch list. Check out your new branch.*

Let’s perform some commits now,

    $ echo 'some content' > test.txt
    $ git add test.txt
    $ git commit -m "Added experimental txt"

Now, let’s compare them to the master branch. Use `git diff`

    $ git diff master

Basically what the above output says is that `test.txt` is present on
the `exp1` branch, but is absent on the `master` branch.

***&rarr; Fork instructions:*** *Honestly not sure if this option exists in Fork. Similarly unsure why it should. Simply switch between branches to see which files exist or don't.*

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Now you see me, now you don’t
-----------------------------

Git is good enough to handle your files when you switch between
branches. Switch back to the `master` branch

Try switching back to the master branch (Hint: It’s the same command we
used to switch to the exp1 branch above)

Now, where’s our `test.txt` file ?

    $ ls
    README.textile  alice.txt   bob.txt     gamow.txt

As you can see the new file you created in the other branch has
disappeared. Not to worry, it is safely tucked away, and will re-appear
when you switch back to that branch.

Now, switch back to the exp1 branch, and check that the `test.txt` is
now present.

***&rarr; Fork instructions:*** *You can also checkout previous commits by double clicking the commit you want to look at. Checking your repository folder, you will its contents changing based on what the repository looked like at any given commit stage.*

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Merging
-------

We now try out merging. Eventually you will want to merge two branches
together after the conclusion of work.\
`git merge` allows you to do that.

Git merging works by first switching the branch you want to merge *into*, and
then running the command to merge the other branch in.

We now want to merge our `exp1` branch into `master`. First, switch to
the `master` branch.

    git checkout master

Next, we merge the `exp1` branch into `master` :

    $ git merge exp1

Do you see the following output ?

    Merge made by recursive.
     test.txt |    1 +
     1 files changed, 1 insertions(+), 0 deletions(-)
     create mode 100644 test.txt

You have to be in the branch you want merge *into* and then you always
specify the branch you want to merge.

At this point, you can also try out `gitk` to visualize the changes and
how the two branches have merged.

***&rarr; Fork instructions:*** *Same way here: You neec to be in the branch that you want to merge into. Checkout the master branch. Now right-click your new branch you want to merge and select 'Merge into master'. Keep the default commit option and click 'Merge'. Note the green arrow and the notification 'The branch can be merged without conflicts' (see next section).*

Merge Conflicts
---------------

Git is pretty good at merging automagically, even when the same file is
edited. There are however, some situations where the same line of code
is edited there is no way a computer can figure out how to merge.\
This will trigger a conflict which you will have to fix.

We now practise fixing merge conflicts. Recall that conflicts are caused
by merges which affect the same block of code.

Here’s a branch I prepared earlier. The branch is called `alpher`. Run
the code below to set it up (don’t worry if you can’t understand it)

    $ git checkout alpher

You should now have a new branch called `alpher`. Try merging that
branch into `master` now and fix the ensuing conflict.

***&rarr; Fork instructions:*** *The 'alpher' branch is not yet in your cloned local repository, but still stored remotely on the GitHub repository. To see a list of remote branches head over to the side bar and expand 'Remotes > Origin'. Double click the 'alpher' branch to check it out. You will be prompted to 'Track Remote Branch', which clones it to your local repository.*

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

Fixing a conflict
-----------------

You should see a `conflict` with the `gamow.txt` file. This means that
the same line of text was edited and committed on both the master branch
and the alpher branch. The output below basically tells you the current
situation :

    Auto-merging gamow.txt
    CONFLICT (content): Merge conflict in gamow.txt
    Automatic merge failed; fix conflicts and then commit the result.

***&rarr; Fork instructions:*** *Try and merge alpher into master following the previous instructions. Check the message that previously read 'The branch can be merged without conflicts'. What does it say now? Click Merge. You will now be automatically directed to the 'Local Changes', where you are prompted to resolve any conflicts before the merge can be performed (close the 'Git Error' message, it only lets you know that a conflict has arisen).*

If you open the `gamow.txt` file, you will see something similar as
below:

    $ cat gamow.txt
    <<<<<<< HEAD
    It was eventually recognized that most of the heavy elements observed in the present universe are the result of stellar nucleosynthesis (http://en.wikipedia.org/wiki/Stellar_nucleosynthesis) in stars, a theory largely developed by Bethe.
    =======

    http://en.wikipedia.org/wiki/Stellar_nucleosynthesis
    Stellar nucleosynthesis is the collective term for the nuclear reactions taking place in stars to build the nuclei of the elements heavier than hydrogen. Some small quantity of these reactions also occur on the stellar surface under various circumstances. For the creation of elements during the explosion of a star, the term supernova nucleosynthesis is used.
    >>>>>>> alpher

Git uses pretty much standard conflict resolution markers. The top part
of the block, which is everything between `<<<<<< HEAD` and `======` is
what was in your current branch.\
The bottom half is the version that is present from the `alpher` branch.
To resolve the conflict, you either choose one side or merge them as you
see fit.

For example, I might decide to choose the version from the `alpher`
branch.

Now, try to **fix the merge conflict**. Pick the text that you think is
better (Ask for help if stumped)

Once I have done that, I can then mark the conflict as fixed by using
`git add` and `git commit`.

***&rarr; Fork instructions:*** *To fix the conflict, click 'Resolve' in the top right corner. Fixing merge conflicts can be achieved in two ways. Either in a text editor (as explained above) or in Fork (see respective buttons). The conflict window is showing you which file on both branches has conflicting changes made to it. If you want to resolve the changes in Fork click 'Merge in Fork'. Select the changes you prefer and click Resolve. The new file changes allowing for a smooth Merge of the branches will now show up as Staged. Fork will automatically generate a merge commit subject and description. Feel free to edit and commit once your happy. Note: You can* **abort** *the merge at any stage before the final merge commit in case you want to back out.*

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Stuck? Ask for help from the workshop staff

    $ git add gamow.txt
    $ git commit -m "Fixed conflict"

Congratulations. You have fixed the conflict. You are now officially a Git Mediator. All is good in the world.

Summary
---

You have learnt how to:

1.  Clone a repository
2.  Commit files
3.  Check status
4.  Check diff
5.  Und changes
6.  Branch and merge
7.  Fix conflicts

either in the command line or using the Git GUI Fork.


GitHub Part 2
=============

We forked a repository earlier. The following <a href="https://help.github.com/articles/create-a-repo">
tutorial</a> will show you how to create a GitHub repo - which you can
then share with others

Merging:
--------

Check out the `pull_request` branch on this repository for further instructions!
You can always get back to this version of the readme by checking out the master branch.

Searching your code
------------------
Go to a repository and it can be really easy to global search and find what file or where you wrote a certain line of code.



Publishing your code
-------
Go to https://zenodo.org/
Will create a DOI for your code.

They have instructions there.
Basically create a release on github and it all should just work.






Bonus Content
=======

Check out the `revert` branch on this repository for further instructions!
You can always get back to this version of the readme by checking out the master
branch.

### References and Further reading

I throughly recommend these resources to continue your Git practice:

-   <a href="http://try.github.com">http://try.github.com</a> Another
    beginners tutorial for git
-   <a href="http://git-scm.com">http://git-scm.com</a> Official
    website, with very useful help, book and videos
-   <a href="http://gitref.org">http://gitref.org</a>
-   <a href="http://www.kernel.org/pub/software/scm/git/docs/everyday.html">http://www.kernel.org/pub/software/scm/git/docs/everyday.html</a>

Author
------

This work is licensed under the Creative Commons
Attribution-NonCommercial-ShareAlike 3.0 License\
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">http://creativecommons.org/licenses/by-nc-sa/3.0/</a>\
Author: Thong Kuah\
Contributors: Andy Newport, Nick Malcolm
Adapted by: Nic Pittman & Jake Weis
