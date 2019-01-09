---
layout: single
title: "Nick that formula like a Pro"
excerpt: "If you ever struggled to replicate this tedious formula from a paper this nice tool might be for you"
header:
  teaser: assets/images/equations.jpg
  overlay_image: /assets/images/equations.jpg
categories: Tools
tags: 
- Latex
- Science
toc: false
date: 2019-01-09
---

Ok, this is going to be a shorty. I recently needed some nice formulas from a scientific paper for a [presentation](https://www.christianwerner.net/tech/Deep-Learning-for-Remote-Sensing-Applications/) and usually I try to just copy them from the source PDF since [Keynote.app](https://www.apple.com/lae/keynote/) is pretty good at incorporating high-quality PDF snippets into a slide.

However, once you want to edit the formula (to match symbols or variable names) you have to tediously compose it by hand. For Keynote people like myself there is also the option since mid 2018 to just enter LaTeX or MathML code and have it render beautifully on the slides. For Word or Powerpoint folks adding formulas usually means using the clunky Microsoft Equation Editor. However, it seems Office 365 now supports to enter formulas using LaTeX syntax, too, but I'm still on Office 2016 here. 

Anyways, depending on your LaTeX and math skills bigger or more fancy equations still require you to put quite some effort into composing the actual code that gives you the nice formula. 

But fear not - with [MathPix](https://www.mathpix.com) this workflow is amazingly simple (not endorsed by the developers, I just discovered their tool recently and love it). Their page probably says it best: "Take a screenshot of math and paste the LaTex into your editor, all with a single keyboard shortcut." Nice! Oh, and it's free! 

The app used OCR to trace the equation and convert it into LaTeX formula syntax which you can paste into any editor or app that can deal with it. And that's it really. 

{%
include figure 
image_path="/assets/images/posts/mathpix.png" 
alt="MathPix" 
caption="MathPix: Take a screenshot of math and paste the LaTeX into your editor, all with a single keyboard shortcut"
%}

## Steps
1. Grab the app from here: [Mac](https://mathpix.com/dmg/snip.dmg), [Win](https://mathpix.com/win_app/mathpix_snipping_tool_setup.exe), [Ubuntu](https://snapcraft.io/mathpix-snipping-tool)
2. Open your source PDF
3. Hit Ctrl + ⌘ + M (Mac) or Ctrl + Alt + M (Win/ Linux)
4. Select the formula you want to extract by drawing a bounding box over it
5. Pick one of the suggested formats
6. Paste it into where-ever 
7. Done

## Some examples 
Coming up some tests with various equations. The numbers indicate the source (1), the MathPix detection (2) and the final rendered equation in Keynote (3). The red marker indicates the equation used in the example.

### Simple stuff: a sigmoid function
No problem at all (not shown).

### More advanced: regularized loss function of a NN
{%
include figure 
image_path="/assets/images/posts/mathpix_clearly.png" 
alt="Example Equation 2" 
caption="An example from a scientific paper: a L1 loss function regularization (source: He & Yokoya (2018), ISPRS Int. J. Geo-Inf. 7, 389; [doi:10.3390/ijgi7100389](https://www.mdpi.com/2220-9964/7/10/389))"
%}

### Advanced but low quality
A quick test how a low res equation scan works out (go to source for actual resolution).
{%
include figure 
image_path="/assets/images/posts/mathpix_just.png" 
alt="Example Equation 3" 
caption="Some random equation from the web from a low quality scan ([source](https://math.stackexchange.com/questions/960831/covariance-of-states-of-a-finite-markov-chain))"
%}


### Matrix stuff: detection ok, but Keynote bails
MathPix manages to detect this formula but Keynote gives an error when rendering it.

{%
include figure 
image_path="/assets/images/posts/mathpix_notquite.png" 
alt="Example Equation 4" 
caption="A rotation matrix from wikipedia ([source](https://en.wikipedia.org/wiki/Rotation_matrix))"
%}

### Too hard: big Matrix
Ok, this definitively seems to be too hard for the little app - MathPix bails.

{%
include figure 
image_path="/assets/images/posts/mathpix_fail.png" 
alt="Example Equation 5" 
caption="Description of neural net weight ([source](https://medium.com/@erikhallstrm/backpropagation-from-the-beginning-77356edf427d))"
%}

# Summary
A really neat tool that stays in my menubar for sure!