[title:Git Notes]: /
[date:2012-08-24]: /
[menu:Git]: /
[template:page_toc]: /

# Git Notes  ###
A collection of my Git learnings. I'm VERY familiar with Mercurial but making the switch to Git. This will collect my thoughts, and notes for reference purposes. This is not a comparison of hg and Git. I just want to be familiar with both.

## Getting started
A good overview of basic Git functionality. [Git Basics Tutorial](http://marakana.com/s/git_basics_tutorial_example,1244/index.html)

A very helpful book: [Pro Git book](http://marakana.com/s/git_basics_tutorial_example,1244/index.html)

## Cleaning up unwanted changes
- Reset entire repo to last committed state:'git reset --hard'. This doesn't remove untracked files
- Remove untracked files, directorys:'git clean'. add -d to remove directories, -n to do a dry-run.

## Retrieving 'lost' changes
If you're not careful, you can appear to lose changes. Doing a careless checkout or reset --HARD can move you to a location, leaving some changesets with no connection to existing code.

git reflog is your friend. It keeps track of where you've been, and allows you to recover lost items. Reflog will show the previous locations of HEAD, and should have some sort of message that indicates where you did a hard relocate and left orphaned changesets.

Doing a git reset --HARD back should restore the changes.

## Useful configuration
git config --global will set the configuration 'globally'. i.e. it will be set for all repos unless overridden locally. --local sets it for the specific repo only

- Set username and email
	- git config --global user.name=name
	- git config --global user.email=email address
- create aliases for common commands
	- git config --global alias.co checkout
	- git config --global alias.ci commit
	- git config --global alias.st status
	- git config --global alias.diffstg 'diff --cached'
- Fix whitespace issues when applying a patch 'git config --global apply.whitespace fix'

## Convert Mercurial (HG) to Git
Instead of using hggit you may use hg-fast-export.

1. Create new git repo on remote server.
1. git clone git://repo.or.cz/fast-export.git
1. mkdir new_git_repo
1. cd new_git_repo
1. git init
1. /path/to/hg-fast-export.sh -r /path/to/hg_repo
1. git checkout HEAD
1. git remote add origin {remote server git path}
1. git push origin master

Appears hg-git introduces its own changesets into the stream...

## Patches
[Patch tutorial](http://ariejan.net/2009/10/26/how-to-create-and-apply-a-patch-with-git)

Summary:If all patches in a branch, simplifies process.

'git format-patch master --stdout > patchName.patch.

This will extract all changes on current branch from master branch. If want changes relative to another branch, change the master to something else.

To apply patch:

- Check what patch will do: 'git apply --stat patchName.patch
- Test patch: 'git apply --check patchName.patch
- Apply patch:'git apply patchName.patch'.
- If you want it signed because it's a patch from someone else, use 'git am --signoff < patchName.patch', and signed-off-by metadata will be added to the commit message.

If get whitespace issues, can remove patch, and turn on apply.whitespace fix to config

## Interactive Staging
One can obviously use the command-line tools, but I find some things easier to do with a GUI. git gui is very helpful for doing this. Allows one to see differences, and move lines/hunks quickly from/to staging.

## Mimic incoming and outgoing
Haven't gotten this working correctly just yet, but once figure it out, will update.
From Stack Overflow [question](http://stackoverflow.com/questions/231211/using-git-how-do-i-find-modified-files-between-local-and-remote/6389348#6389348)

Starting with Git 1.7.0, there is a special syntax that allows you to generically refer to the upstream branch: @{u} or @{upstream}.

To mimic hg incoming:

git log ..@{u}
To mimic hg outgoing:

git log @{u}..
I use the following incoming and outgoing aliases to make the above easier to use:

git config --global alias.incoming '!git remote update -p; git log ..@{u}'
git config --global alias.outgoing 'log @{u}..'
share|edit|flag
answered Jun 17 '11 at 17:18

Richard Hansen
4,0431123
 	
 	
git log ..@{u} gives me these errors. (I have both origin and an upstream repository in my git config). error: No upstream branch found for '' error: No upstream branch found for '..' error: No upstream branch found for '..' fatal: ambiguous argument '..@{u}': unknown revision or path not in the working tree. Use '--' to separate paths from revisions – hced Oct 1 '11 at 13:42
 	
 	
You'll get those errors if your local branch isn't configured with an upstream. To fix, run git branch --set-upstream foo origin/foo. – Richard Hansen Oct 1 '11 at 18:18
 	upvote
 	flag
worked well for me, cheers – Mark Simpson Feb 10 at 11:37


## Git on Windows
If you're using windows, then install Git from the main git page. This will also install git-bash, but if you don't want to work with a unix like command-line, consider using Powershell 2.0. There are a couple of handy items to help out. One for some command prompt changes that acknowledge git, and another for using ssh-agent.

- [ps-get to install posh-git](http://haacked.com/archive/2011/12/13/better-git-with-powershell.aspx): Use psget to install posh-git rather than following the instructions on the posh-git link
- [posh-git](http://lostechies.com/keithdahlby/category/posh-git/)
- [ssh-agent helper](http://markembling.info/2009/09/ssh-agent-in-powershell)
