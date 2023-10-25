# Git with type design

## Opinionated opinions on how git, GitHub, and related tools can fit into a typeface-design workflow
   
This is a document written for people doing type design. It won't tell
you anything about how to do type design itself (or, at least, not at
a significant level), but it will explain what value things like git
and GitHub can bring to a typeface project.

I think it matters to discuss these things in the specific context of
a type-design project, because git and GitHub come from the world of
programming -- and some pretty small niches _within_ programming, for
that matter -- which means that a lot of the generalized advice and
"howto"-style material you find if you just search online is going to
be focused on programming projects, with little to say that applies to
design projects and a lot that doesn't apply. Hence the choice of
titles: it's not "type design with git" because you're not using git
to _do_ type design. You're _doing_ type design, and if git has
something to help you get that done, great: let's see what that
helpful stuff is.

I'm also serious about the "opinionated opinions" part: this is my
perspective and I'm sure other people with experience would have
different things to say. But I think it makes for a more useful
document for one person to write it, intentionally, and to explain the
"why"s -- rather than trying to encapsulate every possible different
approach and viewpoint, which tends to result in a generic and
noncommital list of ingredients. So I am trying to say why I believe
some things are more important than other things: others may disagree,
and you might disagree, too, but at least I'll say why, and hopefully
that will connect the advice to the reasons and be more beneficial.

There are going to be four parts:

- An [overview](overview.md) of what git and GitHub do and why they do
  it that way. That's important because you only need to care about the parts of
  these things that matter for your type-design project.
- A walkthrough of how you use [git
  itself](chapter-1-git/git-basics.md) in a type-design
  workflow. That's important because all of the add-ons, GUIs, and web
  services (including GitHub) are secretly running standard git under
  the hood, so you'll be a lot better off using them once you know
  what they're hooked up into themselves.
- A walkthrough of how projects and repositories work on
  GitHub. That's useful because there are a lot of features and norms
  of GitHub that aren't really part of git and, here again, some of
  them matter for your type-design project and some don't.
- A walkthrough of the GUI app "GitHub Desktop" and some similar
  graphical tools. I think all of these tools I've seen have awkward
  UI and UX designs, so they are harder to get used to than they need
  to be, but yet again, the main goal is to point out how to find and
  use the parts of the programs that are valuable for your project.
  
(although, as I'm writing this, not all of those parts are done
yet....)

I suggest that you start at the overview page, even if you think it
isn't something you're interested in. Some of the overview stuff is
going to get referred to in the other parts, just to not repeat things
too many times.

I'm also adding some [resources](resources.md) made by other people, so you can get
additional perspectives and have some places to quickly go as you
continue getting git and GitHub integrated into your processes.

It's also worth keeping in mind that I'm mainly writing this from the
perspective of a type designer using a Mac, just because that's
helpful to the most people. Not much of it is specific to Macs or to a
particular font editor, but the examples and phrasing of terms leans
that way for convenience.

So that's it. Happy reading; please get in touch with me if you find a
typo or some other mistake, and please please even more get in touch
with me if you have a question that isn't covered. This document
exists solely to be helpful, so let me know how to make it ... more of
that.

Nathan Willis
n8willis
