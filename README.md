# Add issue id hook

## What is it?
Git commit hook for adding related JIRA issue id to commit messages. 

## How does it work?
Issue id is parsed from the current branch name and prepended to your commit message.


    $ git checkout -b ADD-12-new-feature
    $ git add some_code.py
    $ git commit -m "Added some pretty code."
    $ git log
        ...
        ADD-12 Added some pretty code.

Here's the specification from ``spec.py`` tests:

#### AddIssueIdHook:
 - prepends issue id from branch name prefix to commit message
 - doesnt modify commit message if issue id not in branch name
 - doesnt modify commit message if it already starts with issue id
 - doesnt modify commit message if issue id in branch name but not as prefix
 - doesnt modify commit message if in detached HEAD state
 - supports aborting a commit by providing an empty message
 - supports aborting a commit by exiting from editor without making changes

## Installation
1. Copy ``commit-msg`` file into ``.git/hooks/`` directory of your project's repository.
1. Open the newly created copy of ``commit-msg`` file and set ``project`` variable according to your project's name in JIRA.

This plugin requires having Python 2.7 installed.

## Known limitations
As this commit hook depends on parsing the current branch name, it won't work when committing in detached HEAD state, e.g. when doing a *reword* operation during ``git rebase --interactive``.
