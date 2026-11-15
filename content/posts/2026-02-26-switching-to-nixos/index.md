---
title: "I Switched to NixOS and I Can Never Go Back"
date: 2026-02-24T16:21:14-05:00
draft: true
toc: true
description: "The story of how I learned to hate NixOS, then learned to love it. Alternative title: \"NixOS is boring. That's why I love it.\""
tags:
  - Linux
  - Nix
  - IaC
  - Open Source
---

![The "After all, why not? Why shouldn't I..." Bilbo Baggins meme. The top panel reads "After all, why shouldn't I?" and the bottom panel reads "Why shouldn't I spend an entire summer configuring NixOS to then only use it on 1 machine"](001.png "Credit: /u/spcbfr on Reddit")

## Part z3r0: Background

My [last post](http://localhost:1313/posts/2024-07-21-yubikey-setup/) (from July 2024!) starts with a note including this text:

> I am in the middle of migrating to NixOS anyway.

At the time, I truly meant it!
I had a GitHub repo set up with my NixOS configuration and about 30% of the changes I made worked first try.

The problem is, the note continues to say this:

> In the interest of finally getting this blog post out, I have opted to finish writing this post in WSL2 on my Windows machine.

...and there it is.
The "temporary solution" that never goes away.
I had come to truly despise Windows, but kept it around for a few games that I played with my friends that did not (at the time) work under Proton.
Then, I got busy.
I became a volunteer firefighter, moved in with my girlfriend, started the fire academy, then I was too busy with work, and then...
you get it.
I was always "too busy" to fix my Linux setup, so I kept suffering Windows for the occasions where I would get to spend time on my computer.

A few months ago, I had a little bit of free time and reinstalled Arch Linux on my main desktop.
It felt good to go back to actually daily driving Linux (I used almost exclusively Arch Linux during college and even at my first job out of college), but I couldn't help feeling like I was wasting my time.
It took me about two days to get my system to what I would consider a fully usable setup, which meant that I could play a few games and work on [my chess engine](https://gitlab.com/klercke/protochess) (which will be a blog post of its own), but it wasn't as easy as I liked.
I had been using the excellent [dotdrop](https://github.com/deadc0de6/dotdrop) tool for managing my dotfiles, but I found myself annoyed that I still had to remember all of the packages I had to install in order for everything to work.
In the past, I used a pacman hook to update a GitHub Gist with a list of every package I had installed, but that was less than an ideal solution.
It was also frustrating knowing that I have quite a few Linux machines that I regularly use (my desktop, my laptop, and WSL on my work PC) and any change I made on one of these machines would need to be replicated on the others, which was easier said than done due to these machines being a mix of Arch and Fedora.
As soon as I got my new Arch installation configured to my liking, I knew that it was time to start over and install NixOS.

So why didn't I just install NixOS in the first place?
I was scared.
I had first tried to switch to NixOS a year ago (on my girlfriend's birthday apparently, based on my commit log), but ultimately ended up abandoning it due to a few reasons:

1. It was painfully slow.
  Looking back, I think that this was ultimately my fault.
  Not wanting to fully commit to NixOS at the time, I wasn't going to fully replace my Windows drive or even my broken Arch drive with NixOS and having just moved, I didn't have the money to buy a new drive, so I just repurposed an old hard drive I had laying around.
  I figured it would be good enough to experiment with NixOS and I could always reinstall on a faster disk if I liked it.
  Unforunately, likely due to this drive, build times were unbearably slow.
  As in, "go make a coffee" slow.
  This made any sort of iteration *painful*, especially when I didn't really know what I was doing, so most of my builds would fail, which just meant more waiting.

2. I was lost.
  Part of this is certainly through my skimming through the documentation I found, to be sure, but a big part of it is that the NixOS documentation was *hot garbage*.
  Luckily, it has slightly improved now, but "lukewarm garbage" is still not not the ideal state for the documentation of your OS.
  While NixOS was not necessarily difficult to use, things started to get difficult when you have to learn about flakes, Home Manager, and the Nix language itself in order to configure it as you likely want to for a desktop setup.
  Like any good Linux user born after Y2K, I tried watching Youtube videos claiming to show "THE BEST WAY TO SET UP NIXOS" and their configurations all worked fine, but I still could not figure out how to customize anything to my liking.
  Having to learn the confusing Nix language in order to use the dotfiles that I've been using for years without issue was not a pleasant experience.

3. The Nix community was lost too.
  As alluded to in point #2, the Nix ecosystem is extremely confusing.
  You have Nix, the language, Nix, the package manager, NixOS, which is the Linux distro based on the Nix package manager, and Home Manager, which uses the Nix language and is configured similiarly to NixOS.
  Then you have flakes, which are considered an experimental feature, but they're extremely popular, so half of the documentation online assumes you're using flakes and won't work without them, while the other half won't work with flakes and the novice Nix user can't tell the difference between the two.

