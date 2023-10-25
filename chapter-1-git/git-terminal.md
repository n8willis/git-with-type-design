# Git in the Terminal

Originally, git was built to be used as a set of commands to be typed
in a Terminal. Newer GUI apps came later, and you might find them
useful, but the GUI apps can also be a bit of a pain because they try
to show every possible option, or they combine things together
weirdly, or they're just awkward GUIs. It's really better if you take
an hour or so and use the Terminal git commands first.

There are only a few commands that matter, and when those feel clear
to you, you will have an easier time with everything that
follows. This section will highlight the useful functions for design
work, and I'll also try to explain where some of the peculiar features
of git are unavoidable. Most of the peculiar parts of git come from
its history as a programming-tool project and are things it's safe to
not worry about.

We'll start with a bird's-eye overview, then talk about installing and
setting up git. Then we'll look at the key commands for getting info
about your project and we'll end with the key commands you use while
you're working day-to-day.

## Bird's eye view

Git basically has four top-level concepts that it works with. There's

- *your identity*, as the git user
- a *repository*, which is git's changelog for some set of project
  files
- a *branch*, which is the "current state of things" in a repository
- a *remote*, which is some other git repository living on some other
  computer other than yours.

Your **identity** is something that git actually stores a record of --
although you have full control over what details you enter for the
personally-identifiable portions. But you can't use git without
setting up some sort of general identity: the changelog that git
records as you work on a project always records who did what, which is
essential for things like online backup and collaboration.

Another useful part of your identity is that git lets you store
settings and configuration options; some of those you'll care a lot
about even if you aren't working on a multi-person collaboration
project.

A **repository** (or **repo** for short) is the changelog that git
records to track the progress and changes on a project. No repos exist
until you deliberately create them with the necessary commands.

Each repo is defined as existing in a particular folder, and by
default the repo would include every file in that folder and in any of
its sub-folders. That particular-folder definition tells git to watch
which files have changed within the folder. You can choose to exclude
specific files and things if you want to, though, in the configuration
settings for each repo. There are reasons you might want to, which
we'll get into.

Whether you define exceptions or not, git's changelog for the repo
only keeps track of changes to the files it is watching. It knows
nothing about stuff above the repo folder. 

That "defined on a folder" boundary is what lets you have multiple
repos for different projects on the same computer, each in different
folders wherever you want. But it also means that repos can't overlap
with each other: there is a maximum of one repo per folder.

A **branch** is something like a "timeline of changes" in the git
changelog for a particular repo. By default, whenever you create a
repo, there is at least one branch. These days, the default branch is
typically named something generic like "main", but you can change
that. It's purely a label for convenience. With only a single branch,
git functions like any other version-control system (VCS). For more
complex projects, git offers functions to create and manage multiple
branches (hence the name "branch"), so a lot of git documentation
spends time discussing branches and how to mange several at once for a
single repo. But, for getting started, it's just important to know
that there's at least going to be one branch, and if there's only one,
you'll be doing on your there "on" that branch.

A **remote** is shorthand for a remote repository -- specifically, a
copy of the same repo that you're working on. Git can connect your
repo to a remote and use it as a backup location that keeps track of
things just like your local git does. In a way, that's the fundamental
service that GitHub provides: you can connect your local repo to a
remote on GitHub, where the GitHub servers run their own instances of
git. The GitHub site provides a convenient web front-end for other
people to look at the files or to download their own copy. It's
possible to have a remote somewhere else, though, and you can have
more than one remote connected to your local repo.

Just remember that the remote is another copy of the _same_ repo, and
there is _another_ git program keeping watch over it on the other
computer. You can't connect two unrelated projects as remotes to each
other: the git changelogs would be an incoherent mess. It's also not a
remote if you just copy all the files in your project folder and paste
them into Dropbox or Google Drive, because there isn't a copy of the
git program there, monitoring and recording changes.

Most importantly, however, it is up to you to remember to synchronize
your local git repo with the remote. It doesn't happen automatically.


## Installing and setting up git in the Terminal

With that basic conceptual stuff out of the way, we can start
by installing and setting up git in the Terminal. How you install git
can vary from computer to computer, and the info I have seen online
seems to change regularly. For a Mac, for example, some things I read
say it comes pre-installed these days; other people say you have to
install Xcode and git is installed automatically with that. You _can_
also install one of the GUI apps, such as GitHub Desktop, which also
ensures that git is installed.

