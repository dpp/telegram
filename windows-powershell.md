[title:Windows Powershell]: /
[order:20]: /

Still on Windows? Seriously consider Powershell. Amazing replacement for the command prompt.

Ensure you have Powershell 2.0. It's in Windows 7 by default.

Use PsGet for installing extras.

Can install posh-git which adds some sugar to the command prompt if you use git.

Install ssh-agent module to help with that. Currently see git page for details.

Use Console2 rather than command prompt/default powershell. Scott Hanselman provides [instructions here](http://www.hanselman.com/blog/Console2ABetterWindowsCommandPrompt.aspx). Note that to copy, one must hold down the left-shift key.


Commands can be verbose, but very powerful. `dir | ren -newname{$_.name -replace "a","b"}` will rename everything in the current directory, replacing a with b in the name.