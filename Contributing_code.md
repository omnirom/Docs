
== Creating a patch ==

The beauty of open source projects is the ability for even the most novice of developers to be involved in determining the trajectory of the project. The difficulty is in knowing exactly how to submit your patch for code review and (hopefully) inclusion into the project.

Below are the simple, basic steps for contributing code:
# Begin by performing a ''repo sync'' so that we know we’re dealing with the most recent versions of the code. We're also assuming that you have experience with terminal & you have your Omnirom repo in ~/android/omni:
#: cd ~/android/omni
#: repo sync
# Go to gerrit.omnirom.org and register. '''Make sure to accept the agreement.'''
# Now go and make the changes to the files you are wanting to change.
# Now in terminal, navigate to the project directory.
# We need to commit the changes to gerrit for review, along with a message telling exactly what was done for the reviewer(s) to review
#* Let's check what all we changed
#:  git status  (''this will tell you the files that were changed'')
#* Now let's add the files
#:  git add <file name> if you need only some of the changed files
#:  or use git add -A to add all the files.
#* Now we need to create a commit for the changes
#:  git commit
#* This will open up an editor and at the top line you will need to provide the comment about the changes you have done.
#::  '''Suggested format:''' ''<PackageName>: <overview of change(s) made>''
#::  '''Example:''' ''Base: Add new ringtone''
#* Once done press CTRL-O to save your changes, and then CTRL-X to exit
#: Your changes will be saved, and you’ll receive a notice about the number of changes to be submitted
#Now we need to upload our changes to gerrit for review.
#: <nowiki>git push ssh://<username>@gerrit.omnirom.org:29418/<project> HEAD:refs/for/<branch></nowiki>
#::  '''Example:''' ''<nowiki>git push ssh://UtkarshGupta@gerrit.omnirom.org:29418/android_frameworks_base HEAD:refs/for/android-4.4</nowiki>''
#: This will upload the changes, and you’ll receive a web link to those changes like https://gerrit.omnirom.org/1479/

For more information on Gerrit, see [[Gerrit Rules]].

== Creating a patchset ==
Now that you have created a patch, you may want to change it maybe because you have a better idea, or you did a mistake.
So let's begin
# Begin by performing a ''repo sync'' so that we know we’re dealing with the most recent versions of the code. We're also assuming that you have your Omnirom repo in ~/android/omni:
#: cd ~/android/omni
#: repo sync
# Now in terminal, navigate to the project directory.
# Cherry-pick your patch from gerrit.
# Make changes
# Now let's change our original commit
#* Let's check what all we changed
#:  git status  (''this will tell you the files that were changed'')
#* Now let's add the files
#:  git add <file name> if you need only some of the changed files
#:  or use git commit -A to add all the files.
#* We want to change our original commit instead of a new one
#:  git commit --amend
#:: This will open up the same editor we dealt with already
#* Get done with it
# Now the commit is ready to be pushed. This will edit the original commit instead of creating a new one.

== Getting lazy ==
Typing <nowiki>git push ssh://<username>@gerrit.omnirom.org:29418/<project> HEAD:refs/for/<branch></nowiki> everytime is a painful job.
# So instead of typing it everytime, we create a remote for it.
#: <nowiki>git remote add <name> ssh://<username>@gerrit.omnirom.org:29418/<project></nowiki>
# Using it
#: git push <name> HEAD:refs/for/<branch>

You'll have to create remotes for every project.

== Getting more lazy :) ==

Install git-review, here is [http://www.mediawiki.org/wiki/Gerrit/git-review a guide]

Git review config:
<pre>
<nowiki>git remote add gerrit ssh://<username>@gerrit.omnirom.org:29418/<project></nowiki>

git review -s
</pre>

Creating a patch:
<pre>
$ git checkout -b mycoolfeature
change files
$ git commit -a
$ git review
</pre>

Creating a patchset:
<pre>
$ git checkout mycoolfeature
change files
$ git commit -a --amend
$ git review
</pre>

== Licensing ==

It is important that any code you contribute follows either the existing licensing, or utilizes the correct licensing. For pre-created headers, see the [[License template]]