Ultimately, the method you use to install git doesn't matter, so I
prefer to point to some general instruction pages from well-known
sources, and we'll trust that they keep up to date. Here's GitHub's
"install git" page:
[https://github.com/git-guides/install-git](https://github.com/git-guides/install-git)
which points to several of the most reliable options.

However you get it and install it, we're going to be working in the
Terminal, so open the Terminal app. You can type `git version`, hit
Return, and if git is installed it will print out what version number
it is. The version number doesn't really matter here; it's just a way
to see for certain that the `git` program works.

It's also a convenient demonstration of how git in the Terminal
works. Git itself is one program with a ton of different functions, so
whenever you do something with it, what you actually type is `git`
followed by some particular git function ("function" or "command"
both refer to the second word; you'll see people use both terms). In a
lot of cases, you also type some parameter or message after the
function, but not always.

There are a few handy, information-reporting commands you'll want to
use regularly. The `git version` one just gives you one piece of
information. A more useful one you should try is `git config --list`. This
prints out a summary of how your personal git setup is currently
configured; the `config` command tells git to access the configuration
settings, and the `--list` tells it to just list them out. The `list`
here that comes after the `--` is sometimes called a "flag" and
sometimes called a "switch". They mean the same thing; the `--` prefix
just tells git that what comes next is some sort of option.


### Setting up your identity

As mentioned in the bird's-eye view, you have to set up some sort of
identity to use git. In the terminal you do that with some more uses
of the `config` command. There are only two settings that are
mandatory: a name and an email address. You set your name with

```
git config --global user.name "Jan Doe"
```

and you set your email address with

```
git config --global user.email jandoe@example.com
```

In these commands, you can see the `--global` switch, followed by
which configuration field you're setting (`user.name` or `user.email`)
and the value you're setting it to.

> At this point, you might well wonder _why_ an email address is
> mandatory.... If you aren't sending git projects with your email, why
> does git need anything? And why can't you use some _other_ contact
> info instead of an email address, like a phone number, social-media
> account, or a web address?
>
> Well, the answer is that this is one of those places where git's
> origin as a tool built for the Linux kernel project shows
> itself. The kernel programmers use email for everything they do, so
> email-as-mandatory got baked into git, too.
>
> If you are worried about your privacy in this sort of stuff, you can
> put in made-up values for your name and email. But be careful; that
> could cause some unexpected surprises in the future, particularly
> when collaborating with other people.


### Setting up a repository

After you have your basic identity stored in git's configuration (you
can check to see that it looks right by running `git config --list`
again), you can set up a project repository (or _repo_).

You have to do this repo-setup step with the Terminal app "running in"
the folder or directory that you want to use as your repo's
location. Remember: a repo is defined as being inside a specific
folder. This part is definitely something that the Terminal makes
harder, because the Terminal app doesn't really show you what folder
it thinks it's "in" (and, to be honest, it's not like the Terminal app
is _inside_ the folder at all; that's just historical terminology from
years and years of computer history). In the Terminal, you can see
what folder the Terminal considers to be its current location by
typing the command `pwd` and hitting Return. It prints out the
location, using `/` slash characters to separate folder names. By
default, the Terminal launches itself in the base user account
directory, so what it prints is probably something like
`/Users/jandoe`.

You need to set up your repo in the folder that you plan to use for
all of your project's files. If you're familiar with the Terminal app,
you can change to the folder you want. If not, you can find the folder
where you plan to keep your project files in the Finder and choose
`View > Show Path Bar` from the menus. That will show you the location
of the folder you need: select and copy the "path bar" location for
the folder -- or keep it where you can see it -- and, in the Terminal
app, type `cd _Paste_Or_Type_In_The_Path_Bar_Location_` then hit
Return. So, for example, `cd /Users/jandoe/External
Drive/Projects/Font 1` or something like that. That tells the Terminal
app to change its current "location" to the folder you want. You can
check that it worked by running the `pwd` command again.

Once you've gotten that to work, all you have to do to set up git for
the project is type `git init` and hit Return. When you do that, git
will set up a brand-new repo (with a totally empty changelog) and it
will be pinned to the folder you are in.


### Getting basic information from git

Immediately after you set up a new repo, there won't be anything
interesting about it. By default, git is not going to watch for
changes on any particular files, for example. Repositories also don't
have "names" or identifying features of their own; they're just
changelogs, and they start out empty.

The one possible exception to this rule is that git _does_ set up a
default branch. As we saw earlier, the default branch is usually named
something generic like `main`, but whatever it's called, at step one,
it's empty.

