title:Git Notes
date::2012-08-24

<p>A collection of my Git learnings. I'm VERY familiar with Mercurial but making the switch to Git. This will collect my thoughts, and notes for reference purposes. This is not a comparison of hg and Git. I just want to be familiar with both.</p>

<h2>Getting started</h2>
<p>A good overview of basic Git functionality. <a href="http://marakana.com/s/git_basics_tutorial_example,1244/index.html">Git Basics Tutorial</a></p>
<p>A very helpful book: <a href="http://marakana.com/s/git_basics_tutorial_example,1244/index.html">Pro Git book</a></p>
<h2>Cleaning up unwanted changes</h2>
<ul>
<li>Reset entire repo to last committed state:'git reset --hard'. This doesn't remove untracked files</li>
<li>Remove untracked files, directorys:'git clean'. add -d to remove directories, -n to do a dry-run.</li>
</ul>
<h2>Useful configuration</h2>
<p>git config --global will set the configuration 'globally'. i.e. it will be set for all repos unless overridden locally. --local sets it for the specific repo only</p>
<ul>
<li>Set username and email
<ul>
<li>git config --global user.name=name</li>
<li>git config --global user.email=email address</li>
</ul>
</li>
	<li>create aliases for common commands
<ul>
<li>git config --global alias.co checkout</li>
<li>git config --global alias.ci commit</li>
<li>git config --global alias.st status</li>
<li>git config --global alias.diffstg 'diff --cached'</li>
</ul>
</li>
<li>Fix whitespace issues when applying a patch 'git config --global apply.whitespace fix'</li>
</ul>
<h2>Convert Mercurial (HG) to Git</h2>
Instead of using hggit you may use hg-fast-export.

<ol>
<li>Create new git repo on remote server.</li>
<li>git clone git://repo.or.cz/fast-export.git</li>
<li>mkdir new_git_repo</li>
<li>cd new_git_repo</li>
<li>git init</li>
<li>/path/to/hg-fast-export.sh -r /path/to/hg_repo</li>
<li>git checkout HEAD</li>
<li>git remote add origin {remote server git path}</li>
<li>git push origin master</li>
</ol>

Appears hg-git introduces its own changesets into the stream...
<h2>Patches</h2>
<p><a href="http://ariejan.net/2009/10/26/how-to-create-and-apply-a-patch-with-git">Patch tutorial</a></p>
<p>Summary:If all patches in a branch, simplifies process.</p>
<p>'git format-patch master --stdout > patchName.patch.</p>
This will extract all changes on current branch from master branch. If want changes relative to another branch, change the master to something else.
<p>To apply patch:</p>
<ul><li>Check what patch will do: 'git apply --stat patchName.patch</li>
<li>Test patch: 'git apply --check patchName.patch</li>
<li>Apply patch:'git apply patchName.patch'.</li>
<li>If you want it signed because it's a patch from someone else, use 'git am --signoff < patchName.patch', and signed-off-by metadata will be added to the commit message.</li></li>
</ul>
<p>If get whitespace issues, can remove patch, and turn on apply.whitespace fix to config</p>

<h2>Interactive Staging</h2>
<p>One can obviously use the command-line tools, but I find some things easier to do with a GUI. git gui is very helpful for doing this. Allows one to see differences, and move lines/hunks quickly from/to staging.</p>
<h2>Mimic incoming and outgoing</h2>
Haven't gotten this working correctly just yet, but once figure it out, will update.
From Stack Overflow <a href="http://stackoverflow.com/questions/231211/using-git-how-do-i-find-modified-files-between-local-and-remote/6389348#6389348">question</a>
<p>
Starting with Git 1.7.0, there is a special syntax that allows you to generically refer to the upstream branch: @{u} or @{upstream}.
</p>
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