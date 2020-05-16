---
title: Setting up Spacemacs as a C++ IDE
author: Chris Haslehurst
---
I've just started this blog so that I can document my progress on getting Spacemacs setup as a C++ IDE. That's how much I want to avoid people having to replicate the last couple of weeks of tinkering and googling. It wasn't fun.

## Why?

A few weeks ago, in a flurry of lockdown fuelled madness, I decided to replace my laptop's OS with Ubuntu Linux. I didn't do this for any reason other than I hadn't used Linux before and all the cool kids seem to be using it and talking about how awesome it is for developers. 

I took the plunge. And I like it.

The problem arose when I decided to do some C++ development on a little side project and realised.. Oh. No Visual Studio here.

I've done most of my C++ programming within that sluggish behemoth of an IDE and didn't fancy living without all those nice features. Especially if any of my side projects became fairly large.

A colleague of mine had been encouraging me to try Vim for a while. I gave it a whirl and liked the modal editing style, but wasn't sure if it could provide all those tasty IDE features (I still don't know, I didn't really pursue Vim!). I've used Emacs a little in the past, the level of customisation and the ecosystem of packages seemed perfect for getting my setup just how I want it. The problem is, I really don't like the keybindings (a lot of holding down keys with your pinky finger seems like a recipe for RSI). After a bit of googling around, I found Spacemacs. Spacemacs is a layer on top of Emacs which gives Vim style editing with Emacs level tinkering, it sounded perfect.

It was at this point I saw Atila Neves lightning talk from CPPCon 2015 ( https://www.youtube.com/watch?v=5FQwQ0QWBTU ) on using Emacs as a C++ IDE. I've been playing around with CMake and use it for all my C++ projects now, so the idea of getting all my IDE features in a lightweight(ish) cross platform editor sounded GREAT.

So with all this in place, I set out to get Spacemacs working as a C++ IDE. This has not proven to be an easy endeavour so far, and so this blog post is as much road map for confused future travellers as it is breadcrumb trail for me to find my way back if I ever have to do this again.

*Like so many things I start, I'm not done with this yet, so expect this to receive updates as I tinker with my setup.**

## What?

Like any good project, I started by gathering requirements. What do I **need** in my editor to be productive and to enjoy my programming experience. I came up with the following list:

- **Code Navigation** (Jump to Symbol, Jump to Definition, Find References, Find file in project etc.)
- **Syntax Checking and Highlighting** (Sure, your compiler can tell you, but it's great to have real time indicators you've done something incorrect)
- **AutoCompletion** (I find this vital when working with unfamiliar APIs so I don't have to constantly be tabbing over to documentation)
- **Compiling within the editor** (Preferably on one button!)
- **Visual Debugging** (I took a look at GDB command line debugging and after a decade of using a visual debugger decided this was a deal breaker)

## How?

It turns out that once you know how, setting all this up actually doesn't take a ton of work.

This assumes a Linux environment, it might all be the same on windows, it might be a mangled hellscape, I don't know, I've not tried it. It also assumes you're using CMake as your build system. Setting up CMake for your project is required for this stuff to work, but is beyond the scope of this post to explain!

#### Step One - Install dependencies

I'm not going to go into the details of *how* to install these, but you're going to want all of them installed.

- Spacemacs - Somewhat obvious.
- CMake - for setting up your build system primarily, but it's required for cmake-ide to work.
- CLang - provides the backend for syntax highlighting, auto complete and compiling your code.
- RTags - RTags indexes your code and keeps a database of references, declarations and symbolnames to allow for code navigation. It also allows for live updates of compiler errors and warnings which is REALLY cool: https://github.com/Andersbakken/rtags

#### Step Two - Add the following to your spacemacs dotfile

In your configuration layers:

```lisp
dotspacemacs-configuration-layers
   '(
     (c-c++ :variables
            c-c++-enable-clang-support t
            c-c++-backend 'rtags
            c-c++-default-mode-for-headers 'c++-mode)
     (cmake :variables cmake-enable-cmake-ide-support t)
     helm
     auto-completion 
     syntax-checking
     )
```

And in your user-config function:

```lisp
  (require 'rtags) 
  (require 'company-rtags)
  (require 'company-c-headers)

  (setq rtags-autostart-diagnostics t)
  (rtags-enable-standard-keybindings)

  (spacemacs|add-company-backends
    :backends company-c-headers company-clang
    :modes c++-mode)

  (cmake-ide-setup)

```
#### Step Three - Profit?

I think that's it. 

It's incredibly underwhelming that after all the googling and frustration of figuring out what goes where, that's all this post has boiled down to, but there you go!

If you try this and run into any problems, please do get in touch in the comments as I'm eager to iron out any potential issues. I saw a lot of posts in my time figuring this out with incomplete information and it was really frustrating to try to figure out what I was doing wrong.
## todo...

So I said this all works right? That was partially true. This setup is still in its proto stages. I can jump to or find symbol, but I have to navigate through spacemacs menus to do it. I haven't setup any hotkeys really and I've yet to do any real development work to find where the sticky bits are.

I've also not even touched visual debugging yet, which as I mentioned above is a deal breaker.

When I get to these features I'll return to this post and update it, in the hopes of building a proper guide. I just needed to get down what it's taken me a long time to figure out so far.

Let me know how you get on, and if you have any suggestions for improving this setup, or adding to it!

### Update: VS Code

So erm... this is awkward. Visual Studio Code does pretty much everything I wanted from this setup, but it's easier to configure, better documented and has a more modern UI. It's still nice and lightweight and you can even get Vim bindings for it if you want. I decided to stop messing around with spacemacs and actually do some development work, using VS Code.

I'm having a much nicer time.
