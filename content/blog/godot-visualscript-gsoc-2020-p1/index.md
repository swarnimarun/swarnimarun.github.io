---
title: "VisualScript Godot GSOC 2020 Progress Report #1"
date: "2020-07-20T22:10:03.284Z"
description: ""
---

There are a lot of different small things that I have worked on this summer for the project, but let's keep it short and categorize them in two main blocks like I did in mmy proposal.
The essence of this work is to make the Visual Scripts better in ease of use and accessiblity.

## VisualScript Refactoring (drafted working PR)
Visual Script had been incurring a lot of technical debt from my work last year and other things that have been done to improve it, though I can't say we don't have much more to refactor but we are done with a large part of it and even ended up with a small feature enchancement. And likely enough for this summer to move on to the next task(discussed later).

Without getting into the technical details, I redone parts to remove extras and hacks, that had been used before and to try to make it easier for future changes(to be seen how much easier..).

As for the small feature enchancement produced from it, is the ability to use nodes from multiple functions remove the need for duplication of code.

Example image(from master branch with my PR on top),
![image](https://user-images.githubusercontent.com/19930870/87987481-567fb200-cafc-11ea-82dc-fb91d1dc15ce.png)


## Submodules, Groups or just plain Macros (WIP still not completely usable)
As you can already see I am on the fence about the naming, I think a better name might be deserved so suggestions are welcome(in the comments to the blog).
This is the main objective of this summer and can involve a lot of different features but the primary features that it deals with is being able to have function like blocks of VisualScript code that allow us to reuse them without restricting them to functions from the Godot system itself.

The feature is currently made of GUI parts and internal data classes that will hold of the stuff like VisualScript but allow us to detach them from the VisualScript themselves and have a well-defined API to use reuse them in multiple VisualScripts without issues, such as saved node groups/modules in Blender.

The feature is lacking both finish and feature completeness but here's a sample anyways,
![sample](https://user-images.githubusercontent.com/19930870/87987641-96469980-cafc-11ea-855d-0b65ca341cee.gif)


### Note
This was a small progress update but I am thinking about more research and feedback driven development as soon as I draft a working PR for submodules.

I will be keeping everyone posted on my blog, in a weekly or bi-weekly manner outside of the Godot Official Progress Reports and will ask for feedback in comments or forms and be sharing some testing builds if anyone is interested. basically a bug hunting trip.


### Extra
Other than that I will try to look at ways to improve the parts of Godot I worked on(depending on the free time I have), once everything is done this summer. Like Theme Editor, adding submodules to Visual Shader so pls feel free to suggest stuff that you think could help with anything you are having issues with.