So, before going any further, it's worth making note of a handful of
basic information commands that you can run in the Terminal app at any
time to get info about the present status of things in a repo. The
most general of these commands is (no big surprise) `git
status`. Typing that in the Terminal and hitting Return will make git
print out a summary of what it's current changelog state is _for_
_the_ _repo_ and what it knows about the other files in the repo's
folder, in this order:

- a line saying what branch of the repo is active
- a line reporting the state of the branch
- a list of all the files git can see in the repo
- a line about the state of the current or upcoming changes

The very first time you do this, the branch will be `main` or whatever
the default branch name is. The state of the branch will say something
like "No commits yet." Similarly, the state of the current or upcoming
changes won't have anything to report to you, so it will just say
"Nothing added to commit" or something like that.

If you ran `git init` in a new, empty folder, then the list of files
won't have anything in it. However, if you ran `git init` on a folder
that already contained a lot of project files, git will list them all
in alphabetical order, under the heading "Untracked files:". After
you've been working in the repo for a while, the list will also
include all the files that have been updated or changed, listed under
their own heading, "Changes not staged for commit:".

In the long term, that list is really useful, but git does
highlight some of this info -- including the "Untracked files" list --
in red, so that might seem disconcerting. It's nothing to worry about:
the highlighting is there because, months and months into a big
project, you might find yourself in a situation where you accidentally
overlooked a file that's pretty important, and the highlighting will
help you catch that oversight. People do that sort of thing all the
time; git's highlighting is just there to try and grab their attention
to be helpful.

In the future, though you should remember to run the `git status`
command fairly regularly, because it shows you exactly what git's
current understanding of the repo is, and if you make a habit out of
it, then if will be that much easier for you to notice when you've
accidentally overlooked something.

The next useful command to try is `git branch`. If you run this in the
Terminal app, it will print out a list of _all_ of the branches that
git is keeping track of for the current repo. At the very beginning,
there won't be much to print out (basically just `main` or whatever
your default branch is named. But git will print an `*` next to the
"live" branch if your repo has more than one branch, which can be
quite a helpful reminder if you've been away from a project for a
while and don't quite remember how you left everything.

> It might seem weird that the command here is _branch_, singular, and
> not _branches_, plural. I agree; it's just a historical fact of
> life. It probably just comes from the fact that there are several
> optional switches that you can tack on to the end of the basic
> branch command that do other things, and the singular version sounds
> more natural for those.

There are basically three other git commands that are useful for
getting information about your repo, but at the very beginning they
have literally nothing to report back to you. Still, I think it's
useful to know that they're there, because you can start running them
in the Terminal app immediately after you start working on changing
some file in your project. Informative commands are always good to
keep in mind, because they just return information to you and don't
have any risk of accidentally changing things. Feel free to not spend
a lot of time on these at the start of your project, but be sure to
remember that these are here, so you can come back to them at any time
and safely ask git for useful information -- especially if some
unexpected situation comes up.

THe first of these commands is `git log`. This command will print out
a list of all the commit messages that you have saved in the repo as
you've been working. In a sense, this is the "easy to read" version of
the repo's changelog. No matter what happens, it's helpful to be able
to see a list, in "most recent first" order, of your previous work.

You will likely also want to remember `git tag`. This command will
print a list of all the "tags" you have added to your project's git
changelog. Each tag is a semantic label that you pick and attach to
the changelog whenever you want as you work. Tags are 100% your
choice; you can use them to mark significant points in the progress of
your project. It's a good idea to make use of tags, because as your
project history gets longer and longer, it takes ... well ... longer
and longer to scroll through. So you can bookmark significant
milestones by adding a tag to each one as you work, and it's easier to
navigate back through the history when you;re reviewing it. A lot of
commercial and public projects use a tag to mark when a big, new
public release is published; that's definitely an excellent practice
to get into. But don't forget about tags in between big releases,
either. They're your checkpoints, and whatever else happens, git is
there to make the project easier for you to manage.

Finally, you will want to remember `git diff`. This is a command that
will print out all of the changes to the files in your repo _since_
the last time you made a "commit". I said earlier that git's
difference-comparison tools aren't great for visual projects like
typeface design, and that's still true. But there will be times when
you need to figure out (or just remember) what has changed since the
last commit got logged, and `git diff` will show you exactly that
information, with no risk of the change getting lost. For example,
when you run `git status`, you might occasionally be surprised to see
a file listed in the output as having been changed; in those cases,
`git diff` give you a quick way to see what is different. Besides,
almost all projects have some plain-text files involved (such as the
license and the README file); you'll definitely want to be able to
see changes to those text files in a convenient way.


