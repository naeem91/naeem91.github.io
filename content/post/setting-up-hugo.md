---
title: "Setting Up Hugo"
date: 2022-07-16T00:22:14+05:00
draft: false
categories: ["Hugo", "static site"]
---
## Installing and using Hugo
Hugo is a static site generator tool built with the Go language.
I was just reading some random blog and at the bottom of their page found `built with Hugo` thing. After checking it I decided to give it a try, not knowing that I already have a gh pages hosted blog using Jekyll, which I never used after the first time.

Here's how to use Hugo to generate a static site and then host it on Github pages:

## Usage

Installation is pretty straightforward:

On Mac:
```
brew install hugo
```
On Ubuntu:
```
sudo snap install hugo
```

After installing it, you [create a site](https://gohugo.io/getting-started/quick-start/#step-2-create-a-new-site), author pages, posts and other type of content using the [markdown language](https://www.markdownguide.org/cheat-sheet/).

On your local machine, you can run the hugo server to see how the site looks in the browser.
That's pretty much all about the installation and basic usage.

## Hosting on Github Pages
There are various options to [host your hugo blog](https://gohugo.io/categories/hosting-and-deployment). I chose to host it on Github Pages. 
This blog's GH actions setup can be found [here](https://github.com/naeem91/naeem91.github.io/blob/master/.github/workflows/gh-pages.yml).
This GH action:
- On push of `master` branch:
	- Runs a `deploy` job which:
		- Checksout code
		- Installs Hugo
		- Builds the static site
		- Pushes the generated site to `gh-pages` branch.

The prereq is that your repo's Github pages settings (found at your-repo/settings/pages) are set to deploy from the `gh-pages` branch.


