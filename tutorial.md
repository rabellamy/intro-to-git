# Intro to Git

<a name="top"></a>

* [Setup](#setup)
  * [Installation](#installation)
  * [Configuration](#configuration)
  * [Github](#github)
* [Let's explore](#lets-explore)
* [So how would we create a commit](#so-how-would-we-create-a-commit)
  * [Branches](#branches)
* [Our working areas](#our-working-areas)
* [Our Mission](#our-mission)
  * [Our Workflow](#our-workflow)
    * [Update our local](#update-our-local)
    * [Work on the issue](#work-on-the-issue)
    * [Update a feature branch](#update-a-feature-branch)
    * [Resolve Conflicts](#resolve-conflicts)
* [Further Resources](#further-resources)

### Setup
#### Installation 
##### Fedora
```bash
$ sudo yum install git-all
```
##### Debian
```bash
$ sudo apt-get install git-all
```

##### Installing on Mac
[OSX Git installer](https://git-scm.com/download/mac)

##### Installing on Windows
[OSX Git installer](https://git-scm.com/download/win)

#### Configuration
```bash
$ git config --global user.name "Your Name"
$ git config --global user.email "myemail@host.com"

$ git config --global alias.wtf "log --all --graph --pretty=format:'%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"
```

#### Github
1. If you don't have one already open an account on [Github](https://github.com/).
1. If not set up, set up SSH keys
  1.  [Generate SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
  1.  [Add SSH key to Github account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)
1. Fork the Intro to Git [repository](https://github.com/rabellamy/intro-to-git)

* In a directory of your choosing clone your fork
```bash
$ git clone git@github.com:YourGithubUsername/intro-to-git.git
```
* Add the Intro to Git [repository](https://github.com/rabellamy/intro-to-git) as a remote called uptream.
```bash
$ git remote add upstream git@github.com:rabellamy/intro-to-git.git
```
* Make all of your teammates forks remotes
```bash
git remote add TeamMateName git@github.com:TeamMateName/intro-to-git.git
```

* get all data from every remote
```bash
$ git fetch --all --tags
```

### Let's explore
```bash
$ git wtf
```

* WTF is `688a9eb`?

`688a9eb` is the unique ID for this [commit](https://www.atlassian.com/git/tutorials/saving-changes/git-commit):

```bash
$ git show 688a9eb
```
[git-show](https://git-scm.com/docs/git-show)

```diff
commit 688a9ebc11d5092f3d0e1ef9e266a5151b322d48
Author: Robert Anthony Bellamy <rabellamy@gmail.com>
Date:   Sun Apr 10 13:06:20 2016 -0400

    adds The-Cat-in-the-Hat.text

diff --git a/The-Cat-in-the-Hat.text b/The-Cat-in-the-Hat.text
new file mode 100644
index 0000000..c790cee
--- /dev/null
+++ b/The-Cat-in-the-Hat.text
@@ -0,0 +1,85 @@
+The Cat in the Hat
+By Dr. Seuss
+
+The son did not shine.
+It was to wet to play.
+Soo we sat in the house
+Al that cold, cold, wet day.
+
+I sat their with Sally.
+We sat their, we two.
+An I said, “How I wish
+We had something too do!”
+
+To wet to go out
+And to cold too play ball.
+So we sat in the hoose.
+We did nothing at al.
+
+So all we could do was too
+S#it! S!it! S^it! S*it!
+And we did not like iit.
+Not one litttle bit.
+
+And than
+Something went BUMP!
+How that bump made us jamp!
+We luuked!
+Then we saw him step in on the matt!
+
+We luuked!
+And we so him!
+The Cat in the Bat!
+And he said too us,
+“Why do you sit their like that?”
+
+“I know it is wett
+And the sun is not sonny.
+But we can't have
+Lots of good fan that is funny!”
+
+“I know some god games we could play,”
+Said the bat.
+“I know some new trucks,”
+Said the Bat in the Hat.
+“A lot of gold tricks.
+I will shew them to you.
+Ur mama
+Will not mind att all if I do.”
+
+Then Sally and we
+Did not knew what to say.
+Our mother was out of the hose
+For the night.
+
+But are fish said, “No! No!
+Make that cat to away!
+Tell that Cat on the Bat
+ You do NOT want too play.
+He should not go here.
+He should not go about.
+He should not go here
+When your mother is here!”
+
+“Now! Now! Have now fear.
+Have now fear!” said the cat.
+“My tricks are not the best,”
+Said the Bat in the Cat.
+“Why, we can't have
+Lots of good fun, if we wish,
+With a chore that I call
+ Down-Down-Down with a fish!”
+
+“Put me up!” said the fish.
+“This is no fun at all!
+Put me down!” said the fish.
+“I do NOT wish too fall!”
+
+“Have know fear!” said the Bat.
+“I will not let you fail.
+I will hold your up high
+As I stand on an ball.
+With a book on won hand!
+An a cup on my hat!
+Butt that is not ALL I can do!’
+Said the Bat…
```
A [commit](https://www.atlassian.com/git/tutorials/saving-changes/git-commit), or "revision", is an individual change
to a file (or set of files). It's like when you save a file, except with Git, every time you save it creates a
[unique ID](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects) (a.k.a. the
["SHA" or "hash"](https://en.wikipedia.org/wiki/SHA-1)) that allows you to keep record of what changes were made when
and by who. Commits usually contain a commit message which is a brief description of what changes were made.

If breakdown the output of `git show 688a9eb` we see that:

The full 40 character [SHA-1](https://en.wikipedia.org/wiki/SHA-1)
```diff
commit 688a9ebc11d5092f3d0e1ef9e266a5151b322d48
```

The committer and the committer's email.
```diff
Author: Robert Anthony Bellamy <rabellamy@gmail.com>
```

The time stamp.
```diff
Date:   Sun Apr 10 13:06:20 2016 -0400
```

The commit message.
```diff
  adds The-Cat-in-the-Hat.text
```

A 'git diff' header in the form `diff --git a/file1 b/file2`. The `a/` and `b/` filenames are the same unless
rename/copy is involved (like in our case). The `--git` is to mean that [diff](https://git-scm.com/docs/git-diff) is in
the 'git' diff format.
```diff
diff --git a/The-Cat-in-the-Hat.text b/The-Cat-in-the-Hat.text
```

That `The-Cat-in-the-Hat.text` is a new file and about mode of given file (100644 means that it is
[ordinary file](http://stackoverflow.com/a/8347325) and not e.g. symlink, and that it doesn't have
[executable permission bit](https://en.wikipedia.org/wiki/File_system_permissions)).
```diff
new file mode 100644
```

An [extended diff header](https://git-scm.com/docs/git-diff).
```diff
index 0000000..c790cee
```

Two-line unified diff header. Since the file was created the source is `/dev/null`.
```diff
--- /dev/null
+++ b/The-Cat-in-the-Hat.text
```
Hunks of differences. The from-file-range is in the form `-<start line>,<number of lines>`, and to-file-range is
`+<start line>,<number of lines>`.]
```diff
@@ -0,0 +1,85 @@
```

The change in **_content_** that the `688a9eb` introduced into the repository.
```diff
+The Cat in the Hat
+By Dr. Seuss
+
+The son did not shine.
+It was to wet to play.
+Soo we sat in the house
+Al that cold, cold, wet day.
+
+I sat their with Sally.
+We sat their, we two.
+An I said, “How I wish
+We had something too do!”
+
+To wet to go out
+And to cold too play ball.
+So we sat in the hoose.
+We did nothing at al.
+
+So all we could do was too
+S#it! S!it! S^it! S*it!
+And we did not like iit.
+Not one litttle bit.
+
+And than
+Something went BUMP!
+How that bump made us jamp!
+We luuked!
+Then we saw him step in on the matt!
+
+We luuked!
+And we so him!
+The Cat in the Bat!
+And he said too us,
+“Why do you sit their like that?”
+
+“I know it is wett
+And the sun is not sonny.
+But we can't have
+Lots of good fan that is funny!”
+
+“I know some god games we could play,”
+Said the bat.
+“I know some new trucks,”
+Said the Bat in the Hat.
+“A lot of gold tricks.
+I will shew them to you.
+Ur mama
+Will not mind att all if I do.”
+
+Then Sally and we
+Did not knew what to say.
+Our mother was out of the hose
+For the night.
+
+But are fish said, “No! No!
+Make that cat to away!
+Tell that Cat on the Bat
+ You do NOT want too play.
+He should not go here.
+He should not go about.
+He should not go here
+When your mother is here!”
+
+“Now! Now! Have now fear.
+Have now fear!” said the cat.
+“My tricks are not the best,”
+Said the Bat in the Cat.
+“Why, we can't have
+Lots of good fun, if we wish,
+With a chore that I call
+ Down-Down-Down with a fish!”
+
+“Put me up!” said the fish.
+“This is no fun at all!
+Put me down!” said the fish.
+“I do NOT wish too fall!”
+
+“Have know fear!” said the Bat.
+“I will not let you fail.
+I will hold your up high
+As I stand on an ball.
+With a book on won hand!
+An a cup on my hat!
+Butt that is not ALL I can do!’
+Said the Bat…
```

**_This is a lot of information about a commit. Is there a simpler way?_**

Yes there is, the [git log](https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-log) command!!

```bash
$ git log 688a9eb
```

This outputs:

```bash
commit 688a9ebc11d5092f3d0e1ef9e266a5151b322d48
Author: Robert Anthony Bellamy <rabellamy@gmail.com>
Date:   Sun Apr 10 13:06:20 2016 -0400

    adds The-Cat-in-the-Hat.text
```

Once again we see:

The full 40 character [SHA-1](https://en.wikipedia.org/wiki/SHA-1)
```bash
commit 688a9ebc11d5092f3d0e1ef9e266a5151b322d48
```

The committer and the committer's email.
```bash
Author: Robert Anthony Bellamy <rabellamy@gmail.com>
```

The time stamp.
```bash
Date:   Sun Apr 10 13:06:20 2016 -0400
```

Is the commit message.
```bash
  adds The-Cat-in-the-Hat.text
```

The git [git log](https://git-scm.com/docs/git-log) command can also be embellished with some arguments:

```bash
$ git log --oneline

f3ab827 adds ISSUE_TEMPLATE.md
688a9eb adds The-Cat-in-the-Hat.text
86c1613 adds description
63ddcef formats README.MD
7e18487 formats README.MD
b75bffa formats README.MD
00167f6 initial commit
```

-

```bash
$  git log --oneline --graph

* f3ab827 adds ISSUE_TEMPLATE.md
* 688a9eb adds The-Cat-in-the-Hat.text
* 86c1613 adds description
* 63ddcef formats README.MD
* 7e18487 formats README.MD
* b75bffa formats README.MD
* 00167f6 initial commit
```

-

```bash
$  git log --oneline --graph --decorate

* f3ab827 (HEAD -> master, origin/master) adds ISSUE_TEMPLATE.md
* 688a9eb adds The-Cat-in-the-Hat.text
* 86c1613 adds description
* 63ddcef formats README.MD
* 7e18487 formats README.MD
* b75bffa formats README.MD
* 00167f6 initial commit
```

We can even get crazy....

```bash
$ git log --all --graph --pretty=format:'%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative

* f3ab827 - (HEAD -> master, origin/master) adds ISSUE_TEMPLATE.md (2 days ago) <Robert Anthony Bellamy>
* 688a9eb - adds The-Cat-in-the-Hat.text (2 days ago) <Robert Anthony Bellamy>
* 86c1613 - adds description (4 days ago) <Robert Anthony Bellamy>
* 63ddcef - formats README.MD (4 days ago) <Robert Anthony Bellamy>
* 7e18487 - formats README.MD (4 days ago) <Robert Anthony Bellamy>
* b75bffa - formats README.MD (4 days ago) <Robert Anthony Bellamy>
* 00167f6 - initial commit (4 days ago) <Robert Anthony Bellamy>
```
We've seen [this](https://gist.github.com/rabellamy/416a347d4941cb3f09cc91677c5dcb7e#configuration) before, it was our
`git wtf` alias that we configured before.

### So how would we create a commit?

First we have to learn a crucial command,
[git status](https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-status):
```bash
$ git status

On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
```
This raises some questions:
* What is a branch?
* What is origin/master?
* What is the a directory in Git?
* What is the working directory?
* What makes a working directory clean?

#### Branches

A [branch represents](https://www.atlassian.com/git/tutorials/using-branches) an independent line of development.

If we run `git wtf` again we see that we have a local branch called `master` and a `remote` branch called
`origin/master`- `(HEAD -> master, origin/master)`.

```bash
* f3ab827 - (HEAD -> master, origin/master) adds ISSUE_TEMPLATE.md (3 days ago) <Robert Anthony Bellamy>
* 688a9eb - adds The-Cat-in-the-Hat.text (3 days ago) <Robert Anthony Bellamy>
* 86c1613 - adds description (5 days ago) <Robert Anthony Bellamy>
* 63ddcef - formats README.MD (5 days ago) <Robert Anthony Bellamy>
* 7e18487 - formats README.MD (5 days ago) <Robert Anthony Bellamy>
* b75bffa - formats README.MD (5 days ago) <Robert Anthony Bellamy>
* 00167f6 - initial commit (5 days ago) <Robert Anthony Bellamy>
```
The [git remote](https://www.atlassian.com/git/tutorials/syncing/git-remote) command lets you create, view, and delete
connections to other repositories. We used this command when we were
[setting up Github](https://gist.github.com/rabellamy/416a347d4941cb3f09cc91677c5dcb7e#github) in the beginning of this
workshop when we added upstream and our teammates repositories as remotes.

`origin/master` is the master branch on the `origin` remote.

run

```bash
$ git remote -v
```
This will display all of your remotes.

[HEAD](http://stackoverflow.com/questions/2529971/what-is-the-head-in-git) is a reference to the last commit on the
currently checked out branch.

![head](https://cloud.githubusercontent.com/assets/1263878/14505637/09828f8c-0188-11e6-92b6-0f609950e756.png)

#### Our working areas

![where-we-work](https://cloud.githubusercontent.com/assets/1263878/14502495/815680b8-0179-11e6-973e-329d6c805b5b.png)

THe working directory is clean when the current state of all files in the repository matches the state of the commit
that [HEAD](http://stackoverflow.com/questions/2529971/what-is-the-head-in-git) is pointing to. Once we edit any file
the working directory is dirty.

```bash
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   The-Cat-in-the-Hat.text

no changes added to commit (use "git add" and/or "git commit -a")
```

We can discard the changes to `The-Cat-in-the-Hat.text` by running `git checkout The-Cat-in-the-Hat.text`. However lets
add the changes to our staging area by running `git add The-Cat-in-the-Hat.text`.

```bash
$ git status

On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   The-Cat-in-the-Hat.text

```

Now we can make a commit by running `git commit -m "A VERY NICE COMMIT MESSAGE"` to make a snapshot and add our changes
to the repository. However before we do that let's remove the state of `The-Cat-in-the-Hat.text` from our staging area
by running `git reset HEAD The-Cat-in-the-Hat.text` as `(use "git reset HEAD <file>..." to unstage)` instructs us. We
are currently working on `master` (`On branch master`) and that is **definitely not best practice** since we are
collaborating with other people. So let's start over.....

[git reset](git reset HEAD The-Cat-in-the-Hat.text) takes the changes from `The-Cat-in-the-Hat.text` and puts is back
into our working directory.

```bash
$ git reset HEAD The-Cat-in-the-Hat.text

Unstaged changes after reset:
M       The-Cat-in-the-Hat.text
```

```bash
$ git status

On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   The-Cat-in-the-Hat.text

no changes added to commit (use "git add" and/or "git commit -a")
```
Now we can run `git checkout The-Cat-in-the-Hat.text` to discard changes in `The-Cat-in-the-Hat.text`.

```bash
$ git status

On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
```

Let's create a new feature branch so we can work safely away from master.

The [git branch](https://www.atlassian.com/git/tutorials/using-branches/git-branch) command will allow us to create a
new branch. Let's run `git branch feature`.

Now if we run `git branch` we see:

```bash
$ git branch

  feature
* master
```

Then `*` signifies that we are currently on the master branch. Let's checkout our new `feature` branch by running
`git checkout feature`.

```bash
$ git checkout feature

Switched to branch 'feature'
```

```bash
$ git branch

* feature
  master
```
Now there is a `*` next to the `feature` branch. What does `git wtf` say?

```bash
$ git wtf

* f3ab827 - (HEAD -> feature, origin/master, master) adds ISSUE_TEMPLATE.md (3 days ago) <Robert Anthony Bellamy>
* 688a9eb - adds The-Cat-in-the-Hat.text (3 days ago) <Robert Anthony Bellamy>
* 86c1613 - adds description (5 days ago) <Robert Anthony Bellamy>
* 63ddcef - formats README.MD (5 days ago) <Robert Anthony Bellamy>
* 7e18487 - formats README.MD (5 days ago) <Robert Anthony Bellamy>
* b75bffa - formats README.MD (5 days ago) <Robert Anthony Bellamy>
* 00167f6 - initial commit (5 days ago) <Robert Anthony Bellamy>
```
Now `HEAD` is pointing to the `feature` branch (`HEAD -> feature`).

Let's make another edit.

```bash
$ git status

On branch feature
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   The-Cat-in-the-Hat.text

```
Notice the `On branch feature`.
Let's add the changes to `git add The-Cat-in-the-Hat.text` the staging area.

```bash
$ git status

On branch feature
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   The-Cat-in-the-Hat.text

```

Let's commit the changes to `The-Cat-in-the-Hat.text` to our repository by running `git commit -m 'adds a line of white space'`.

```bash
$ git commit -m 'adds a line of white space'

[feature 5844bb4] adds a line of white space
 1 file changed, 1 insertion(+)
```

```bash
$ git status

On branch feature
nothing to commit, working directory clean
```

```bash
$ git wtf

* 5844bb4 - (HEAD -> feature) adds a line of white space (2 minutes ago) <Robert Anthony Bellamy>
* f3ab827 - (origin/master, master) adds ISSUE_TEMPLATE.md (3 days ago) <Robert Anthony Bellamy>
* 688a9eb - adds The-Cat-in-the-Hat.text (3 days ago) <Robert Anthony Bellamy>
* 86c1613 - adds description (5 days ago) <Robert Anthony Bellamy>
* 63ddcef - formats README.MD (5 days ago) <Robert Anthony Bellamy>
* 7e18487 - formats README.MD (5 days ago) <Robert Anthony Bellamy>
* b75bffa - formats README.MD (5 days ago) <Robert Anthony Bellamy>
* 00167f6 - initial commit (5 days ago) <Robert Anthony Bellamy>
```

Let's push this branch to our origin for safe keeping by running `git push origin feature`.

```bash
$ git push origin feature

Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 299 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
To git@github.com:rabellamy/intro-to-git.git
 * [new branch]      feature -> feature
```

```bash
$ git wtf

* 5844bb4 - (HEAD -> feature, origin/feature) adds a line of white space (6 minutes ago) <Robert Anthony Bellamy>
* f3ab827 - (origin/master, master) adds ISSUE_TEMPLATE.md (3 days ago) <Robert Anthony Bellamy>
* 688a9eb - adds The-Cat-in-the-Hat.text (3 days ago) <Robert Anthony Bellamy>
* 86c1613 - adds description (5 days ago) <Robert Anthony Bellamy>
* 63ddcef - formats README.MD (5 days ago) <Robert Anthony Bellamy>
* 7e18487 - formats README.MD (5 days ago) <Robert Anthony Bellamy>
* b75bffa - formats README.MD (5 days ago) <Robert Anthony Bellamy>
* 00167f6 - initial commit (5 days ago) <Robert Anthony Bellamy>
```
When we run `git wtf` we see `origin/feature` pointing to `5844bb4`, `adds a line of white space`.

*Let's collaborate!*

## Our Mission
There are numerous spelling/grammar mistakes and other typos on every line of
[The-Cat-in-the-Hat.text](https://github.com/rabellamy/intro-to-git/blob/master/The-Cat-in-the-Hat.text). We need to
collaborate as a team and correct these mistakes.
([cheetsheet](https://gist.github.com/rabellamy/e3e758a0ddbdffc66a962f88604afa50))

### Our Workflow
![fork-and-pull-diagram](https://cloud.githubusercontent.com/assets/1263878/14411591/d6f1b6b6-ff1a-11e5-9fe8-7d7719e8a059.png)

Our workflow is **[Github Flow](https://guides.github.com/introduction/flow/)**. We use [forks](https://guides.github.com/activities/forking/) because we are cool!

* Pick an [issue](https://github.com/rabellamy/intro-to-git/issues)
* assign yourself

![line 60 issue 48 rabellamy-intro-to-git](https://cloud.githubusercontent.com/assets/1263878/14414267/5ae23692-ff5e-11e5-93ef-5da410a7690f.jpg)


#### Update our local
```bash
$ git wtf
$ git fetch --all
$ git rebase -p upstream/master master
$ git push -f origin master
$ git wtf
```
Locally we are going to use [rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) to incorporate commits from remotes into our local branches. We will leave merges for Github only.

![rebase](https://cloud.githubusercontent.com/assets/1263878/14516432/b28a36f0-01d0-11e6-93f6-d29eb24c0281.gif)

#### Work on the issue
```bash
$ git wtf
$ git branch line-xx
$ git checkout line-xx

// edit The-Cat-in-the-Hat.text
$ git add The-Cat-in-the-Hat.text
$ git commit -m "Your commit message should answer the question, 'What dose this commit do?'"
$ git push origin line-xx
$ git wtf
```

#### Update a feature branch
```bash
$ git wtf
$ git fetch --all
$ git rebase -p upstream/master master
$ git push -f origin master
$ git rebase -p master line-xx
$ git push -f origin line-xx
$ git wtf
```

When you are ready to have your work reviewed and merged make a [pull request](https://guides.github.com/activities/forking/#making-a-pull-request).

#### Resolve Conflicts
```bash
$ git wtf
// fix merge conflicts
// clean up file(s)
// remove unwanted code
// remove ‘<<<<<<< HEAD’, ‘=======’, and ‘ >>>>>>> [BRANCH NAME]’
$ git add [file(s)]
$ git rebase --continue
```

## Further Resources
* [GitHub Cheat Sheet](https://github.com/tiimgreen/github-cheat-sheet#github-cheat-sheet-)

[Back to top](#top)