### Daily workflow with git

Once you've set up your basic identity and configured the repo for
your project, you're actually ready to start working. As you work on
your files in a live repo, git actually just sits idle until you do
something with it. So it really is on you to develop the habits of
committing and logging changes and so on, which you can do with
Terminal commands.

#### How it works

Git keeps track of the state of a repo in three basic parts. First,
there are the actual files in the folder. Git can check and see when
they're changed.

Second, there's a "staging" zone. This is a temporary list of any
changed files that will go into the next commit to git's
changelog. When you run `git status`, like we did above, all of the
output it reports to you about tracked and untracked files and
upcoming commits is the current state of the staging zone. You have
full control over what's in the staging zone: you get to add updated
files to it, you can intentionally remove updates files from it, and
you can let the list sit there for as long as you like before you have
git commit the changes. After you make a commit, the staging zone is
automatically reset to be an empty list again, and it's ready to be
used for the next commit.

The third part of the repo is git's database of changelogs and related
status info. You don't see that database directly, because git stores
it in an invisible folder named `.git`; you interact with it by
running the different git commands in the Terminal.

In your regular workflow, you'll make some changes to files, then add
them to staging with a git command, then (finally) you'll make a
commit with another git command -- and with the commit, you add the
useful information like the message of what you changed about the
files and why. Those three steps reflect the three parts of the repo:
the files are files you edit like you normally would, staging is the
list that you prepare of the updated files, and when you make a
commit, the list that you prepared in staging gets logged into the
database.

The staging zone doesn't get talked about nearly as much, because it's
sort of an intermediary step, so it might get overlooked in some other
git or GitHub guides and be more confusing than it should be. I think
the key thing to remember is that "staging" is simply a list. You get
to change as many files as you want, at whatever pace you want to
work. When you add the changed files to staging, what you're doing is
assembling the list of updates that go together at the moment: the
changes that mean something together. You have to put that list
together before it gets logged as a commit every time, so it's
something you will have to think about regularly, and it can help you
keep your project organized.

For example, if you have edited three files since the last commit, two
of them might belong together (for example, you updated two .glyphs
font files) but the third file might be something else (like a
reference image). You _could_ just add everything to staging together
and put them all in one commit, but in the long run, it's more helpful
to stage the two updated font files together, and log them in one
commit, then afterwards stage the reference image and log it in
another commit by itself.


#### Workflow commands

Here's what the standard workflow looks like in the Terminal
app. First, you can run `git status` and get git's report on the
current state, including the list of all the new and changed files.

You now have to decide which of the new or changed files you want to
package together in the next commit. My advice there is that you be
guided by how easy it is to describe what's changed -- because I
believe that a readable list of commit messages is the most important
thing about a repo. If it would take three or four sentences to
describe what's changed in a set of updated files, then maybe split
them up into a few separate commits you can describe easily, rather
than doing them all at once.

Whatever you decide, you add the updated files to staging by typing

```
git add thefirstfile.ufo
```

(or whatever the actual file name is, of course) and hitting
Return. You do this for each of the files you want to bundle up into
the commit. If you add a file to staging then change your mind about
it, you remove it from the list by typing

```
git reset thefirstfile.ufo
```

(or whatever it's called). The actual file itself is unchanged; the
`reset` command just takes the filename off of the staging list. You
can check the current state of the staging list by running `git
status`, of course. It will list the staged files under the heading
"Changes staged for commit:" and (usually) highlighted in green. 

You use the `git add` command for every updated file that you want to
stage for the next commit, but you _also_ use it for every new file in
the repo when you first add the file or when you create the repo for
the very first time. At the beginning, with a brand-new repo, all of
the files that git can see are listed below that "Untracked files"
header: that shows you that git knows about them, but it is not
recording changes on them in the changelog.

So, at the beginning, git isn't actually monitoring any files at
all. You have to add each one that matters. You can use a shortcut
with `git add` to add literally every file to staging, with the `*`
wildcard symbol:

```
git add *
```

instead of a filename. It's quick way to get started. But do make sure
you haven't accidentally added some stray unrelated file to staging:
run `git status` to double-check.

As soon as the files you're interested in (new or updated) are in
staging, you are ready to make a commit. You do that with

```
git commit -m "Here you type a commit message to summarize the changes"
```

What you put in the quotes is the "commit message" and you want it to
be a convenient summary that you can look back on and understand. If
this is the very beginning of the repo, and you've added all the files
because you're just starting up, then it's 100% fine to write
something more general: many, many, many people write "Initial
commit." for that first commit message.

> Getting a little more complicated, there are some advanced features
> in git that let people write a short commit message and also attach
> a longer, more detailed message to it separately. Some of the GUI
> git apps even do that by default.
>
> My advice is don't worry about the length of the commit message _at_
> _all_. Write whatever you want, write it as long as you want and as
> detailed as you want. The only reason some people care about short
> or not-so-short commit messages dates back to git's history with the
> Linux kernel project, where everything is run through email -- and
> they used to put the commit messages into email Subject lines. But
> it doesn't matter to anybody else, so write anything you want. The
> messages are meant to useful to you.

Once you've written that commit message (don't forget to include the
`-m` switch and the quotation marks) and hit Return ... you're
done. The commit has been made; it is logged in the changelog
database, and staging has been wiped clean. You can now take a look at
things in their new state by running `git log`. You'll see your commit
message, so you'll know it worked.

