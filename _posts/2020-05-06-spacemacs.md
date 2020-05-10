---
title: Setting up Spacemacs as a C++ IDE
author: Chris Haslehurst
---

A few weeks ago, in a flurry of lockdown fuelled madness, I decided to replace my laptop's OS with Ubuntu Linux. I didn't do this for any reason other than I hadn't used Linux before and all the cool kids seem to be using it and talking about how awesome it is for developers. I took the plunge. And I like it.

The problem arose when I decided to do some C++ development on a little side project and realised.. Oh. No Visual Studio here.

I've done most of my programming within that sluggish behemoth of an IDE and didn't fancy living without all those nice features. Especially if any of my side projects became fairly large.

A colleague of mine had been encouraging me to try Vim for a while. I gave it a whirl and liked the modal editing style, but wasn't sure if it could provide all those tasty IDE features (I still don't know, I didn't really pursue Vim!). I've used Emacs a little in the past, the level of customisation and the ecosystem of packages seemed perfect for getting my setup just how i want it. The problem is, I really don't like the keybindings (a lot of holding down keys with your pinky finger seems like a recipe for RSI). After a bit of googling around, I found Spacemacs. Spacemacs is a layer on top of Emacs which gives Vim style editing with Emacs level tinkering, it sounded perfect.

It was at this point I saw Atila Neves lightning talk from CPPCon 2015 (https://www.youtube.com/watch?v=5FQwQ0QWBTU) on using Emacs as a C++ IDE. I've been playing around with CMake and use it for all my C++ projects now, so the idea of getting all my IDE features in a lightweight(ish) cross platform editor sounded GREAT.

So with all this in place, I set out to get Spacemacs working as a C++ IDE. This has not proven to be an easy endeavour so far, and so this blog post is as much road map for confused future travellers as it is breadcrumb trail for me to find my way back if I ever have to do this again.

*Like so many things I start, I'm not done with this yet, so expect this to receive updates as I tinker with my setup.*
