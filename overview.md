# What is git and why do so many people care so much
## Some background

It's probably important, here at the beginning, to put git and GitHub
into context. Because they're wildly popular ... at least, as of
today. So everyone hears a lot about them and they become the default
"how to do stuff" option.

But they've also each got their own peculiar, specific histories to
them, which affects things like what all the components are named and
how they work. None of that stuff is magically or inherently the right
(or only) way it could be set up: it's just the way it happens to be
because of how it went yesterday, and last year, and so on.

If you keep that in mind, then when some aspect of git or GitHub seems
awkward or overly complicated, there's less risk of falling into the
trap of assuming that _you_ need to adjust your thinking, or that
_you_ are the odd one out for not liking it, or anything like that.

You probably know that git is a utility for "version control" and that
GitHub is a site where people post source code and general
software-like projects for the public and usually for free. But
there's weirdness and quirks in the way both of them do the
specifics. A lot of times, it is the way it is just because of history
or somebody had to make some sort of choice and run with it.


### Git and Linux

Most specifically, it's probably important to understand that git grew
out of the Linux kernel project — which is a massive, collaborative
software project that just focuses on building one thing: the Linux
kernel
([wikipedia](https://en.wikipedia.org/wiki/Linux_kernel)). That's the
core-level operating system layer that has to handle everything from
controlling the RAM and filesystems on disks to sending and recieving
network traffic to swapping control back-and-forth between all the
programs running simultaneously on the computer (and hopefully doing
that efficiently and "fairly", for whatever definition of fairly you
decide on).

The important bits of that backstory are that (a) the Linux kernel
project involves a huge, work-remotely team of programmers in
different locations, who all have various employers, and (b) the Linux
kernel itself has a ton of different subsystems (and sub-subsystems)
for all those different tasks that make up what-the-kernel-does.

As a result, the Linux kernel project has a lot of subdivisions: teams
and sub-teams of programmers who ware working on related components,
and they have an overall hierarchy of how all the components come
together to eventually get stitched into one working, combined
whole. For example, the WiFi people work on adding support for the
next new WiFi version, and the Bluetooth people work on updating
Bluetooth, and only when those individual subsystems are both
successful at the new revisions do they get merged up a step together,
into the next-level-up of the networking subsystem.

The programmers also all work remotely, and there are so many of them
that it would be incredibly difficult (or expensive) to try and keep
everybody's copy of the software source code in a single location or
to keep it all synchronized all the time: thousands of people,
in thousands of locations, and each person potentially keeping track
of multiple revisions.

Managing _that_ situation, without ever getting any tiny part of the
software source code lost or mangled, is what git was created to
do. There were version-control tools before git, and plenty of others
are still around today, but the pressures of working correctly for the
Linux kernel project eventually made git extra robust and extra
efficient.

Nevertheless, there are several functions in git and design-patterns
in how git operates that stem from this history, but which are not
particularly beneficial to other projects or make a difference  at all
to other projects. That's because, for example, smaller-team projects
are different, visual-design projects are different, and
single-employer (or "single-foundry") projects are different.


### GitHub the service

Despite the similarity of the name, GitHub is a separate
entity entirely from the git software utility itself. GitHub's main
purpose is to publicly host software projects (or software-related
projects) and provide services that projects use for day-to-day
operations, like discussions and planning. 

You can use the git Terminal programs to perform a lot of tasks
intereacting with projects hosted at GitHub — most importantly,
downloading and uploading. But you can use git without GitHub, you can
do a lot of things with GitHub-hosted projects without creating a
GitHub site account, and there a lot of things you can do on the
GitHub site (or in the GitHub desktop app) that don't involve the git
program itself.

Since it has been around, GitHub has become popular with a wide
variety of software projects, and a lot of the things that make it
popular are free site features that are not related to git. Partly the
popularity is because of all the features and the fact that
programmers find them useful; partly the populaBrity is because the
services are free, and partly it's a popular site today because it was
popular last year, too and there's a strong "the more the merrier"
effect and long as it stays popularr with users ... which is the sort
of thing that could actually change.

Regardless, the GitHub service (including the non-git-related
features) and the terminology that comes with it has become common
enough that you hear it even outside of GitHub-specific
discussions. But, like git itself, there are quite a few aspects of
GitHub that don't matter for type-design projects and it's fine to
pass over them.


## The essentials 

To whittle the get-up-and-running material down to the absolute
essentials, it is best to think of the following:

- Git is a changelog-management program. Its main value is that you
  can use it to keep a stable record of the changes that you make in
  the files of your projects. But you have to take the steps of
  recording the changes and recording changes for the important files,
  or else it isn't valuable.
  
- Your local git program can send and retrieve changelogs and files to
  git programs on other, remote computers, which means it can do
  backups.
  
- GitHub is a free service that you can use as a remote git backup
  location. The service also provides people with a conveient
  public web-interface, so you and other people can browse the files
  and changelog, search for things, and comment on discussions about
  things in the project.
  
Beyond that, there's just a big bag of individual features that may or
may not be useful in your project.
