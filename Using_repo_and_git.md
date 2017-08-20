
==Using Repo and basic Git commands==

Please have a look at Google's official guide: http://source.android.com/source/developing.html
* repo - http://source.android.com/source/using-repo.html
* github - https://guides.github.com/activities/hello-world/
* ssh - https://help.github.com/articles/generating-ssh-keys/

==Basic Git commands==

Need help with git? Don't forget about the man and help pages.
    git help
    git <command> --help
    man git

Clone a remote git repo into a local git directory.
    git clone --Clone a repository into a new directory.
    git clone git@github.com:omnirom/name_of_repo.git

*'''The following commands will be ran from within the cloned repo's directory.'''

Pulls all the changes from upstream.
    git pull --Fetch from and integrate with another repository or a local branch.

Returns some basic info
    git status --Show the working tree status.

Returns current branch
    git branch --List, create, or delete branches.

Switches branch that is currently being tracked.
    git checkout --Checkout a branch or paths to the working tree.
    git checkout <branch>
    git checkout android-5.0

This is a very powerful tool, everyone should get familiar using it.
    gitk --The Git repository browser.

==Troubleshooting==

===I'm getting "Permission denied" when trying to 'repo upload' a change===

Make sure you have an username set on your gerrit account at http://gerrit.omnirom.org

Then, make sure it is set properly in your git config by running the following command:

    git config --global review.gerrit.omnirom.org.username <your username here>

Another thing to check is that you have added your SSH public key to Gerrit
