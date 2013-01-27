---
layout: article
category: meetings
title: "Meeting Notes: August 2012 at Puppet Labs"
---

<pre>
We had a great meeting. There was lots of discussion and hopefully everyone learned something. I'm grateful to all the folks that contributed questions and comments throughout the evening. 

Here's some of what we talked about tonight....

"Git Describe" by Jonathan "Duke" Leto
PDF for this presentation will be posted soon
Annotated tags (git tag -a ...) allow you to sign a commit and add a message. Seems preferred to lightweight tags (git tag ...): http://stackoverflow.com/questions/4971746/why-should-i-care-about-lightweight-vs-annotated-tags
My understanding is that signing and annotation are in fact mutually exclusive---you can either supply `-a v1.0 -m "this tag is annotated"` and get an annotated tag, or you can supply `-s v1.1 -m "this tag is signed"` and sign the tag using the gpg key associated with the git user's email. You can also provide a key in git config.
Git can be used for all sorts of versioning of data:
gollum is a wiki running on git: https://github.com/github/gollum
Image diff using python: https://gist.github.com/1716699
Image diff using github: http://goo.gl/yfpqR

"Git GUIs" by Igal Koshevoy
I'm a big fan of the shell, but revision control is one of those cases where an interactive tool can really make my life easier. These tools eliminate a lot of tedious, complicated and repetitive commands and save you from having to remember the state of your repository. Sadly, none of these tools are friendly wizards that hold your hand -- you still must understand Git concepts, terminology and workflow to be able to use them effectively.
git gui
Cross-platform and bundled with Git
Manage branches, view status, stage files/hunks/lines, commit, amend
Alias: 
g = !git gui &
Tutorial: http://nathanj.github.com/gitguide/tour.html and search for "Git GUI Here" and begin reading there
gitk
Cross-platform and bundled with Git
View history for current branch, review changes, search, manage branches, format patches, cherrypick
"Markup words" setting shows just the words that have changed in a line. Equivalent to git diff --word-diff on the command line.
View history for ALL branches: gitk --all
Aliases:
k = !gitk &
ka = !gitk --all &
Tutorial: http://lostechies.com/joshuaflanagan/2010/09/03/use-gitk-to-understand-git/
qgit
Needs Qt. May be hard to compile on anything other than Linux.
Better at displaying tree of commits, but worse at everything else.
Download: http://sourceforge.net/projects/qgit/
gitx
Mac only
Many forks are available: http://gitx.org/
This fork is actively developed: http://gitx.laullon.com/
diffuse
Cross-platform, third-party
View changes: git difftool ...
Resolve collisions: git mergetool
Download: http://diffuse.sourceforge.net/
Add to ~/.gitconfig:
[diff]
	renames = copies
	tool = diffuse
[merge]
	tool = diffuse
	conflictstyle = diff3
	log = true
[mergetool]
	prompt = false
	keepBackup = false
	keepTemporaries = false
meld
Cross-platform, third-party
View changes: git meld
View diff of an entire tree for a revision: git meld $REVISION
Download the tool itself: http://meldmerge.org/
Download and install this so you can run `git meld`: https://github.com/wmanley/git-meld
opendiff
Like diffuse and meld, but only for OS X
git-cola
Cross-platform, third-party
Provides git gui and gitk features
Site: http://git-cola.github.com/
tig
UNIX only
Console-based interactive tool
Used by some smart people, but requires memorizing many keystrokes and keeping track of stacked interface
Manual: http://jonas.nitro.dk/tig/manual.html
Download: http://jonas.nitro.dk/tig/

"Local development workflow" with Git by Igal Koshevoy
The ability to do the workflow below is THE reason that I switched to Git....
Create and switch to a new "raw" branch, do NOT push this ever, it's only for you, not for sharing
Hack with reckless abandon and make messy commits that don't interfere with the "flow" of your problem-solving process. Obviously make good commits with reasonable commit messages whenever possible.
Spawn more branches as needed to explore different solutions. Switch back or back out changes that don't work.
Continue till you have a good solution and clean code committed.
Be a good citizen and write tests and such. :D
Create and switch to a new, properly-named clean branch.
Change your Git commit history to make it clear, logical and correct by eliminating errors, combining changes, and writing useful commit messages: git rebase -i master
Why? Make it easy for reviewers to read, understand and accept your changes, and make it easier for everyone to read your changes in the future.
Maybe merge this clean branch into master if appropriate.
Publish the contents of this clean branch or the updated master. 
Get rid of all the obsoleted "raw" branches you produced while hacking.
Practice rebasing on a throw-away repository until you can do this without shooting yourself in the foot.
Never rebase stuff that you've already pushed because it'll cause grief for anyone using your repository since they won't be able to easily pull changes any more.
Tutorials on rebasing:
Video demonstrating all the rebase features, view it in full screen so you can see what's going on: http://www.youtube.com/watch?v=ZLdcqIvnYPs
Commands: https://help.github.com/articles/interactive-rebase
Concepts: http://www.jarrodspillers.com/2009/08/19/git-merge-vs-git-rebase-avoiding-rebase-hell/

Perry Wagle
https://code.google.com/p/gource/
fun visualization of repo histories

Git philosophy
These two Google Tech Talk videos give remarkable insight into the minds of the creators of distributed version control systems, their priorities and how they choose to explain what they've done:
Linus Torvalds on Git: http://www.youtube.com/watch?v=4XpnKHJAok8
Bryan O'Sullivan on Mercurial http://www.youtube.com/watch?v=iR0rBYI1gy4

Git hooks
These provide a way to execute code on either the client or server for specific events, e.g. before accepting a commit.
Documentation:
http://git-scm.com/book/en/Customizing-Git-Git-Hooks
http://net.tutsplus.com/tutorials/tools-and-tips/quick-tip-automation-with-git-hooks/
http://www.kernel.org/pub/software/scm/git/docs/githooks.html
Examples: 
Heroku deploys a new version of your application when you push commits to a special repository: https://devcenter.heroku.com/articles/git
Gerrit adds changes to a code review system when it's pushed: http://code.google.com/p/gerrit/
Travis CI fires off tests when you push changes: http://travis-ci.org/

Programmatically interacting with Git
For simple stuff, just invoke shell commands.
For reading data or performing complex changes that may rely on commands that change between Git versions, use bindings.
Bindings are provided for many programming languages. EGit .g. Ruby bindings for Git: https://github.com/mojombo/grit
Or consider using libgit2 with bindings for a fast, self-contained C library that makes it easy to embed Git support in your app: http://libgit2.github.com/

Git configuration
Create a "~/.gitconfig" file and put your customizations there.
Duke Leto's: https://github.com/leto/Util/blob/master/config/.gitconfig
Igal's: https://gist.github.com/3495650

Git prompt
Display Git repo, branch and other useful information in your prompt.
Example: https://gist.github.com/3495692
When the above is sourced, you can run `myprompt; devprompt` and get a prompt with Git repo name, branch name, RVM version, RVM gemset, and whether last command exited successfully:
    myproject^mybranch ∴ ree-1.8.7-2011.03@everything :) 
Or `myprompt; gitprompt` for username, hostname, Git repo name, branch name, command number, time, and whether last command exited successfully:
    me@myhostname:myproject^mybranch #1234 00:34 :) 
</pre>
