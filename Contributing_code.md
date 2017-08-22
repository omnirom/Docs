![LOGO](images/omnirom_logo-big_layout_transparent-250px-150x150.png)
# OmniROM Documents
## Contributing code to Omnirom

### Creating a patch

The beauty of open source projects is the ability for even the most novice of developers to be involved in determining the trajectory of the project. The difficulty is in knowing exactly how to submit your patch for code review and (hopefully) inclusion into the project.

Below are the simple, basic steps for contributing code:

1. Begin by performing a `repo sync` so that we know we’re dealing with the most recent versions of the code. We're also assuming that you have experience with terminal & you have your OmniROM repo in ~/android/omni:
```
#: cd ~/android/omni
#: repo sync
```
2. Go to https://gerrit.omnirom.org and register. ***Make sure to accept the agreement.***
3. Now go and make the changes to the files you are wanting to change.
4. Now in terminal, navigate to the project directory.
5. We need to commit the changes to gerrit for review, along with a message telling exactly what was done for the reviewer(s) to review
6. Let's check what all we changed
```
#:  git status  (''this will tell you the files that were changed'')
```
7. Now let's add the files
```
#:  git add <file name>
```
if you need only some of the changed files, or use
```
#: git add -A
```
to add all the files.
8.  Now we need to create a commit for the changes
```
#:  git commit
```
This will open up an editor and at the top line you will need to provide the comment about the changes you have done.
  - Suggested format:
```
<PackageName>: <overview of change(s) made>
```
  - Example:
```
Base: Add new ringtone
```
9. Once done press CTRL-O to save your changes, and then CTRL-X to exit. Your changes will be saved, and you’ll receive a notice about the number of changes to be submitted.
10. Now we need to upload our changes to gerrit for review.
```
#: git push ssh://<username>@gerrit.omnirom.org:29418/<project> HEAD:refs/for/<branch></nowiki>
```
  - Example:
```
git push ssh://UtkarshGupta@gerrit.omnirom.org:29418/android_frameworks_base HEAD:refs/for/android-7.1
```
11. This will upload the changes, and you’ll receive a web link to those changes like https://gerrit.omnirom.org/1479/

**For more information on Gerrit, see [Gerrit Rules](Gerrit_rules.md).**

### Creating a patchset
Now that you have created a patch, you may want to change it. To create a patchset, follow the below steps:

1. Begin by performing a `repo sync` so that we know we’re dealing with the most recent versions of the code. We're also assuming that you have your Omnirom repo in ~/android/omni:
```
#: cd ~/android/omni
#: repo sync
```
2. Now in terminal, navigate to the project directory.
3. Cherry-pick your patch from gerrit.
4. Make your changes
5. Now let's change our original commit
  - Let's check what all we changed:
```
#:  git status  
```
this will tell you the files that were changed
  - Now let's add the files:
```
#:  git add <file name>
```
if you need only some of the changed files, or use
```
#:  git commit -A
```
to add all the files.
  - We want to change our original commit instead of creating a new one
```
#:  git commit --amend
```
This will open up the same editor we dealt with already.
  - Make any changes to the commit message that you need to and exit, making sure to save your changes.
6. Now the commit is ready to be pushed. This will edit the original commit instead of creating a new one.

### Getting lazy
Typing `git push ssh://<username>@gerrit.omnirom.org:29418/<project> HEAD:refs/for/<branch>` every time is a painful job. So instead of typing it every time, we can create a remote for it:
```
#: git remote add <name> ssh://<username>@gerrit.omnirom.org:29418/<project></nowiki>
```
Using it
```
#: git push <name> HEAD:refs/for/<branch>
```
You'll have to create remotes for every project, but hey - you're getting lazy.

#### Getting more lazy
If you're *extremely* lazy, you can install **git-review** via [this guide](http://www.mediawiki.org/wiki/Gerrit/git-review). Once done, you will need to configure it:
```
#: git remote add gerrit ssh://<username>@gerrit.omnirom.org:29418/<project>
#: git review -s
```

***Creating a patch:***
```
$ git checkout -b mycoolfeature
```
Change the files you need to, then:
```
$ git commit -a
$ git review
```

***Creating a patchset:***
```
$ git checkout mycoolfeature
```
Change the files you need to, then:
```
$ git commit -a --amend
$ git review
```

### Licensing

It is important that any code you contribute follows either the existing licensing, or utilizes the correct licensing. For pre-created headers, see the [License template](License_template.md).
