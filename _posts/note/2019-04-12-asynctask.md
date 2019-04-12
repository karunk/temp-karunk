---
layout: post
title: AsyncTask 
category: note
tags: project
desc: Making asyncronous jobs transactional・非同期ジョブをトランザクションにする! <br><br><a class="github-button" href="https://github.com/karunk/asynctask" data-icon="octicon-star" data-size="large" aria-label="Star ntkme/github-buttons on GitHub">View on Github</a>
heading-bg: img/sidekiq.png
heading-bg-local: true
heading-bg-color: "#070708"
heading-bg-size: "cover"
heading-bg-repeat: "no-repeat"
heading-bg-text: "#fff"
---

<!-- Place this tag in your head or just before your close body tag. -->
<script async defer src="https://buttons.github.io/buttons.js"></script>
## The Problem


In short answer: yes, but additional actions required.

tl;dr: You can serve AMSF as a static site on GitHub Pages, but not a Jekyll site using Jekyll renderer provided by GitHub Pages.

There're some factors that prevent it from generating pages using GitHub Pages renderer:

- Many features Almace Scaffolding provides like LiveReload, Sass support, inline SVG, and HTML minification are implemented using [Grunt.js](https://gruntjs.com/), it's not supported by GitHub Pages.
- Almace Scaffolding uses the latest pre-release Jekyll, so not all features are supported by GitHub Pages renderers.
- GItHub Pages build server [overwrites the `source` settings](https://help.github.com/articles/pages-don-t-build-unable-to-run-jekyll#source-setting). This prevent it generating pages from current file structure.

## The Solution for Users or Organization Sites

Since GitHub Pages for users or organization sites can only be served from the root directoy of your master branch. You have to:

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
