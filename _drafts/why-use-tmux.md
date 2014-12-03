---
layout: post
title: "Why Should I Use Tmux?"
date: 2014-01-07 22:00
comments: true
---

## TL:DR
If you're an intermediate (or better) vim user and you haven't given tmux
a chance, do it. Expect to spend a good chunk of time customizing your tmux.conf.
Once that's in place, you'll wonder why you wasted all that time reaching for your
mouse.

## "What problem is tmux solving for you?"
For the last 2 years I've used vim nearly everyday. Along the way I've learned a
lot from browsing docs, reading blog posts, and practicing a ton. The highest yield 
technique for improving my vim skills, however, has been discussing tools and 
workflows with fellow vimheads.

On several occasions during these collarabitve discussions the topic of tmux
has come up. Despite this, I never felt compelled to explore it. Why not?
Unlike the
myriad of vim patterns, plugins, etc. that came up in these discussions, no one
seemed to be able to provide a sufficiently compelling reason for using tmux.
"What problem is tmux solving for you?" I would ask. The answers were underwhelming:
* it has tabs (windows in tmux parlance)
* it support horizontal/vertical splits
* it's a glorified wrapper for screen

After reading [ tmux: Productive Mouse-Free Development ]( https://www.goodreads.com/book/show/13506825 )
and refining a workflow with tmux at its core, I can safely say **tmux can do a lot more than that boring crap!**


## What problems is tmux solving for me now?

* I can now copy / paste any text that appears in any terminal output without ever touching the mouse.
* tmux's multiple copy buffers `PREFIX + =` take it to a whole new level
* [vimux](https://github.com/benmills/vimux) run tests and arbitrary code without ever leaving vim. This has to be experienced to be properly appreciated - it's a game changer.
* I now have 1 command that launches *everything* I need to start writing code: vim, terminal, local server, REPL, etc.
...

## Mouse-free copy/paste

I need to say this up front: if you don't grok vi motions, this feature is going
to be rather confounding. If you aren't comfortable with vi, tmux's copy mode 
will almost certainly slow you down.

If you're a vim user and h, j, k, and l are your best friends, then this isn't going
to be much help either. If this describes you, please check out [ vim-hardmode ]( https://github.com/wikitopian/hardmode ).

On the other hand, if you already think in terms of `?, /, f, F, t, T, ;, w, W, b, B, etc.`
then you're in for a treat. 

## The multiple copy/paste command composition workflow

let's say you have 3 panes (splits) open in your current tmux window (tab).
Let's call these splits A, B, and C.

A: local output from `git log`
B: output from a log file
C: ssh to some server where we're going to do make some changes

Let's say we want to do the following:
* grab a git SHA from pane A
* copy a long file path from pane B
* in pane C compose a git command using the SHA from A and the path from B

Most of us would do the following:
* move the mouse to A, click, drag, copy the SHA
* move the mouse click on C and paste the SHA
* move the mouse to B, click, drag, copy the path
* move the mouse to C, click, paste the path
* movement between panes: A -> C -> B -> C

With tmux, there are a few advantages:
* no mouse involvement
* jump to A, enter copy mode, yank SHA
* jump to B, enter copy mode, yank path
* jump to C, paste SHA, paste path (thanks multiple paste buffers!)
* movement between panes: A -> B -> C

This is a fairly simple example - the more complex the task and the more 
sources for components of the command, the more valuable this feature becomes.

There are plenty of tools that provide similar behavior. If you're already using
one of them, this feature will be less of a gamechanger. It's still worth checking
out though!

## Scripting dev environment startup
I can safely say I spent *at least* 1 minute everyday messing around with my terminal.
It was a mess: my first tab usually had my local server running; my second tab would 
have a REPL; then next 10+ tabs were complete anarchy. There was a mental cost involved
in figuring out which tab I needed to go to. When I'd get started in the morning, I had
a ritual of cycling through my open terminal tabs. Closing tabs, restarting services,
etc. as I moved along. In the case of a restart, I'd have a to spend 30 seconds getting
everything set up again.

With tmux none of these issues remain because:
* my tmux session starts up with all of the windows I need; they're all named from the getgo. 
* having named windows (they're like tabs) discourages me from repurposing a window and creating confusion. I'm not going to fire up a server in a window called vim. That would be madness.
* Jumping to an existing window is easier than opening and naming a new one. This broke me out of my anti-pattern of opening tabs willynilly and creating cognitive overhead for my future self. Everything has its place now.
* in case of a restart (or if I manage to bork my tmux session -- haven't yet!) I just run 1 command and it all springs back to life. Beautiful!

This aspect of tmux becomes an even greater strength, if you're working on multiple projects.
Right now I have 2 tmux sessions running: one for rails development and another for elixir experimentation.
Before, I may have been tempted to just open a few more tabs for my elixir work.
No doubt, when I returned to rails-mode, I would have closed or repurposed those elixir
tabs at some point. Then, when it was time to go back to elixir work, I'd have to go through the process
of opening everything up again. It's almost embarrassing to write that now.
Now my elixir session is waiting patiently for me to return to it.


