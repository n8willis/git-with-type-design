# Git and why you should care

Git is usually described as a version-control system (VCS). The idea
of VCSes goes back decades in programming, and it focuses attention on
the idea that as someone saves newer and newer versions of a file, all
of the old versions get recorded in a database so they're not
lost. That's essentially like the "Undo" menu history in everyday apps
(including code editors), except it's keeping track of entire folders
full of files, and it's unlimited in how many changes it can
undo. Git and several other contemporary VCSes push that idea further,
with additional features like letting people keep track of multiple
versions of the files in parallel (so you can switch back-and-forth
between them) and offering functions for sharing and collaborating on
projects with people in remote locations.


## Versions are okay; history is great

I think that "version control system" puts too much emphasis on the
ability to undo changes, however, because undos are not the only
useful thing that git does for you, and usually not the most
interesting thing git does for you, either. Yes, being able to undo
changes is a huge benefit for programming projects, because
programming is about making changes until the code functions
correctly. So, when the code stops working, a VCS lets you undo it by
however many steps you need to until it was working, then try again.

That's a "success" in programming usage. But it's not really how a
"success" is defined for design projects. In a design project, when
you make changes to a file, it's not usually because the file was
broken before and now you're repairing it; you're changing it to
improve the design, to make various design elements look or work right
together, or to make the whole thing more acceptable, appealing, or
useful for users or clients. 

So, in type design, for example, if you make the horizontal strokes a
little thinner one day because you need to increase the stroke
contrast, then a few days later you are adding diacritics and you
determine that you need to make the horizontal strokes a little bit
heavier, you wouldn't _undo_ the changes you had made to the
horizontal strokes before. Because they weren't "broken": they were
not a mistake, you've just updated the design to work better. So the 
undo/roll-back-a-change feature isn't quite as central when you use
git for type design. [Don't get me wrong: it's definitely useful that
the old revisions get saved, but usually they're useful as things you
can go look at, rather than because you actually need to revert
changes and redo some work.]

But what _is_ useful is that git can track _why_ you made the
changes, with the *commit messages* that it logs every time you record a
change. That gives you a running record of what your design decisions
were -- and, over the course of a long project like a typeface, that's
valuable to be able to look back at (including as you're working and
if you come back to a project after time has gone by). It also happens
to be valuable when you share or collaborate with others.

That's why I prefer to think of git as a _changelog_ system: that word
includes both the "change" (that is, the old versions of the files)
and the "log" (the commit messages that you write). Which one of the
two is the most important varies from project to project, but they're
both important. For design projects, I tend to think the log part is
more useful in the long run. Although you do have to develop the habit
of writing useful commit messages (and doing them often enough).

In other words: write good commit messages that record what you were
thinking or attempting with your changes, and git automatically
becomes a detailed project diary that tracks your progress and your
process.

That having been said, git's ability to automatically save all the
previous versions of files in its changelog is great for your
workflow, because it means you don't _ever_ have to "Save As..." a
bunch of alternate or experimental versions of your files, and thus
add a bunch of extra files (with hard-to-remember-later filenames...)
on your hard drive. Extra, alternative versions of your project files
get out of control super fast, and they're hard to ever get sorted
back into order as time goes by. If you ever do decide you want to
jump back to a particular point in your project's history, you can do
that easily with git's "tag" and "branch" features, which we'll get
to; doing it with those features instead of doing it with a bunch of
separately-saved, separately-named extra files is a lot easier to keep
track of over time.


## Viewing file-version differences isn't very important

I also emphasize the importance of the commit messages because git's
built-in utilities for comparing two different revisions of a changed
file are basically beneficial for programming projects but are not
very useful for design projects.

The reason the comparison-of-differences utilities aren't very useful
for design projects is that they just compare lines of text. That kind
of comparison is exactly what people need when working on programming
projects, where a line like

```
if (SessionActive = True and CurrentCounter < 1):
```

might be where a bug snuck in, and the fix would be easy to see by
comparing it to the previous version of the line, like

```
if (SessionActive == True and CurrentCounter < 1):
```

But, unfortunately, git's comparison tools can't provide you with that
degree of clarity when comparing changes between versions of a font
file, because the changes are of a visual nature.

Technically speaking, it's true that font source formats (like .glyphs
or .ufo) are formatted text files, but if you were to look at the
differences in a .ufo file when you changed a serif or a crossbar, all
you would be able to see is a bunch of numeric coordinates inside of
nested XML tags. Which is not helpful.

Because git is so popular with programmers, you will likely read and
hear a _lot_ about the version-to-version comparison features. That
stuff is important for programmers, but it's safe to consider it
low-priority for design projects.


## Backups and sharing are really, really important

Git's changelog features are really useful, even though they do
require you to adopt a bit of discipline to write commit messages that
communicate what you're doing (and a bit of discipline to actually
save the changes regularly in commits).

Separate and completely unrelated to that benefit is the fact that git
can also send and retrieve files over the Internet. You don't have to
push copies of your project files anywhere at all, but it is a really
good idea to have external backups in case of disaster, and git offers
some convenient features to make that easy to do. And, probably
obviously, if your project is a collaboration in some way (formally or
informally), then being able to send copies of the files _and_ the
changelog with them makes the workflow a lot nicer in the long term.

From that Internet-connectivity functionality, git provides some other
features that you might find useful, like labeling things with
semantically important tags, but we'll get to that in due time. I just
think it's good to remember that git's changelog functionality doesn't
really relate to its Internet-connected functionality. In other words,
you can happily use git for your project entirely on one, single
computer, offline. But you will probably want to understand the
Internet-connectivity functions, because that gives you backup and
collaboration features, if you use it.


## Next: git setup and connecting your project to git

So that covers the high-level perspective of why git matters and what the
useful aspects of it are for type-design projects. Next, we will get
into the specifics, starting with how to use [git in the Terminal](git-terminal.md).

