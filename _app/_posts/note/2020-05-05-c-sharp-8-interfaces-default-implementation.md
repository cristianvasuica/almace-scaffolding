---
layout: post
title: C# 8.0 new features: Interfaces default implementation
category: note
tags: c# 8.0 features
---

In 8.0 version there were addded a couple of new features to the language which are worth checking out. We will do so with a series of articles dedicated to them.

Today we will check on Interfaces Default implementation. This feature is available starting with .NET Core 3.0 and of course C# 8.0 compiler. This compiler is available in Visual Studio 2019 starting with version 16.3 or with .NET Core 3.0 SDK.

Which problems are solved by this feature

Lets suppose that you have written a nice API with some public interfaces and released it to the world. Version 1.0 was highly appreaciated and users have started to make use of it, but as it happens in software development you need to extend your code to support newly requested functionalities. That's great! But what happens when with the new code changes you are forced to do changes to the publically exposed interfaces?
Well if the users of your API have just referenced your interfaces, but have not implemented them they will not be affected by any addition of new features.
But what if they created their own types implementing your interfaces?
Well, prior to C# 8.0 that would have ended in compilation errors. Now, when it is the case to extend your interfaces and you fear of this situation, you can also provide a default implementation.
//add some code here


## The Problem

In short answer: yes, but additional actions required.

tl;dr: You can serve AMSF as a static site on GitHub Pages, but not a Jekyll site using Jekyll renderer provided by GitHub Pages.

There're some factors that prevent it from generating pages using GitHub Pages renderer:

- Many features Almace Scaffolding provides like LiveReload, Sass support, inline SVG, and HTML minification are implemented using [Grunt.js](https://gruntjs.com/), it's not supported by GitHub Pages.
- Almace Scaffolding uses the latest pre-release Jekyll, so not all features are supported by GitHub Pages renderers.
- GItHub Pages build server [overwrites the `source` settings](https://help.github.com/articles/pages-don-t-build-unable-to-run-jekyll#source-setting). This prevents it from generating pages from current file structure.

## The Solution for Users or Organization Sites

Since GitHub Pages for users or organization sites can only be served from the root directory of your master branch. You have to:

- Make sure your `baseurl` is set to `""` (empty) in your `_config.yml`.
- Build your site locally (`grunt build`).
- Use your own method, create a script, bash, whatever it works to move the generated pages to the root directory of your repository.
- Upload Jekyll generated static files to your `username.github.io` repository.

If you'd like to keep all things under Git control, you can try the following file structure:

```
├── _amsf/ (Almace Scaffolding source code)
├── *.html (Jekyll-generated static pages)
└── README.md (your own readme)
```

You can see this [live demo](https://github.com/amsf/amsf.github.io/) how it actually works.

## The Solution for Project Sites

Things can be simpler if you need AMSF for your project sites since GitHub Pages supports serve your site from a subdirectory:

- Make the following changes in your `_config.yml`:
  - Change `destination` to `docs`
  - Change `baseurl` to the name of your repository slug, ie. `/my-project`.
  - Change `flatten_base` to `true`.
- Build your site locally (`grunt build`).
- Push changes to GitHub
