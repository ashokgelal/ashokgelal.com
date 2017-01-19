---
title: Automatically setting color scheme for .leaf files in Xcode
date: 2017-01-19 10:10:03
tags:
- vapor 
- xcode
- colors
---

Unlike AppCode, Xcode doesn't allow you to associate a custom file extension with a color scheme. When using Vapor and Leaf, this means you have to go to `Editor > Syntax Coloring` and select `HTML` every time you open a *.leaf* file. This is annoying and to make things worse Xcode doesn't remember this setting after you (re)build the project 😡

To fix this annoyance, I've made [a very tiny MacOS app][1] that automatically associates *.leaf* to *.html* file for you. All you have to [download][2] this tiny app, and double-click it. You can then close the app. No further action required! You can now open your .leaf file and Xcode will recognize it as an HTML file and automatically sets syntax coloring for you.

Download the app here: https://github.com/ashokgelal/xcode-leaf-color-schemer/releases

The source is open and on GitHub: https://github.com/ashokgelal/xcode-leaf-color-schemer

[1]: https://github.com/ashokgelal/xcode-leaf-color-schemer
[2]: https://github.com/ashokgelal/xcode-leaf-color-schemer/releases