If you've tested this out by now or have just looked through that `git
status` report in detail, you may be wondering about what to do for
files in the repo that you don't want git to care about. For example,
if you export your typeface design to a font file, you generally do
not want to keep adding all the .ttf and .otf output files to the
repo: they're not what you "work on"; you don't make changes to them
-- they're the end product.

Git has a solution for this: you create a new file in the repo (and
make sure it's in the base folder of the repo, not further down in
some subfolder) and name the file `.gitignore` -- be sure that the
file name starts with that `.` dot.

This file is supposed to be plain text, so you can create it with
TextEdit or any similar app like that. In the file, you list any
filenames or "filename patterns" that you want git to not pay
attention to. For starters, on a Mac project, you will want to have at
least this one line:

```
.DS_Store
```

That tells git to ignore some OS bookkeeping files. If you're working
in the Glyphs font editor, you'll also want to add these lines:

```
*(Autosaved)*
UIState.plist
```

to tell git to ignore some of Glyphs's bookkeeping files. I would also
recommend that you add some lines to ignore the generated font binary
files that Glyphs exports:

```
*.otf
*.ttf
*.eot
*.woff
*.woff2
```

unless you are absolutely certain that saving every exported file is
necessary.

All that these lines in the `.gitignore` file do is tell git not to
monitor files matching those filenames (including the `*` symbol as a
wildcard) whenever it reports status to you. So it prevents `git
status` from outputting extra lines that you don't care about, and it
prevents git from raising unnecessary warnings about things having
changed.

Another strategy you can use to simplify what git reports to you is to
put a folder name into the `.gitignore` file. For example, you could
configure Glyphs to export all of its font output files to a folder
named "output" in the repo. Then, in the `.gitignore` file, you could
just put

```
output/
```

and everything in the "output" folder will be safely ignored. Do
remember to put that `/` at the end of the folder name; that tells git
it refers to a folder. But you do _not_ need to put the `*` wildcard at
the end: git will ignore everything inside the folder.

You might also want to create a folder or two for temporary files or
experiments and add those folders to the `.gitignore` file in the same
way, or perhaps to ignore a folder that you use for massive,
full-color scanned source images or something. It's up to you. The
purpose of `.gitignore` is to cut down on the number of unwanted lines
in the `git status` output and make things more convenient for you as
you work.


### Summary

That really is all there is to the standard git workflow. You may also
know (or have seen) discussions of other git commands like `git push`
and `git pull`. Those are important, too, but they deal specifically
with git's remote-server features, so to talk about how they work,
we'll have to get into how GitHub (and similar services) work, and
that's for the next section.

For now, the commands discussed here let you work with git even if
you're working on a solo project or are offline from the Internet
entirely. And that's useful: git's ability to watch for changes and to
keep a detailed changelog for your project as you work is the main
thing. Connecting that up to the Internet and remote servers is an
extension into new territory. But you don't have to evern worry about
that on day one. You can spend weeks, months, or even years working
with git on your project, and only link it up to a remote server at
the very end.

The main takeaways you should feel comfortable with after this section
are the bird's-eye basic concepts (your identity, repos, branches, and
what remotes are), the setup commands (like `git init`), the info
commands (mainly `git status` and `git log` at this point, but the
others will get more useful as you go along), and the general workflow
of using `git add` and `git reset` to load up the right files into
staging, followed by `git commit -m` to make and save a commit.

If any of those bits are still not clear, it might help to back up and
go through them again, but if that doesn't do it, just contact me the
author: I really want to know what parts are proving useful and what
parts need improvement.
